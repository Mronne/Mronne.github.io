---
layout: article
title: （十一）无监督学习
tag: [机器学习课程,无监督学习,deep learning]
excerpt: 介绍无监督学习的基本情况
---
[toc]
# 概述
- Clustering(分类)
- Generation(生成式)

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pA9BkV9DUaCi*GwLue9bKvVcFljT0tg8T0mKJ07JHnegiJm*55c4Na*P2V.SQIDS7ntOP.chpIze*VuB9ifhJmM!/b&bo=egWzAgAAAAADB.w!&rf=viewer_4)

# 1. Clustering
## 1.1 传统聚类方法
### 1.1.1 K-means
- 将`$X={x^1,...,x^n,...x^N}$`分成K类
- 初始化聚类中心`$c^i,i=1,2,...,K$`(从样本K中随机挑选)
- 重复以下步骤：
    - 对于X中所有样本：判断其类别
    - 更新聚类中心`$c^i$`
```math
b_i^n = \begin{cases}
   1 & x^n\text{ is most "close" to } c^i \\
   0 &\text{Otherwise }
\end{cases}
```

```math
c^i=\sum_{x^n}b_i^nx^n/\sum_{x^n}b_i^n
```

### 1.1.2 Hierarchical Agglomerative Clustering(HAC)
- 依据相似度建立树结构
- 选择阈值
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pKg9NYiifvtJozycfMVze3rf1*f2rbdQq9KFDTjurgOkXp17FcQWX4XhJtdwDZGaOKgAEvo986VyMWQfq4oTJtk!/b&bo=wASIAgAAAAADB2w!&rf=viewer_4)

## 1.2 Distributed Representation
- 把样本直接确定其属于哪一类，以偏概全
- 其实确定分布情况相当于Dimension Reduction，即用维数较小的特征向量表示原来的信息

# 2. Dimension Reduction
- 核心是求解一个函数，输入为x，输出为z，z的维度比x的维度小

## 2.1 Feature selection
- 考虑x的分布情况，选择其分布较多的维度。可用范围很窄

## 2.2 主成分分析 Principle component analysis(PCA)

# 3. 主成分分析 Principle component analysis(PCA) 线性降维
```math
z=Wx
```
## 3.1 一维情况
- 降维到一维：`$z_1=w^1 \cdot x$`
- 假设：`$\|w^1\|_2=1$`
- 此时`$z_1$`实际是x在`$w^1$`上的投影
- 选择`$w^1$`，希望投影后的`$z_1$`的方差尽可能大
- Formulation:
```math
Var(z_1)=\sum_{z_1}(z_1-\bar{z}_1)^2\\[0.5em]
\|w^1\|_2=1
```
## 3.2 多维情况
- 先按上述方法求解1维情形
- 再将其组合成为`$W$`矩阵，在求解时注意正交约束
- 此处由于`$w^i$`之间相互正交，因此矩阵`$W$`是正交矩阵(Orthogonal Matrix)。
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pP4H5lZOwhZdR6ZIqA0Pp6Pqj1.QZzUvFGO2YTw*AfRmUjtVKJFs7pI9arjCjx6jqzcTCawAogMgfvb9ZwI7FFA!/b&bo=aQNbAgAAAAADBxE!&rf=viewer_4)

## 3.3 拉格朗日乘数法(Lagrange multiplier) 求解`$w^i$`
- 经过变形可将问题转换为在约束条件下的求解目标函数的最大值问题
```math
w^1 = \max_{w^1} (w^1)^T \bold{S}w^1\\
s.t. \quad \|w^1\|_2=(w^1)^Tw^1=1
```
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pCaXKESYYtblnJTHQtdiTczAXOzr2yEv2CMLTrqxrsayQKoheP3X7QCa*tWp6R233wOR8dwi52iYvEI.D6ccPQw!/b&bo=vgPLAgAAAAADB1Y!&rf=viewer_4)

- 采用拉格朗日乘数法求极值，最后求得`$w^1$`实际是`$X$`的协方差矩阵`$\bold{S}$`最大的特征值对应的特征向量
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pM5N2ju491LpUw9BfKaige29jXr8Undg2hu4yOIon6MIrwPlZaNDU8C*aPzCp94N5563CWxJcgD5O1.jx.k0xvM!/b&bo=sAPBAgAAAAADB1I!&rf=viewer_4)


- 求解`$w^2$`是`$X$`的协方差矩阵`$\bold{S}$`第二大的特征值对应的特征向量
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pDasxaTcyL1jTcYJyiUBtmMyAg6WgLWv05e0MVSU134DH8moWSl7z3TOPLinHDz5sqWJ4eXTTTyr45F7tWnRdCw!/b&bo=ugPMAgAAAAARB0c!&rf=viewer_4)

## 3.4 去相关（decorrelation）
- 不同维度的`$z$`间的协方差为0，即`$Cov(z)=D$`为对角矩阵(Diagonal matrix)
- 后续再使用`$z$`用于其他训练时，可以使用较为简单的模型
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pKttqhYDiD5em*4JUYwwLyBcH6s6b6FyqMMlXo04l*MAefU.rYsGqe6Wg*GTTrUD*YOknJxpciuAYTlm5HXRERs!/b&bo=ugPMAgAAAAARB0c!&rf=viewer_4)

## 3.5 另一个角度的PCA
假设用x的组成元素来重建x
```math
x=c_1u^1+c_2u^2+...+c_Ku^K+\bar{x}
```
- 记`$\hat{x}=x-\bar{x}=c_1u^1+c_2u^2+...+c_Ku^K$`
- 定义重建误差，其实是求解组成元素来使重建误差值最小
```math
\|(x-\bar{x})-\hat{x}\|_2\\[0.6em]
L=\min_{\{u^1,...,u^K\}}\sum\bigg\|(x-\bar{x})-\bigg(\sum_{k=1}^Kc_ku^k\bigg) \bigg\|_2
```

- 用PCA求得的解`${\{w^1,w^2,...,w^K\}}$`即是使得上式L最小的组成元素`${\{u^1,u^2,...,u^K\}}$`
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pEFKsLyejc081kj2DTOuiN6pZwBlExytkOu0CLD.kgCJWIZpnxMIhxikVhR60MTe7uQXL4Sh0v.AhDltHqAjs18!/b&bo=oAU4BAAAAAARB6k!&rf=viewer_4)

- 采用SVD方法对矩阵进行分解
```math
X=U \Sigma V
```
- 矩阵U是`$XX^T$`的前k大的特征值对应的特征向量

## 3.6 PCA的缺点
- PCA的降维丢失了部分的信息
- PCA是线性的
- PCA中的权值可以是正是负，这样的话求出来的组件并不是原信息的组成部分

## 3.7 Non-negative matrix factorization(NMF)
- 令权值必须为正
- 求得的特征向量也必须是正的

# 4. Word Embedding
将单词表示为向量
- Word Class
- 从大量的文本中通过上下文学习词汇含义
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pKIXru*vs8F2BlQII7*UsdLjn9N.Y11kwkg2IeFoSlOvVaqdtKTVQeLzzk*mn9gED4C5cV8qVCaS52tnShdezyw!/b&bo=1gJQAgAAAAARB7Y!&rf=viewer_4)

## 4.1 Count based
如果两个词汇在一篇文章中同时频繁出现，他们的向量也就十分接近

## 4.2 Prediction-based
- 给定前一个word`$w_{i-1}$`，通过网络求解预测下一个word是什么  
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pCP2ZNquzKFgv4gWGV.tABXWd7Fk8rymZETxW0og5nmG8jMn8C14e3ZyCM.*G4AlbReEZ3GKLdE2NimyixCc98c!/b&bo=bQXsAwAAAAADB6U!&rf=viewer_4 )

- 在此基础上，给定一系列词（sentence）预测下一个word
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pJliZj8caawIWBrqWHq*cwjqS9NuRBn99.M0IR.1tw9srhAHdqop7SblbfFIiHQZVnbet9RTI0WG2fNF7UzzMXY!/b&bo=bQXqAwAAAAARB7E!&rf=viewer_4)

# 5. Neighbor Embedding 非线性降维
## 5.1 Locally Linear Embedding(LLE)
- 在初始空间求解权重证`$w_{ij}$`
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pNlMpIEqNCwiB*THm47mTdjnY9QrrTewjsJGoRx2EoG5SXl95lBkJqa3GO6sFff9rK1LBls3ccLGNNsKt.XPaaU!/b&bo=GAVIAgAAAAADB3U!&rf=viewer_4)
- 投影到新空间后，保证`$w_{ij}$`不变
- 固定权值`$w_{ij}$`，求解投影后的值`$z^i$`
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pD7AevEfZDfN5Ayc9psfgiY2cgU3xNPPQaR2ISbw4lJRDzihTiR.rHaz0VTgoNhu6i1IOTrheYhLgCOqPLtEFug!/b&bo=QwWOAwAAAAADB.k!&rf=viewer_4)

## 5.2 Laplacian Eigenmaps
- 用graph来重建数据
- 如果`$x^i$`和`$x^j$`在高密度区域很接近，则其投影后的`$z^1$`和`$z^2$`也比较接近。
- 但为了避免投影后都集中到一起，需要对z添加约束：
    - 假设z的维度是M，`$Span\{z^1,z^2,...,z^N\}=R^M$`

## 5.3 T-distributed Stochastic Neighbor Embedding(t-SNE)
- 如果原始数据里的很远，则其投影后的数据也应该离得较远
- 计算所有原始样本的相似度
```math
P(x^j|x^i)=\frac{S(x^i,x^j)}{\sum_{i,k} S(x^i,x^k)}
```
- 投影后的相似度
```math
Q(z^j|z^i)=\frac{S'(z^i,z^j)}{\sum_{i,k} S'(z^i,z^k)}
```
- 定义误差函数为KL散度
```math
L=\sum_{l}KL\bigg(P(*|x^i) || Q(*|z^i))\bigg)\\
=\sum_i\sum_i P(*|x^i)ln\frac{P(*|x^i)}{Q(*|z^i)}
```
- 对上述函数求最小值，求得z
- 缺点：
    - 会计算所有数据点的相似度，数据量大的时候速度较慢
    - 训练好的模型不能用于其他数据
    - 通常用来做可视化

- 相似度函数
```math
S(x^i,x^j)=exp\big(-\|x^i-x^j\|_2\big)\\[0.6em]
S'(z^i,z^j)=1+\|z^i-z^j\|_2
```

# 6.Auto-encoder
- 输入一个对象，输出是一段code，code是该对象的精简表示
- 学习时对encode和decode同时训练
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pFY*ql69ilo3I*kHL4xbrtOWa4L6iaypyHMyNvEirY5zf0QygIKvpBrGdLZjph6T5NqbhrMWMotflJjrEfjEseI!/b&bo=gwVZAgAAAAARB.0!&rf=viewer_4)

## 6.1 PCA基础上的encoder
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pEDt.APFrPGsndpLv3qme9qt*m9OuSOP6AtCc4vYeA65AcaZ2otsEDFisp6ERXLHH8ZeYJll1Xh51IEVtTKeTag!/b&bo=ZQWVAwAAAAADB9Q!&rf=viewer_4)
- PCA 实际是只有一个隐藏层的神经网络，效果不佳
- 受PCA启发，增加auto-encoder的深度
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pLB9HDXxaQde8DrxqsA*X45LGYiS8wC2mWnTvrvzrcazFaXELNrSzIpFaDDcIxPwSTNeDIx6lHg5tRZzanWgqys!/b&bo=0wQ3AgAAAAADB8A!&rf=viewer_4)

## 6.2 应用
- 以图识图
- 图像去噪
- 用decoder产生新的image
- pre-training 寻找网络参数的初始化 在大量数据未做标签的情况下效果比较好
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pC0VZJGrG4HbABgy7qTVfTg1i0ItREeNYCvdp2lw.smJDXyqoLfBCHbtpDc7ZeQaBqMlSHt5kllvLVkC*aabnK0!/b&bo=XgUiAwAAAAADB1g!&rf=viewer_4)
- 应用于CNN中
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pGJAh4BgQHSZbmOh48qfHGcR2xTHbjEP2Hjx1*VJPLVFsIlCDbjd0ugpbjGTnhreYhqDUP34Cgg05VjWZ1F*tDc!/b&bo=kgPFAwAAAAADB3U!&rf=viewer_4)

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pL*F71eIdusXlBBtDnJ9ZLILsidWcS.TLWnKqf2hdmLIy6BlIYDhhPmavuOj8HoovhdzgVDUBwjZupaxv*cgNSM!/b&bo=4wNvAgAAAAARB70!&rf=viewer_4)
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pMtkiaSj*Bp5o*V6lP*DgBad88.vR1lZ1lJkqz9ZtkM5C6KJU04ZsvaCfZRa9H*3hf16mBJ4pUWlf0Ol0Rgz2B8!/b&bo=0wO*AgAAAAADB08!&rf=viewer_4)

## 6.3 Sequence-to-sequence

# 7.Generative Model
使机器自动生成
## 7.1 PixelRNN
- 要创建一幅图片，每次生成一个像素
- 训练时放入一大堆图片，进行无监督学习。训练学习像素间的迭代关系
![image](5A4A32BA1DE9431380BA92B74356B7EC)

## 7.2 Variational Autoencoder(VAE)
![image](70074E72B33B430BA65A82910A7090E0)

- 实际并不是学习如何产生图片
- 只是学习和原图如何尽可能的相似
- 只是记忆已有的图片，而不是创造新网络
## 7.3 Generative Adversarial Network(GAN)
- GAN的迭代过程：
![image](F4C146482EC64118A42BEFABF7C89853)


### Discriminator
- Discriminator是判断器，输入是一张图片，输出是1/0
- 将Generator产生的图片标注为0，将真实图片标注为1
- 将上述数据进行二分类，训练Discriminator

### Generator
- Generator是VAE中的Decoder，输入是从一个分布抽样得到的向量，输出是一系列的图片
- 训练时，调整Generator的参数，将产生的图片输入Discriminator，使其尽可能接近1
- 将Generator和Discriminator组合成一个神经网络进行训练，输入为一个向量，输出为1，固定Discriminator的参数，通过梯度下降寻找generator的最佳参数

![image](58EAD8A7E4FB40C59FC3DCDFA25E2E8C)

### 特点
- GAN很难进行优化
- 无法评判generator的好坏
- 当discriminator效果不好时，无法保证generator产生真实的图片
