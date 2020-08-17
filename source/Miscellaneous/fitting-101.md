# Fitting 101

## Statistical inference section 11

ANOVA: 对随机变量进行统计分析的过程（不仅是方差）？

### Oneway Analysis of Variance

$Y_{ij} = \theta_i + \epsilon_{ij}, i = 1, ..., k, j = 1, ..., n_i$

$Y_{ij} = \mu + \tau_i + \epsilon_{ij}, i = 1, ..., k, j = 1, ..., n_i$

假设$\epsilon_{ij} = 0$。如果不为0，可以将不为0的部分放到前面去。

当$i$不一样的时候一般来说$\theta_i$也不一样；比如说$i$为药物浓度，$\theta_i$为药物的效果。
但是我们不能同时估计$\mu$和$\tau_i$，因为这里有一个可辨识性的问题。

**定义11.2.2**：若一个分布$\{f(x|\theta):\theta \in \Theta\}$的系数$\theta$不同时，$f(x|\theta)$也不同，则这个模型是可辨识的。

> 一个模型是可辨识的，如果它在理论上能通过无限的观测结果学习到的真正该模型背后参数的真实值。 在数学上，这相当于说基于这些观测结果的不同的参数值必须产生不同的概率分布。([维基百科](https://zh.wikipedia.org/wiki/%E5%8F%AF%E8%BE%A8%E8%AF%86%E6%80%A7))

一般来说可辨识性的问题可以通过改造模型来解决。比如$\mu$和$\tau_i$的问题，添加一个条件$\sum_{i=1}^k \tau_i = 0$即可让模型变得可辨识。

#### Oneway ANOVA假设(assumption)

$Y_{ij} = \theta_i + \epsilon_{ij}, i = 1, ..., k, j = 1, ..., n_i$

1. $\mathrm{E}[\epsilon_{ij}] = 0, \mathrm{Var}[\epsilon_{ij}] = \sigma_i^2 < \infty$，$\mathrm{Cov}[{\epsilon_{ij}, \epsilon_{i'j'}}] = 0$ for all $i, j, i', j'$ unless $i=i'$ and $j=j'$.
2. $\epsilon_{ij}$互相独立并服从正态分布
3. 对于所有$i$有$\sigma_i^2 = \sigma^2$ (homoscedasticity).

#### 经典ANOVA假说(hypothesis)

[经济学范畴里，假设与假说的区别是什么？](https://www.zhihu.com/question/23977515)

我们想去检验零假说（一个“特别蠢”的，希望被证伪的假说）：

$H_0: \theta_0 = \theta_1 = ... = \theta_k$

相对的，备择假说($H_1$)为：

$\exists i, j$使得$\theta_i \ne \theta_j$.

实际上用的时候，$H_0$的连等号会比较难表达，所以我们需要将它转换成一些比较容易表达的假说.

定义$\sum_{i=1}^k a_i t_i$为$t_i$的线性组合；如果加上$\sum a_i=0$则叫做对比(contrast). 那么：

$\theta_1 = \theta_2 = ... = \theta_k \Leftrightarrow \sum_{i=1}^k a_i \theta_i = 0, \forall \boldsymbol{a} \in A$

$A$为$\boldsymbol{a}$的对比. 
从左往右是显然的，而从右往左可以将$A$用$\boldsymbol{a}_1 = (1, -1, 0, ...), {a}_2 = (0, 1, -1, ...), {a}_{k-1} = (0, 0, 0, ..., 1, -1)$表示.
将这些基代入上式则有$\theta_1 = \theta_2, ..., \theta_{k-1} = \theta_k$.
这样我们就将连等号拆成了很多个等号了.

#### 平均值线性组合的统计推断

补充：期望与方差的性质

1. $\mathrm{Var}(x) = \mathrm{E}(x^2) - \mathrm{E}^2(x)$
2. $\mathrm{Var}(bx+a) = b^2\mathrm{Var}(x)$
3. $\mathrm{Var}(\sum_i x_i) = \sum_i \mathrm{Var}(x_i) + \sum_{i=1}^n \sum_{j\ne i}^n [\mathrm{E}(x_i x_j) - \mathrm{E}(x_i) \mathrm{E}(x_j)]$
4. $\{x_i\}$独立时协方差为0，$\mathrm{Var}(\sum_i x_i) = \sum_i \mathrm{Var}(x_i)$（因为积分不耦合）

在oneway ANOVA假设下，我们有：

$Y_{ij} \sim N(\theta_i, \sigma^2), ~~ i = 1, ..., k,~~ j = 1, ..., n_i$.

均值

$\bar{Y}_{i\cdot} = \frac{1}{n}\sum_{j=1}^{n_i} Y_{ij} \sim N(\theta_i, \sigma^2/n_i)$

线性组合$\sum_{i=1}^k a_i \bar{Y}_{i\cdot}$

$\mathrm{E}\left(\sum_{i=1}^k a_i \bar{Y}_{i\cdot} \right) = \sum_{i=1}^k a_i \theta_i$

$\mathrm{Var}\left(\sum_{i=1}^k a_i \bar{Y}_{i\cdot} \right) = \sigma^2 \sum_{i=1}^k \frac{a_i^2}{n_i}$

$\frac{\sum_{i=1}^k a_i \bar{Y}_{i\cdot} - \sum_{i=1}^k a_i \theta_i}{\sqrt{\sigma^2 \sum_{i=1}^k \frac{a_i^2}{n_i}}} \sim N(0,1)$

这里的$\bar{Y}_{i\cdot}$是样本期望。实际上我们连$\sigma^2$（分布的方差）都不知道，只能用样本方差去估计：

$S_i^2 = \frac{1}{n_i-1} \sum_{j=1}^{n_i} (Y_{ij} - \bar{Y}_{i\cdot})^2$.

推导在[这里](https://zh.wikipedia.org/wiki/%E6%A0%B7%E6%9C%AC%E6%96%B9%E5%B7%AE).
此时$S_i^2$是$\sigma^2$的无偏估计.

根据卡方分布（基于**标准**正态分布）的定义有

$(n_i-1) S_i^2/\sigma^2 \sim \chi^2_{n_i-1}$

（推导在[这里](https://www.zhihu.com/question/37400689)有但是得用到特殊函数）.

补充：[**合并方差**](https://zh.wikipedia.org/wiki/%E5%90%88%E5%B9%B6%E6%96%B9%E5%B7%AE) (pooled variation)

当多个总体均值不同，但每个总体都有着相同的方差时，如何估算总体方差？

$S_p^2 = \frac{\sum_{i=1}^k (n_i-1)s_i^2}{\sum_{i=1}^k (n_i-1)} = \frac{(n_1-1)s_1^2 + (n_2-1)s_2^2 + ... + (n_k-1)s_k^2}{n_1 + n_2 + ... + n_k}$

其实就是把所有的方差加起来再除以总的自由度。

$S_p^2 = \frac{1}{\sum(n_i-1)}\sum_{i=1}^k (n_i-1) S_i^2$

因为$S_i^2$是独立的、又服从卡方分布，由卡方分布的性质可知

$\sum(n_i-1) S_p^2 / \sigma^2 \sim \chi^2_{\sum(n_i-1)}$

补充：**$t$分布**（陈书p54）

设$X \sim N(0,1), Y \sim \chi^2_n$，且$X, Y$相互独立；令$T=\frac{X}{\sqrt{Y/n}}$，则$T$服从自由度为$n$的$t$分布。$t$-value实际上就是信噪比，信号的差值除以噪音的大小。

应用$t$分布的定义得

$\frac{\sum_{i=1}^k a_i \bar{Y}_{i\cdot} - \sum_{i=1}^k a_i\theta_i}{\sqrt{S_p^2 \sum_{i=1}^k a_i^2/n_i}} \sim t_{N-k}$

在水平$\alpha$下当

$|\frac{\sum_{i=1}^k a_i \bar{Y}_{i\cdot}}{\sqrt{S_p^2 \sum_{i=1}^k a_i^2/n_i}}| > t_{\sum(n_i-1), \alpha/2}$

时，$H_0$假设将被拒绝.

同时我们也可以写出它的置信区间估计：

$\sum_{i=1}^k a_i \bar{Y}_{i\cdot} - t_{\sum(n_i-1), \alpha/2} \sqrt{S_p^2 \sum_{i=1}^k \frac{a_i^2}{n_i}} \le \sum_{i=1}^k a_i \theta_i \le \sum_{i=1}^k a_i \bar{Y}_{i\cdot} + t_{\sum(n_i-1), \alpha/2}$


## 问题

1. (p545中间)在推导$\beta$的BLUE的时候，为什么要求$\mathrm{E} \sum_{i=1}^n d_i Y_i = \beta$？
2. (p547中间)有式子$b = \sum_{i=1}^n \frac{(x_i-\bar{x})}{S_{xx}}y_i = \frac{S_{xy}}{S_{xx}}$；但是$S_{xy} = \sum_{i=1}^n (x_i-\bar{x}) (y_i-\bar{y})$，这个式子和$S_{xy}$的定义矛盾吗？
3. (p550中间)由$(11.3.25)$有$\beta = \rho \frac{\sigma_Y}{\sigma_X}$；那如果$\rho = 0$那么斜率就是0了？
4. 在p551中间有$\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n (y_i - \hat{\alpha} - \hat{\beta}x_i)^2$，但是p552上部有$\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n \hat{\epsilon_i}^2= \frac{1}{n}\sum_{i=1}^n (Y_i - \hat{\alpha} - \hat{\beta}x_i)^2$；$Y_i$和$y_i$可以互换吗？
5. 我可能还没理解里面的区别；p577下部12.2开头说EIV和11.3的regression非常不一样；但是p550中间也有类似的内容，这两部分的内容也是非常不一样的吗？
6. (p584中间)书上说如果我们可以控制所有的参数的话,我们可以让likelihood保持在infinity;那我实际上可以写出likelihood之后用各种方法去sample它,就可以求得它的最大值对应的参数位置了?这算是一个万用方法么(我之前就是想这样做的)?