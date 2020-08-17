# Data analysis recipes: Fitting a model to data

## Abstract

同权重最小二乘拟合只在某一轴的数据点误差可忽略，另一轴数据点误差符合已知方差的高斯分布的情况下可用；方差可以不一样。

这个食谱是为了一般情况准备的。我们会接触到更复杂的二维误差、outliers、未知误差、以及存在但未知的内禀误差。

“Generative Model?”

## Introduction

很多时候我们对数据的线性拟合是错误以及不必要的。一方面线性关系极少存在，并且需要物理基础去证明它；另一方面数据包含的信息比斜率+截距更多。只有当仅在$y$方向上有已知大小的高斯分布误差时，同权重最小二乘拟合才能被使用。

## Standard practice

我们有（矩阵形式）$\boldsymbol{Y} = \boldsymbol{A}\boldsymbol{X}$，以及：

$$ \boldsymbol{Y} = \begin{bmatrix}
y_1 \\
y_2 \\
... \\ 
y_N
\end{bmatrix}$$

$$ \boldsymbol{X} = \begin{bmatrix}
1 & x_1 \\
1 & x_2 \\
... \\ 
1 & x_N
\end{bmatrix}$$

$$ \boldsymbol{C} = \begin{bmatrix}
\sigma_{y_1}^2 & 0 & ... & 0 \\
0 & \sigma_{y_2}^2 & ... & 0 \\
... \\ 
0 & 0 & ... & \sigma_{y_N}^2 \\
\end{bmatrix} $$

最小二乘法求得的拟合结果就是：

$$ \begin{bmatrix}
b \\
m \\
\end{bmatrix} = \boldsymbol{X} = [\boldsymbol{A}^\top \boldsymbol{C}^{-1} \boldsymbol{A}]^{-1} [\boldsymbol{A}^\top \boldsymbol{C}^{-1} \boldsymbol{Y}]$$

在$\boldsymbol{Y} = \boldsymbol{A}\boldsymbol{X}$下，上式就是估计参数的正统办法。
它只在$y$方向有误差，并且误差服从高斯分布（$\sigma$可以不同）的情况下是正确的。 

在这里我们做的其实是最小化我们的目标函数：

$$ \chi^2 = \sum_{i=1}^N \frac{[ y_i-f(x_i)^2 ]}{\sigma_{y_i}^2} = [\boldsymbol{Y} - \boldsymbol{A}\boldsymbol{X}]^\top \boldsymbol{C}^{-1} [\boldsymbol{Y} - \boldsymbol{A}\boldsymbol{X}]$$

顺便一提将目标函数求导并令之为就可以求得上上式。

## 目标函数

目标函数是怎么来的？是我们构造得来的。怎么构造？通过生成模型构造出来的。什么是生成模型？生成模型是指能够随机生成观测数据的模型；也就是说我们需要建立一个模型，这个模型可以模拟观测数据、有概率生成和观测数据一样的数据集。

在上一节我们的模型是这样的；假设：

- 所有的数据点都是从一个没有宽度的线性关系$y = mx + b$得来的；
- 数据点只有$y$方向上的服从高斯分布$N(0, \sigma_{y_i})$的误差，$x$方向上没有误差；
- 不同点之间的误差相互独立。

那么，给定一组$x_i, \sigma_{y_i}, m, b$，这个模型取到$y_i$的概率为：

$$ p(y_i|x_i, \sigma_{y_i}, m, b) = \frac{1}{\sqrt{2 \pi \sigma_{y_i}^2}} \exp{(- \frac{[y_i - mx - b]^2}{2\sigma_{y_i}^2})} $$

对所有的数据点来说，因为不同点之间的误差相互独立，所以似然函数为：

$$ \mathscr{L} = \prod_{i=1}^N p(y_i|x_i, \sigma_{y_i}, m, b)$$

$$ \begin{align}
    \ln{\mathscr{L}} &= K - \sum_{i=1}^N \frac{[y_i - mx - b]^2}{2\sigma_{y_i}^2} \\
    &= K - \frac{1}{2}\chi^2
\end{align}$$

这样推导出来的$\chi^2$是有充分依据并且可以推广到其他形式/限制的。

更一般的形式需要用到贝叶斯公式：

$$ p(m, b|\{y_i\}, I) = \frac{p(\{y_i\}|m, b, I)p(m, b|I)}{p(\{y_i\}|I)} $$

其实就是把不好算的改成好算的就行了。

## Outliers

我们继续用第二节的模型；要是这个时候有outliers，怎么办？以前的做法是手动将它们丢掉，或者用sigma slipping；这两个过程都比较主观并且没有数理基础。“正确”答案是：将outliers也纳入生成模型然后在后面的将它积分掉。

添加一些新的变量：
- $q_i$，为1时表示第$i$个点是数据点，为0时表示第$i$个点是outlier；
- $P_\mathrm{b}$，数据点为outlier的概率；
- $Y_\mathrm{b}, V_\mathrm{b}$，假设outlier们服从均值为$Y_\mathrm{b}$标准差为$V_\mathrm{b}$的高斯分布。

这个时候我们的模型就既能产生好的数据点又能产生outliers了。这个模型的likelihood为：

$$ \mathscr{L} = \prod_{i=1}^N p(y_i|m, b, \{q_i\}_{i=1}^N, Y_\mathrm{b}, V_\mathrm{b}, I)$$

$$ \begin{align}
    \mathscr{L} &= \prod_{i=1}^N [p_{fg}(y_i|m, b, I)]^{q_i} [p_{bg}(y_i|Y_\mathrm{b}, V_\mathrm{b}, I)]^{(1-q_i)} \\
    &\propto \prod_{i=1}^N \left[ \frac{1}{\sqrt{2 \pi \sigma_{y_i}^2}} \exp{(- \frac{[y_i - mx - b]^2}{2\sigma_{y_i}^2})} \right]^{q_i} \\
    &~\times \left[ \frac{1}{\sqrt{2 \pi (V_\mathrm{b}^2 + \sigma_{y_i}^2)}} \exp{(- \frac{[y_i - Y_\mathrm{b}]^2}{2(V_\mathrm{b}^2 + \sigma_{y_i}^2)})} \right]^{(1-q_i)}
\end{align}$$

其实就是根据是否为outlier给按上不同的高斯分布。
然后我们需要留意到的是，先验分布不再是平的了。在给定$P_\mathrm{b}, I$的情况下得到$\{q_i\}$的概率不是均等的，而是一个二项分布的连乘：

$$ p(\{q_i\}|P_\mathrm{b}, I) = \prod_{i=1}^N [1-P_\mathrm{b}]^{q_i} P_\mathrm{b}^{(1-q_i)} $$

那么总的先验分布就是：

$$ p(m, b, \{q_i\}, P_\mathrm{b}, Y_\mathrm{b}, V_\mathrm{b}|I) = p(\{q_i\}|P_\mathrm{b}, I) p(m, b, P_\mathrm{b}, Y_\mathrm{b}, V_\mathrm{b}|I) $$

对于其他的参数，取自己认为合适的先验即可。

这里我们加上了两个额外的假设：
1. 每个数据点为outlier的概率都为$P_\mathrm{b}$；
2. outlier的likelihood是高斯分布。

第1点并不意味着每个数据点为outlier的后验分布都是一样的；$P_\mathrm{b}$主要是给不同的outlier情况做了排序：outlier多的可能性就小。第2点的话，因为我们不知道outlier是什么情况，所以这就是最少信息的假设。

令所有的变量为$\boldsymbol{\theta} = (m, b, \{q_i\}, P_\mathrm{b}, Y_\mathrm{b}, V_\mathrm{b})$，那么后验分布为：

$$ p(\boldsymbol{\theta}|\{y_i\}, I) = \frac{p(\{y_i\}|\boldsymbol{\theta}, I) p(\boldsymbol{\theta}|I)}{p(\{y_i\}, I)} $$

首先分母我们可以不管（就是个归一化项而已）；第二我们关心的量只有斜率和截距，所以我们可以将其他量的概率边缘化掉：

$$ p(m, b|\{y_i\}, I) = \int p(\boldsymbol{\theta}|\{y_i\}, I) d\{q_i\} dP_\mathrm{b} dY_\mathrm{b} dV_\mathrm{b} $$

因为$\{q_i\}$是二项分布，对$d\{q_i\}$的积分就是对$\{q_i\}$所有$2^N$个可能性的求和。虽然这意味着我们要算$2^N$个likelihood，这个可以通过剪枝的办法来处理。

我们能不能避开这$2^N$个求和呢？上面添加的第一个额外假设为我们提供了可能性。我们可以不把$\{q_i\}$当作变量，但是将数据点看作从一个“混合”模型-既产生数据点又产生outlier的模型-中产生的数据。此时：

$$ \mathscr{L} = \prod_{i=1}^N p(y_i|m, b, Y_\mathrm{b}, V_\mathrm{b}, I)$$

$$ \begin{align}
    \mathscr{L} &= \prod_{i=1}^N (1-P_\mathrm{b})p_{fg}(y_i|m, b, I) + P_\mathrm{b}p_{bg}(y_i|Y_\mathrm{b}, V_\mathrm{b}, I) \\
    &\propto \left[ \prod_{i=1}^N \frac{1-P_\mathrm{b}}{\sqrt{2 \pi \sigma_{y_i}^2}} \exp{(- \frac{[y_i - mx - b]^2}{2\sigma_{y_i}^2})} \\
    &~+ \frac{P_\mathrm{b}}{\sqrt{2 \pi (V_\mathrm{b}^2 + \sigma_{y_i}^2)}} \exp{(- \frac{[y_i - Y_\mathrm{b}]^2}{2(V_\mathrm{b}^2 + \sigma_{y_i}^2)})} \right]
\end{align}$$

这个时候的边缘化就只需要对三个连续变量做了，方便了很多。这个的实际实现非常适合用MCMC。

我们必须要指定prior；必须进行边缘化（MCMC可以做）。[这里](https://chi-feng.github.io/mcmc-demo/)有一个很不错的MCMC算法可视化网站。

在我们得到MCMC结果（一组所求量的sample）之后，我们需要考虑我们要给出的是什么结果。当存在无关变量的时候，给出边缘化后的distribution是更好的。当然还有一个问题是贝叶斯方法只给出所求变量的概率，这个好不好就见仁见智了。我们既可以求sample的统计量并只给出数字（回到传统方法），或者直接给出后验分布。

**实际拟合的时候可以直接用emcee**。

### 练习6

## 参数的误差

当我们不相信$y$方向上的误差的时候，我们可以用bootstrap或者jackknife来估计参数的误差。

## 非高斯误差

1. 继续用高斯。这是我们最保守的假设了。
2. 拒绝非高斯误差数据点
3. 搞清楚误差分布是怎么样的；我们可以用一堆高斯分布去逼近别的分布

## 拟合优度

在简单的线性拟合之下，拟合优度可以用$\chi^2$来表征；但是更偏离1的$\chi^2$不一定就意味着这个模型更差；可能仅仅因为误差被高估/低估了。如果误差也不知道，那就把误差也放到变量中去做贝叶斯。

## 双向误差

当$x$方向上也有误差的时候，它们可能会有相关：

$$ \boldsymbol{S}_i = \begin{bmatrix}
\sigma^2_{xi} & \sigma^2_{xyi} \\
\sigma^2_{xyi} & \sigma^2_{yi} \\
\end{bmatrix}$$