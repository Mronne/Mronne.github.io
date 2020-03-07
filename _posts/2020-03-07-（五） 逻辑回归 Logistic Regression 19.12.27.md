---
layout: article
title: （五）逻辑回归 Logistic Regression
tag: [机器学习课程,Logistic Regression,deep learning]
excerpt: 逻辑回归模型
---
# 1.Function Set
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pOTrjHH6P02Pf8bgcHEOSpg0VotadsUf0foNp5ioWRCgDRqCCHEg9Y0*bz2S05LXVdcXJl80C13rW0V.o9al628!/b&bo=zQOCAQAAAAADB28!&rf=viewer_4)

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pGApy05KcFFwYu.P8.ba2EZ1EZrkMHpQhhlR4iS*zyUeYhyLeZRDlCoAfsGc3hMcLyogWWxIduU5xUKDnv1vMrQ!/b&bo=lAXlAgAAAAADB1Q!&rf=viewer_4)

# 2.确定损失函数 Goodness of a Function
- 训练数据

`$x^1$` | `$x^2$` | `$x^3$`|... |`$x^N$`
---|---|---|---|---
`$C_1$`| `$C_2$`|`$C_1$`|...|`$C_1$`
`$\hat{y}^1=1$`| `$\hat{y}^2=1$`|`$\hat{y}^3=0$`|...|`$\hat{y}^N=1$`


- 假定数据是从概率分布`$f_{w,b}(x)=P_{w,b}(C_1|x)$`中产生的
- 给定一系列的`$w$`和`$b$`，产生这些样本的概率为
```math
L(w,b)=f_{w,b}(x^1)f_{w,b}(x^2)\bigg(1-f_{w,b}(x^3)\bigg)...f_{w,b}(x^N)
```
- 最有可能的`$w^*$`和`$b^*$`是使得`$L$`取得最大值所对应的参数值
```math
w^*,b^*=arg\max_{w,b}L(w,b)\\
w^*,b^*=arg\min_{w,b}\big(-lnL(w,b)\big)
```

- 将C表示为对应的`$\hat{y}$`的值，则似然函数的负对数可以化简为

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pAxAwNpRBwcaU9WrdqUcEKjPRXVqShqwlwnnWy1q9oExqZc1N9MlbkyQ5Z8a8sXA8WhHSzoB7uEk8bZ*8v0Fxvo!/b&bo=gQUkAwAAAAADB4E!&rf=viewer_4)

# 3.最佳参数求解 Find the best function
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pDXrHr0.iyfrpePX1uaMyUocRNCBsnaYkufIq6XomOoNJeaV8BZqTmPH.8xuRbRTu9CsoxL5r8e.0qeSnloU8Sw!/b&bo=jgWnAwAAAAADR00!&rf=viewer_4)



![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pKc06tSA6tVsoxxAzUNFJ27.th*BLzB0zavN*V2hpo6O9NRecgyEyoeWJlOwhKJol.bVAxpwsw0N*PtzFxXGBDI!/b&bo=dwVIAwAAAAARFxk!&rf=viewer_4)


![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pCshgCXEUfXsvmLR5uhIfTtI*EEKG9ESPTdYjiBrbu0aMbg4Enz8d6tnqTNbnzx6cnA*SK95d9nzQcKyChvL0pQ!/b&bo=jwU2AwAAAAARF58!&rf=viewer_4)

# 4.与线性回归的对比
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pEi5wucsrvd0loHBbaOWQD9xCVuCyEJTBhQdkwp7wy8UQi7W6falZ6KcUBBNX9sl759yXe2UkCBv4tfFyN8M5*s!/b&bo=mgUJBAAAAAARB6I!&rf=viewer_4)

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pFjvxbRFTOha0Hb5VD13l5UiMJjHXAfWFO6aQvNQAdy3CRfO62PPYTRgHeu*HKa25*W3ebEGclWIGIlnUcn8Gwk!/b&bo=eAWdAwAAAAARB9M!&rf=viewer_4)

- 生成式模型：首先假设类别的概率分布，再对其进行估计
- 判别式模型：不对类别的概率分布进行求解，直接对`$w$`和`$b$`进行估计
- 逻辑回归无法求解边界是多个的情况

# 5.多类别分类
- SoftMax
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pBJIeRW8eHg*T5SIJu0QUB766SZGN*hFi7wTXfU9HA1wurcLElyNs*N*Q73q*HoGbXv4TTfKZ1J.i6f1oz4CThg!/b&bo=bQWbAgAAAAARF9E!&rf=viewer_4)

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pOBvfwbtzWVxgIY1KetunchqucmDBADA*sA3AUG0o7Y2SFB3Y3rWqmd1ei0k9rJ.4ELcO4dHhoM7r94ps52sDPM!/b&bo=hgVTAwAAAAADN8E!&rf=viewer_4)

- 对于一些无法直接确定边界的情况，可先对输入进行变换，分别进行逻辑回归，再输入到逻辑回归中，进行分类 即 神经网络
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pIPqmdWIcJqGIOx1909xenP88ohU8*0eO8kyDcrXa5k*swALBqPvln0AjC.WjYXgVEOoooYdnJeVP.jsOTZncyE!/b&bo=cgUoAwAAAAADB34!&rf=viewer_4)
