# 第六章：黑体和黑体辐射

无聊的一章。请自行谷歌黑体辐射。

## 可公开的信息

韦恩定律（高频）：

$$ I_\nu = \nu^3f(\nu/T) \tag{6.1}$$

瑞利金斯近似（低频/长波）：

$$ I_\nu = \frac{2kT\nu^2}{c^2} = \frac{2kT}{\lambda^2} \tag{6.6}$$

## “推导”

前提：只有两个能级 + 处于热动平衡

第一章的原子激发与电离里面有这样的一个公式：

$$ \frac{N_n}{N_m} = \frac{g_n}{g_m} e^{-\frac{h\nu}{kT}} $$

从第五章最后的两个公式得出细致平衡原理：

$$ N_u A_{ul} + N_u B_{ul} I_\nu = N_l B_{lu} I_\nu $$

$$ I_\nu = \frac{A_{ul}}{B_{lu}(N_l/N_u) - B_{ul}} $$

合在一起就有

$$ I_\nu = \frac{A_{ul}}{(g_l/g_u)B_{lu}e^{-\frac{h\nu}{kT}} - B_{ul}} $$

将$$ e $$指数展开

$$ I_\nu \approx \frac{A_{ul}}{(g_l/g_u)B_{lu} + (g_l/g_u)B_{lu}\frac{h\nu}{kT} - B_{ul}} $$

令它等于瑞利金斯近似，得

$$ B_{ul} = B_{lu}g_l/g_u, A_{ul} = \frac{2h\nu^3}{c^2}B_{ul} \tag{6.8}$$

所以

$$ I_\nu = B_\nu = \frac{2h\nu^3}{c^2} \frac{1}{e^{-\frac{h\nu}{kT}}-1} $$

求导等于0可以得出韦恩位移定律，对频率积分可以得出斯特芬玻尔兹曼定律：

$$ \lambda T = b, F_\nu = \oint I_\nu \cos{\theta} d\omega = \sigma T^4 $$

之前有一个疑惑就是物质的发射或者吸收是怎么从稀薄的谱线到一大块的黑体谱的，[这里](https://physics.stackexchange.com/questions/105875/blackbody-radiation-and-spectral-lines)有一个思路。

再联络。
