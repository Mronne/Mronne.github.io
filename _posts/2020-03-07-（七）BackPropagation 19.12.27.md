---
layout: article
title: （七）反向传播算法
tag: [机器学习课程,反向传播,deep learning]
excerpt: 介绍机器学习中的反向传播求解梯度
---
# 计算梯度
有效计算神经网络中的梯度值

## 1.建模

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pJLm.YxNoN4ZH7nQubQN*AG1FnchucILorrNvqi0BIP*PgKsaSME8DubSx3D4vh1.SgGS*6WeLK0WimUWso5F8M!/b&bo=lgWdAwAAAAADBy8!&rf=viewer_4)

## 2.分类
将其分为前向传递和反向传播
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pKVoNRgmHSsMMZOgcb9F9RzaP*l5vE1T*IfSLOIK0noKhd1eA2GJrx5tN4ZAllWP1OU.75ExiWDnAwJkIzwk1Uc!/b&bo=dwWnAwAAAAADN8Q!&rf=viewer_4)

## 3.前向传递
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pC*o23CuoaUcs7APx1z8v5ehGvlZT3MazvBJ1FdizxI2BEpMVMqVo.WHF6MoY9O4wac6fuQJf8rTpWY1EnILsHo!/b&bo=FwUWAwAAAAADNxU!&rf=viewer_4)

## 4.反向传播
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pHonYV7WEguUbz1md2YPh37Z8kIs3nHKlLBgLwMGJO*6FHuHoqp3.qYgzcOn9*n39ghze1mM*OFFplg682cmddM!/b&bo=dgVtAwAAAAADR38!&rf=viewer_4)

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pNrQlGU8NSzSLWrWzWJdXOVYYdEcw*aGHErbbg0jXn3.9*pfxlaxqnxkZZkkG6QvEOfPEvEosVMmsbH96lZgQ*c!/b&bo=TgXgAgAAAAADN7s!&rf=viewer_4)

- 假如目前处于输出层

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pMV9YptGrK1et1jrqjRkgyvgz5Fh.fGuz3wVW9KeYGRMIZeSDDAn39uGWUE8Vs3rh1ztY6b*8T76wMOyrQ0h2qU!/b&bo=XAUHAwAAAAADN08!&rf=viewer_4)

- 假如是普通层

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pCfO0QC0GGIvMVKtsh9Q6kopwcbdxolsivIqFDLPhyjq6xn9lHEimCBiu1N7tdWzAdjEIIW6My0S6PVeJAQ98hI!/b&bo=kQXgAgAAAAADN2Q!&rf=viewer_4)

- 反向传播过程
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pOfm71jvHO9bZBk..RpBtMs9BA5dKTFGw2vYVrbxHpxj5m7ewufcXpKV1JLWEX.aFNjn64lG6e6gHTZfbbu5Iv0!/b&bo=bQW9AgAAAAADB*U!&rf=viewer_4)

## 5.总结
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pIWUhLLRoqJi*K7ucgDU1hcxqLgKX4gOuMVO04Son9qILl*u3YFJpAp8hCRnIxk1TDtMoWVwzu2vQXB7SLyzf7A!/b&bo=lwVmAwAAAAARB8c!&rf=viewer_4)

# 实例
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pETE1DvLulJP8W64ygzocUvknN.tZhz*dzbDb2uYWyVp3MX*W6ptmxUMG5ZrK0V4FDgiQ1q68bquUm9uLVBM*G0!/b&bo=jQUSBAAAAAADB7w!&rf=viewer_4)
需要调整Batch Size
