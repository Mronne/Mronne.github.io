[toc]
# 1.生成式模型(Generative Model)的半监督学习
## 1.1 算法
初始化参数：`$\theta = \{P(C_1),P(C_2),\mu^1,\mu^2,\Sigma\}$`
- Step 1:对每一笔未加标签的数据计算先验概率
`$P_{\theta}(C_1 |x^u)$`
- Step 2:更新模型
```math
P(C_1)=\frac{N_1+\Sigma_{x^u}P(C_1|x^u)}{N}\\[0.4em]
\mu^1=\frac{1}{N_1}\sum_{x^r\in C_1}x^r+\frac{1}{\Sigma_{x^u}P(C_1|x^u)}\sum_{x^u}P(C_1|x^u)x^u
```
其中
```math
N:数据的总个数\\[0.4em]
N_1:属于类别1的加标签数据个数\\[0.4em]
x^\mu:未加标签的数据个数
```
循环进行，模型逐渐更新。理论上算法最终可以收敛，但结果会受到初值的影响。

## 1.2 算法原理
上述算法实际是最大化有标签和无标签数据的似然函数。
```math
logL(\theta)=\sum_{x^r}log P_{\theta}(x^r,\hat{y}^r)+\sum_{x^u}log P_{\theta}(x^u) \tag{1}
```

```math
P_{\theta}(x^r,\hat{y}^r)=P_{\theta}(x^r|\hat{y}^r)P_{\theta}(\hat{y}^r)\\[0.6em]
P_{\theta}(x^u)=P_{\theta}(x^u|C_1)P(C_1)+P_{\theta}(x^u|C_2)P(C_2)
```
其中（1）式是一个非凸的函数，需要进行迭代求解。1.1节中的算法实际是在迭代求解（1）式，不断迭代使似然函数最大化。

# 2.Low-density Separation 非黑即白
假设类别之间交界处数据密度很小，两个类别的数据可以很清晰的分开。
## 2.1 Self-training
- Given:labeled data set = `$\{(x^r,\hat{y}^r)\}_{r=1}^R$`,unlabeled data set =`$\{x^u\}_{u=l}^{R+U}$`
- 重复以下步骤：
    - 从加标签的数据训练模型`$f^*$`
    - 把`$f^*$`应用到无标签的数据集上求得`$\{(x^u,y^u)\}_{u=l}^{R+U}$`(Pseudo-label)
    - 从无标签数据集中移除部分数据，将其加入到加标签的数据集中
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pEOLysm48Gu9gsgfPhjZ0N1dkNnaN5NvhxztJ5DvyxG..0iTb8eVfJMoAsljwfhiIgfOrG4Qo9ngv5TJ1fgWXio!/b&bo=kgX6AgAAAAADB00!&rf=viewer_4)

## 2.2 Entropy-based Regularization
- `$y^u$`的熵：评价`$y^u$`的分布有多集中
```math
E(y^u) = -\sum_{m=1}^5y_m^u ln(y_m^u)
```
- 目标函数
```math
L=\sum_{x^r}C(y^r,\hat{y}^r)+\lambda\sum_{x^u}E(y^u)
```

## 2.3 Semi-supervised SVM
- 穷举未加标签数据的可能的标签，然后分别使用SVM进行分类
- 比较看哪个分类结果的余量最大且误差最小


# 3.Smoothness Assumption 平滑假设
## 3.1 假设：
- x分布不均匀
- 假设`$x^1$`和`$x^2$`在一个高密度区域很接近(high density path)，则其标签可能比较接近。
- 即未标签样本之间过渡比较平滑

## 3.2 聚类算法 ：聚类，然后对其添加标签

## 3.3 Grpah-based Approach
### 3.3.1 原理
- 判断两个样本之间是否在高密度区域是接近的（connected by a high density path）
- 把数据点用Graph表示
- 已加标签的点会影响他们周围的点
- 标签会随着Graph传播
![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pKHXQc6eovayewk09WVHfudSQmJ7oyzdngXtVK3YTY2qsb072JmcgWnqKDwLlODy63riPvHwpC4*D95bgjXSCSg!/b&bo=eAUhAwAAAAARB28!&rf=viewer_4)
### 3.3.2 构建图 Graph Comstruction
- 定义两个样本`$x^i$`和`$x^j$`之间的相似度函数`$s(x^i,x^j)$`
    - Gaussian Radial Basis Function
```math
s(x^i,x^j)=exp(-\gamma\|x^i-x^j\|^2)
```
- 添加edge 
    - K近邻
    - e-Neighborhood 
- 为每条边分配权重

### 3.3.3 平滑度评价 smoothness
- 定义图上标签点的平滑度(smoothness)
```math
S=\frac{1}{2}\sum_{i,j}w_{i,j}(y^i-y^j)^2
```
- 对每个点进行上述计算，其中`$y^j$`是它相连的所有点,其中smoothness 函数也可表示为
 

![image](http://m.qpic.cn/psc?/V10GdCbE4Hg3EY/Kl*GVNe9OdIAJBN6RDL7pCZ58JpfdtT96noCWod8fOXJMAOkL73uLdGQ.SYoSpCS4msCLX3278TFpOK6WvJX09IfQELWLFlwAoSnlWjfxvc!/b&bo=igXGAgAAAAADB2k!&rf=viewer_4)

- smoothness中的`$\bold{y}$`依赖于网络参数
- 网络的损失函数定义为
```math
L=\sum_{x^r}C(y^r,\hat{y}^r)+\lambda S
```

# 4.Better Representation
- 寻找在现象背后的潜在因素
- 潜在因素即better representation
