# Chapter 11 辐射转移方程

辐射在介质中的流动是由辐射转移方程决定的。
如果物质是静态的，或者说没有移动的话，光子将以固定的频率在直线上向前运动。
如果物质在时间或者空间上有不均匀的的运动，那么我们必须区分两个坐标系：实验室坐标系（与观测者固定且物质在运动的坐标系）和共动坐标系（与物质共动的坐标系）。
当物质在运动的时候，辐射转移方程的微分算子在实验室坐标系中的形式是简单的，但是物质的吸收和发射为非各向同性，因为光子经历了在不同位置不一样的多普勒频移、abrreation、advection。
在共动坐标系下，情况是反过来的。
在这一章中我们只讨论在静态物质中的辐射转移。

$\S$11.1定义物质吸收、发射和散射系数的宏观描述。
我们会在$\S$11.2中推导一般坐标$\mathbf{q}$下、直角坐标$\mathbf{q}=(x,y,z)$、球面坐标$\mathbf{q}=(r, \theta, \phi)$和柱坐标$\mathbf{q}=(r,z,\phi)$下中的辐射转移方程。
我们用$\Theta$和$\Phi$定义在直角坐标下光子传播的方向$\mathbf{n}$，用$\nu$表示光子的频率。
和之前的章节一样，对于任意的函数$f(\mathbf{q}, t; \mathbf{n}, \nu)$，我们将$\mathbf{q}, t$省略掉，写成$f_{\mathbf{n}\nu}$.

辐射转移方程的解为我们给出恒星大气里面任意一点上任意方向的辐射强度。
我们会在$\S$11.3中对辐射转移方程在立体角和频率上积分，给出与辐射能量密度、辐射通量、辐射应力张量(radiation stress tensor)有关的矩方程。
$\S$11.4定义光深和源函数、给出边界条件，并在一些简单的情况下解辐射转移方程。

$\S$11.5讨论用于计算辐射强度角矩的史瓦西和米恩积分公式。
我们会在$\S$11.6中推导舒斯特的二阶辐射转移方程，它为解方程提供了有效以及稳定的方法。
$\S$11.7则将舒斯特的二阶辐射转移方程离散化，为得出方程的数值解给出基础。
$\S$11.8讨论辐射转移方程的概率描述，并在$\S$11.9中给出它的渐近扩散极限。

## $\S$11.1 吸收、发射和散射和系数

在介质中传播的光子会不断地发生吸收、发射和散射。
它们通过热吸收过程从辐射场中被移除，或者说被破坏。
同时它们又通过热辐射过程生成并添加到辐射场中。
它们也可以从某条光束上通过向外散射(outscattering)被移除，或者通过向内散射(inscattering)添加到某条光束上。
这些过程都可以用一些宏观系数去描述。

在静止介质中，热吸收系数$\kappa_\nu$和热发射系数$\eta_\nu$是各向同性的。
但是即使是最简单、散射系数$\sigma_\mathrm{T}$和频率无关的散射-纯汤姆逊散射中，散射系数也不是各向同性的。
瑞利、拉曼和康普顿散射的系数更是和频率以及方向有关；所以一般我们需要用两个量，$\sigma_{\mathbf{n}\nu}$，来描述散射系数。
我们定义介质的消光系数为吸收系数和散射系数之和，$\chi_{\mathbf{n}\nu} = \kappa_\nu + \sigma_{\mathbf{n}\nu}$.

史瓦西在他的[文章(page 35)](https://books.google.co.jp/books/about/Selected_Papers_on_the_Transfer_of_Radia.html?id=Ga88AAAAIAAJ&redir_esc=y)中指出，在大尺度下光子被吸收、发射和散射时与介质的作用是不一样的。
光子的统计集合携带着它们产生时所在的介质中的状况信息（如普朗克函数的频率分布）。
一个光子大约在穿过了一个平均自由程$\lambda \approx 1/\chi$后被吸收或者是散射。
当光子与介质发生吸收或者散射是，我们可以定义一个散射-破坏概率(single-scattering destruction probability)$\epsilon = \kappa / \chi$（或者叫做热耦合常数）来表征光子是被吸收了还是被散射了。
这个概率也意味着光子能量被转化成热能的概率。
如果没有散射，亦即$\epsilon = 1$，一个在某处发射的光子与之前在那个地方被吸收的光子是没有直接联系的；这个光子只反映那个地方的物理性质，如温度、密度、能级占据数等。

当出现散射的时候，在某处的辐射场性质就与其他地方的介质性质有关了。
光子不被吸收的概率为散射反照率(sigle-scattering albedo)$1 - \epsilon$.
当$\epsilon \ll 1$时，光子可以通过不断的散射传播远大于一个自由程的长度。
所以当光子有很大的散射反照率的时候，它可以将产生此光子处的物理性质传播到大气中很远的地方。
在这个情况下，某处的辐射场可能跟此处的物理性质关系不大了。

### 热吸收和热辐射系数

#### 束缚-束缚跃迁 (Bound-Bound Transitions)

$(5.9)$式说明了改正受激发射后、从低能级$l$到高能级$u$的束缚-束缚跃迁吸收系数为：

$$ \kappa_\mathrm{bb}(\mathbf{n},\nu) = n_l B_{lu} \left(\frac{h\nu}{4\pi} \right) \left[\phi_{lu}(\nu) - (\frac{g_l n_u}{g_u n_l}) \psi_{ul}(\mathbf{n},\nu)\right] \tag{11.1}$$

$B_{lu}$是爱因斯坦B系数。
对LTE的偏离通过改变$n_u$或者$n_l$改变$\kappa_\mathrm{bb}$。
在静态介质中，吸收轮廓$\phi_{lu}$是各向同性的，但是一般来说受激发射轮廓由$\S$10中提到的依赖角度和频率的再分配函数(redistuibution funciton)给出，在静态介质中也可能是非各向同性的。

在完全再分配(complete redistribution)极限下，处于激发态的电子在发射光子前随机地再分配在高能级$u$的子态中；此时$\psi_{lu}=\phi_{lu}$，$(11.1)$式简化为：

$$ \kappa_\mathrm{bb}(\nu) = n_l B_{lu} \left(\frac{h\nu}{4\pi} \right) \left[1 - \left(\frac{g_l n_u}{g_u n_l}\right) \right] \phi_{lu}(\nu). \tag{11.2} $$

加上LTE假设：

$$ \left(\frac{g_l n_u}{g_u n_l}\right) = e^{-\frac{h\nu_{lu}}{kT}}, \tag{11.3}$$

$(11.2)$变为：

$$ \kappa^*_\mathrm{bb}(\nu) = n_l^* B_{lu} \left(\frac{h\nu}{4\pi} \right) \left[1 - e^{-\frac{h\nu_{lu}}{kT}} \right] \phi_{lu}(\nu). \tag{11.4} $$ 

由$(5.10)$可知自发束缚-束缚发射系数为：

$$ \eta_\mathrm{bb}(\mathbf{n},\nu) = n_u A_{ul} \left(\frac{h\nu}{4\pi} \right) \psi_{ul}(\mathbf{n},\nu). \tag{11.5}$$

#### 束缚-自由跃迁系数

由$(5.25)$，改正了受激发射的束缚-自由吸收系数为：

$$ \kappa_\mathrm{bf} = (n_l - n_l^* e^{-\frac{h\nu_{lu}}{kT}}) \alpha_\mathrm{bf}(\nu) \tag{11.6}$$

对LTE的偏离只通过改变$n_l$来影响$\kappa_\mathrm{bf}$。
在LTE下，有：

$$ \kappa_\mathrm{bf}^* = n_l^* (1 - e^{-\frac{h\nu_{lu}}{kT}}) \alpha_\mathrm{bf}(\nu) \tag{11.7}$$

由$(5.25)$，自发辐合（发射）的束缚-自由发射系数为：

$$ \eta_\mathrm{fb}(\nu) = n_l^* \alpha_\mathrm{bf}(\nu) (1 - e^{-\frac{h\nu_{lu}}{kT}}) B_\nu(T), \tag{11.8}$$

它与$n_l^*$成正比[^lte_popu]，并且在流体坐标系(fluid frame)中是各向同性的。

[^lte_popu]: 这里的占据数不是“绝对”的LTE占据数；NLTE占据数$n_\mathrm{f}$实际上包括在了$n_l^*$里面，所以虽然书上的$\eta_\mathrm{fb}(\nu)$打了星号，我觉得它在NLTE下也能用；详见p120中$(5.24)$到$(5.25)$之间的讨论。

#### 自由-自由跃迁系数

自由-自由跃迁是碰撞过程，所以所有的吸收和发射都是在LTE下的。
由$(5.149)$可得：

$$ \kappa_\mathrm{ff}^*(\nu, T) = n_\mathrm{ion} n_e \alpha_\mathrm{ff}(\nu, T) \left( 1-e^{-\frac{h\nu_{lu}}{kT}} \right), \tag{11.9}$$

其中$n_\mathrm{ion}$和$n_e$是离子和电子的数密度。
自由-自由跃迁的自发发射系数为：

$$ \begin{align}
\eta_\mathrm{ff}^*(\nu, T) &= n_\mathrm{ion} n_e \alpha_\mathrm{ff}(\nu, T) (2h\nu^3/c^2) e^{-\frac{h\nu_{lu}}{kT}}\\
&= n_\mathrm{ion} n_e \alpha_\mathrm{ff}(\nu, T) \left( 1-e^{-\frac{h\nu_{lu}}{kT}} \right) B_\nu(T). \tag{11.10}
\end{align}$$

束缚-自由和自由-自由跃迁的这四个系数遵循基尔霍夫-普朗克定律[^ft2]。

[^ft2]: 应该是p99的基尔霍夫定律。

#### 总热吸收和热辐射系数

总吸收系数是所有能级、离子、元素的占据数乘上非0的束缚-束缚、束缚-自由和自由-自由跃迁在频率$\nu$下的系数。
我们假设这些过程是独立的，所以可以线性相加。
对于束缚-束缚跃迁来说低能级为$l$，高能级为$u$.

$$ \begin{align}
\kappa_\mathrm{thermal}(\mathbf{n}, \nu) &= \sum_k \sum_j \left\{ \sum_{u>l} \sum_l \left[ n_{ljk} \phi_{lu,jk}(\mathbf{n}, \nu) - (g_l/g_u)n_{ujk} \psi_{ul,jk} (\mathbf{n}, \nu) \right] (B_{lu,jk} h\nu/4\pi)\\ 
+ \sum_i \left(n_{ijk} - n_{ijk}^* e^{-\frac{h\nu_{lu}}{kT}}\right) \alpha_{ijk}^\mathrm{bf}(\nu) + n_e n_{jk} \left( 1-e^{-\frac{h\nu_{lu}}{kT}} \right) \alpha_{jk}^\mathrm{ff}(\nu, T) \right\}. \tag{11.11}
\end{align} $$

总热发射系数为：

$$ \begin{align}
\eta_\mathrm{thermal}(\mathbf{n}, \nu) &= \sum_k \sum_j \left\{ \sum_{u>l} \sum_l n_{ujk} \psi_{ul,jk}(\mathbf{n}, \nu) (A_{ul,jk} h\nu/4\pi) \\
+ (2h\nu^3/c^2) e^{-\frac{h\nu_{lu}}{kT}} \left[ \sum_i n_{ijk} \alpha_{ijk}^\mathrm{bf}(\nu) + n_e n_{jk} \alpha_{jk}^\mathrm{ff}(\nu, T) \right]\right\}. \tag{11.12}
\end{align} $$

$\kappa_\mathrm{thermal}(\nu)$的单位是$\mathrm{cm^{-1}}$，$\eta_\mathrm{thermal}(\nu)$的单位是$\mathrm{ergs/cm^{3}/sec/Hz/sr}$.

### 连续谱散射

第6章主要关注的是单个光子的散射。
现在考虑一下一道光束中的散射。
在高温恒星($T_\mathrm{eff} > 3 \times 10^4$)中，介质是高度电离的。对于低能量($h\nu \ll m_ec^2$)的光子来说，主导的散射机制是汤姆孙散射，散射截面$\sigma_\mathfm{T}$与频率无关。
此时我们可以忽略速度分布函数中的相对论性效应。

用和$(6.59)$类似的记号，从$(\mathbf{n}, \nu)$被电子散射到别的方向$(\mathbf{n}', \nu')$的能量为：

$$ E_\mathrm{out}(\mathbf{n}, \nu) = n_e \int_0^\infty d\nu' \oint_{4\pi} \frac{d\Omega'}{4\pi} \sigma(\nu\rightarrow\nu';\mathbf{n}\rightarrow\mathbf{n}') I(\mathbf{n}, \nu) \left[ 1 + \left( \frac{c^2}{1h\nu'^3} \right) I(\mathbf{n}', \nu') \right] \tag{11.13}$$

类似的，从$(\mathbf{n}', \nu')$被电子散射到$(\mathbf{n}, \nu)$的能量为：

$$ E_\mathrm{in}(\mathbf{n}, \nu) = n_e \int_0^\infty d\nu' \oint_{4\pi} \frac{d\Omega'}{4\pi} \frac{\nu}{\nu'} \sigma(\nu'\rightarrow\nu;\mathbf{n}'\rightarrow\mathbf{n}) I(\mathbf{n}', \nu') \left[ 1 + \left( \frac{c^2}{1h\nu'^3} \right) I(\mathbf{n}, \nu) \right] \tag{11.14}$$

$(11.14)$中的$\frac{\nu}{\nu'}$将其他方向的光转成光子数（因为散射中光子数守恒），然后再转成$\nu$上的能量。

这些式子有一些有趣的性质：
- 