---
layout: article
title: Fully Convolutional Network 图像语义分割
tag: Semantic Segmentation
excerpt: 首次采用全卷积网络实现语义分割任务
---

> Long J, Shelhamer E, Darrell T. Fully convolutional networks for semantic segmentation[C]
>
> Proceedings of the IEEE conference on computer vision and pattern recognition. 2015: 3431-3440.



# 贡献

- 首次构建**完全卷积(fully-conv)** 语义网络，可接受任意大小的输入

- 提出了**反卷积层(deconv layer)**,可增大feature map尺寸，输出精细的结果

- 提出了**skip architecture**，能够结合不同深度层的信息，提高结果的精度和效果。

# 网络结构
![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200304211505.png)

- 网络包括卷积部分，skip architecture，以及反卷积部分

## 1.全卷积部分
- 卷积部分可接收任意大小的输入，对于不同尺寸的输入图像，各层数据的尺寸（height，width）相应变化，深度（channel）不变。
- 卷积部分采用成熟的分类网络改造而来，把他们最后的全连接层改为卷积层。

## 2.逐像素预测

- 虚线下半部分，从卷积的不同阶段，以卷积层预测深度为21(类别总数)的分类结果。

  > 例：第一个预测模块
  > 输入16 *16 * 4096，卷积模板尺寸1 * 1，输出16 * 16 * 21。
  > 相当于对每个像素施加一个全连接层，从4096维特征，预测21类结果。

## 3.反卷积（上采样）

- 通过反卷积操作（橙色）将feature map的尺寸扩大，滤波器的参数由学习得到。

- 反卷积(transposed convolution)的操作示意如下

  ![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200304213601.gif)

## 4.跳级结构（skip architecture）

- 在虚线下半部分，将不同阶段卷积层的结果相加（黄色×2）

- 把不同深度的预测结果融合，较深的结果比较鲁棒，较浅的结果更为精细

- 融合之前，使用裁剪层统一大小（灰色×2）

  ![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200304214712.png)


# 训练

训练主要分为四个阶段

## 第一阶段

![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200305101348.png)

首先以经典的分类网络作为初始化，继承他们训练好的参数，最后两层全连接层的参数舍弃

## 第二阶段

![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200305101324.png)

- 从feature map(16 * 16 * 4096)进行预测，得到分割小图 (16 * 16 * 21)

- 分割小图进行反卷积（transposed convolution）升采样，步长为32，这个网络称为FCN-32s

- 对这个网络进行单独训练，得到各参数

## 第三阶段
![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200305100947.png)

- 把第四个池化层（绿色）进行预测（添加一个1 * 1 的卷积层），得到蓝色结果。

- skip-architecture：进行两次升采样（橙色×2），统一大小后进行融合。

- 融合后结果进行反卷积升采样，步长为16，这个网络称为FCN-16s。

- 将第二阶段的参数作为初始化，训练其他参数。

## 第四阶段

  ![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200305101533.png)

- 对pool3,pool4,conv7的结果分别进行融合。

- 升采样分为三次进行(橙色×3)。

- 最后一次反卷积升采样，步长为8，这个网络称为FCN-8s。

- 训练得到全部的参数。

## 参数设置
- 分类网络以外的卷积层参数初始化为0。
- 反卷积参数初始化为双线性插值。最后一层反卷积固定为双线性插值不进行学习。

# 结果
![](https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200305101930.png)

三个网络的预测结果如上图所示。较浅层的预测结果包含较多的细节信息，跳级结构通过融合不同深度的信息，可以得到更为精细的效果。

# 总结
## 其他方法
- 作者有考虑采用其他提高结果精细度的方法。
	- **减小池化层的步长**。 在此情况下，要使卷积网络的感受野不变，需要增大卷积核的尺寸，这会增加计算负担且难以进行学习。而且初始化采用的是预训练好的分类网络参数，导致结果并不理想。
	- **shift-and-stitch 技巧**。即对输入进行shift，得到多个结果，将他们进行融合，得到精细的结果。但经实验此种方法并不如直接学习升采样层的参数效果好。

## 结论
- 本文首次把分类网络扩展到语义分割领域，通过设计的跳级融合结构取得了不错的效果。
- 想要精确预测每个像素的分割结果，必须经历从大到小、再从小到大的过程。
- 在升采样过程中，分阶段增大比一步到位的效果更好。
- 在升采样的每个阶段，使用浅层的信息进行辅助。
- 网络对单张图片的预测时间在175ms，速度较慢。
