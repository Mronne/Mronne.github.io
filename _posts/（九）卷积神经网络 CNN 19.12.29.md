[toc]
# 1.概述
普通的神经网络如果用来处理图像的话需要大量的神经元
- 有些特征要比整张图像要小，神经元无需对整张图像进行运算即可发现特征
- 相同的特征会在不同的区域出现
- 可以通过subsample使图片变得更小，并不改变物体

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pG3Bzi34z8ZDH6*0UoG2RH1dwDYlmdodgh4tDjB9TvFc9n4DtEegcgXLllA*38eWjOctAgwqLkwt8ZJSibF5Ask!/b&bo=ZAX5AwAAAAADB7k!&rf=viewer_4)

# 2.组成
## 2.1 Convolution 卷积
### 2.1.1 灰度图
- 卷积结果如图所示：
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pG4mJZb6oaAIxYL1QMs6b6m1z7TSNnGCMKDe.EO5lm6sdJ1cHaCYAYmhNI7Mueyq7HsQfIbfuBVY1dnWIWaXMQA!/b&bo=NQWeAwAAAAADB48!&rf=viewer_4)


- stride 为Filter移动的步长
- 每次卷积后的结果被称为feature map

### 2.1.2 彩色图
- filter变成一个立方体的核，与彩色图的通道数一致，然后进行空间的卷积

### 2.1.3 卷积与全连接的关系
- 卷积其实是全连接层去掉一些权值后的结果 
- 即部分连接，不是全连接
- 权值共享，对于使用同一个核的部分权重是一样的

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pCjGDpRRhxfVO*QI.NQ9736e3XG9WdUqJZ7XRIoqPKek7d2wx3GIoUB1TtYMYr8WMyRGGuSmoONP729BktNtF8U!/b&bo=hQUsBAAAAAADB4o!&rf=viewer_4)

## 2.2 Max Pooling 池化
- 把卷积后的结果选择平均值或者最大值保留下来，实现subsample
- 具体把feature map分成几部分，可以自己选择参数
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pKg8WeH0plnYvuSC6d8zx6AvHERAorTXRNtTwcBCPHs7ryczTN7jMDeAjAv56wAIEzvkMICfOAO9EDjbNEf9Rhs!/b&bo=QwUnAwAAAAADRwA!&rf=viewer_4)

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pBPF0KQdJgES6Rddo2rsA2rzhpANCe0WtotOLE.4G27nI54YTT9ub3OpVu5iq4SjbiW9sqAzMXJ5ZGFQJJFiwQc!/b&bo=UAViAgAAAAADNyc!&rf=viewer_4)

## 2.3 Flatten
- 把feature map变成一个向量

## 2.4 全连接

# 3. CNN的作用
- 由filter的输出来反推输入图像 

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pF4MuRhRfFh.V1nmENt2d6lGWKAZ4l66ausjXkCtwghEpP61YwLJNd5XZLUgZdzbVgIu21qgzJ6g7ud7NzKblR0!/b&bo=VgWsAwAAAAARB8w!&rf=viewer_4)

- 由全连接层的输出来反推输入图像
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pI3XzAevdCBXDgyEaZvX6QOYmF2tXSfH2wBVea.rErG05cT7xhfIsUv5K0Ngou20c1GUqiPsVIJvXvdTB8ey3wU!/b&bo=LgXiAwAAAAADB.g!&rf=viewer_4)

- 由CNN输出来反推输入图像
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pFtm7xkC2LO0MncPqXahGCJjTibuAAdoXJQk6edx5WxVLqRDvnF7VmN9iHMylJ2fBLM54eIyHvS7xpUCNl7yiK0!/b&bo=cQXXAwAAAAADB4I!&rf=viewer_4)

