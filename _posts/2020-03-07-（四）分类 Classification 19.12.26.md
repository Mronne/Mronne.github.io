---
layout: article
title: （四）分类 Classification
tag: [机器学习课程，deep learning]
excerpt: 机器学习中的分类任务
---
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pIvVF0iz6nfinBUXtEYXAw2gYiNRETN.jNP.tlHsHtRrlLkb5hinX4NlQ573ZxlbcxDlajTYvxW2FktKRFnYFEw!/b&bo=kwWHAwAAAAADBzA!&rf=viewer_4)

高斯分布
```math
f_{\mu,\Sigma}(x)=\frac{1}{2\pi^{D/2}}\frac{1}{|\Sigma|^{1/2}}\exp \bigg\{-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu)\bigg\}
```

- 均值`$\mu$`
- 协方差矩阵`$\Sigma$`
- 假定变量服从高斯分布，对其进行采样，以确定高斯分布。

## 极大似然估计
假定变量的均值和协方差已知
```math
L(\mu,\Sigma)=\Pi f_{\mu,\Sigma}(x^i)\\[0.7em]
\mu^*,\Sigma^*=arg\max_{\mu,\Sigma}L(\mu,\Sigma)


\mu^* = \frac{1}{N}\sum_{n=1}^Nx^n\\
\Sigma^*=\frac{1}{N}\sum_{n=1}^{N}(x^n-\mu*)(x^n-\mu*)^T
```



![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pEYUllOHTbIZOF5L1LZOmytWjliu4eo4b9zhzcTTU9*54QXyg2Z0Qo9aTCRE397CIvj6cedZBCrQ1*QHU0MJFAw!/b&bo=owWoAwAAAAARBz0!&rf=viewer_4)

## 相同协方差
- 不同类别之间共享协方差矩阵`$\Sigma$`
- 可以有效减少模型参数，避免过拟合

假定对样本进行分类
- 类别1：`$x^1,x^2,...,x^m$`是从均值为`$\mu^1$`,协方差矩阵为`$\Sigma$`的高斯分布中采样产生的
- 类别2：`$x^{m+1},x^{m+2},...,x^{m+n}$`是从均值为`$\mu^2$`,协方差矩阵为`$\Sigma$`的高斯分布中采样产生的
- 似然函数
```math
L(\mu^1,\mu^2,\Sigma)=\Pi_{i=1}^mf_{\mu^1,\Sigma}(x^i)\cdot \Pi_{j=m+1}^{m+n}f_{\mu^2,\Sigma}(x^j)
```
- 求解
```math
\mu^{1*} = \frac{1}{m}\sum_{i=1}^mx^i\quad
\mu^{2*} = \frac{1}{n}\sum_{j=m+1}^{m+n}x^j\\[0.5em]
\Sigma^*=\frac{m}{m+n}\Sigma^{1*}+\frac{n}{m+n}\Sigma^{2*}
```

## 小结
- 如果不同类的协方差矩阵不同，分出来的边界是非线性的
- 如果采用相同的协方差，会得到线性边界
- 类别的概率模型需要自己选择
    - 对于二维特征，可假设为伯努利分布
    - 假设所有的维度是独立的，分类器称为Naive Bayes Classifier

## 后验概率
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pHYV0d6tURTT9P30xC.rh.FPhxT0.7QeIs4A3JVXXCd1V4iHpTV40zVivx*bkST1hNUP*bYHtjt89TPf.xWVDmY!/b&bo=eQWPAwAAAAARB8A!&rf=viewer_4)

```math
P(C_1|x)=\sigma(\bold{w}\cdot x+b)
```
在普通模型中，先估计出`$N_1,N_2,\mu^1,\mu^2,\Sigma$`，再求解`$\bold{w}和b$`
