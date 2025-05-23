# 第一章

对恒星的光谱观测基本上就是对光球层的观测。我们可以从里面得到很多信息，比如质量、年龄、金属丰度、温度等等。我们关注光球层的原因是可见光光谱中的光子就是从光球层中发出的。

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/32/Sun_Atmosphere_Temperature_and_Density_SkyLab.jpg/800px-Sun_Atmosphere_Temperature_and_Density_SkyLab.jpg)
*恒星各层的位置和温度。来自[维基百科](https://en.wikipedia.org/wiki/Photosphere)*

这一章简要地介绍了一些概念，没有涉及太多的计算。这里默认读者对这些概念已经了解，仅简要列举如下：

### 基本量

- 重力加速度$g$

$$ g = g_\odot \frac{m}{R^2} $$

以太阳为基准计算物理量是天文领域惯用的伎俩了；相对量不用管系数是多少，抓住和物理量有关的量确定幂次（或者更加复杂的形式）就好，$g_\odot$测定就行。

- 有效温度$T_\mathrm{eff}$

$$ \sigma T_\mathrm{eff}^4 = \int_0^\infty f_\nu d\nu $$

有效温度是通过恒星的流量来定义的。这里的$f_\nu$会在第五章定义。

- 光度$L$

$$ L = 4\pi R^2 \sigma T_\mathrm{eff}^4 $$

- 光谱型分类

略。

### 测光相关

- 星等

$$ m = -2.5 \lg \int_0^\infty F_\nu W(\nu) \mathrm{d}\nu + C $$

这里$F_\nu$是投射到望远镜或者CCD上的光量，$W(\nu)$是透过率；常数$C$用标准星标定。如果$W(\nu) = 1$那么星等就变为热星等。

有关各星等系统的透过率信息在[这里](http://svo2.cab.inta-csic.es/svo/theory/fps/)。

- 色指数

$$ m_a = m_b = -2.5 \lg \frac{E_1}{E_2} + C $$

这里的常数$C$是令某光谱型恒星色指数为0的常数。

- 星际消光

星际消光影响星等和色指数，不影响谱线形状，但是会在光谱上产生吸收线。

### 物理公式

- 理想气体

$$ PV = nRT $$

$$ P = \frac{nN_0}{V} \frac{R}{N_0} T = NKT $$

- 速率分布

$$ \frac{\mathrm{d}N(v_R)}{N_\mathrm{total}} = (\frac{m}{2\pi kT})^{3/2} e^{-\frac{mv_R^2}{2KT}} \mathrm{d}v_R $$

麦克斯韦分布。$v_R$为视向速度分量。

$$ \frac{\mathrm{d}N(v)}{N_\mathrm{total}} = (\frac{2}{\pi})^{1/2}(\frac{m}{kT})^{3/2} e^{-\frac{mv^2}{2KT}} \mathrm{d}v $$

麦克斯韦-玻尔兹曼分布。

- 原子激发与电离

对于某两个能级来说，占据数有如下关系：

$$ \frac{N_n}{N_m} = \frac{g_n}{g_m} e^{-\frac{\Delta \chi}{kT}} $$

对于某一个能级和总原子数，有

$$ \frac{N_n}{N} = \frac{g_n}{u(T)} e^{-\frac{\chi_n}{kT}} $$

其中$u(T) = \Sigma g_i e^{-\frac{\chi_n}{kT}}$为配分函数；附录D中有表格可供计算。从这里可以看出基态的占据数和温度无关（*如何理解？*）

Saha方程是用在原子的电离上的，表示某电离态和原子态的数量之比：

$$ \frac{N_n}{N_0} P_e = \frac{(2\pi m_e)^{3/2}(kT)^{5/2}}{h^3} \frac{2u_1(T)}{u_0(T)}e^{-\frac{I}{kT}} $$

结合Saha方程和上上式，即可得出某能级原子占总原子数的比：

$$ \frac{N_n}{N_\mathrm{total}} = \frac{N_n}{N_0+N_1+N_2+...} $$

要讨论某个电离态里面的某个激发态的时候，就用那个电离态的$N_i$去除上式，就可以把那两条式子代入了。
