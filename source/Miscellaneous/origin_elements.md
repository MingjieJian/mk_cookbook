# Origin of elements

[Kobayashi et al. (2020)](https://ui.adsabs.harvard.edu/abs/2020arXiv200804660K/abstract)

从第一性原理（模型）出发预测在不同环境不同时间下的元素形成情况。

## Introduction

[Burbidge et al. (1957)](https://ui.adsabs.harvard.edu/abs/1957RvMP...29..547B/abstract)这篇是开山之作，有100页，但是得看。
我们现在知道不同的元素来源于不同的天体（不同质量的恒星、超新星、双星等）。
不同的元素在恒星内部形成，随着恒星的死亡抛向星际介质中，下一代恒星就带着这些新形成的元素形成。

观测方面，我们有越来越多的数据，包括中分辨率的大量恒星光谱以及高分辨率的太阳光谱等。

[3氦过程](https://zh.wikipedia.org/wiki/3%E6%B0%A6%E9%81%8E%E7%A8%8B)是3个氦原子核（α粒子）转换成碳原子核的过程。
> 由于3氦过程需要较长的时间才能形成碳，因此在原初核合成不太可能发生。此一结果可以说明大爆炸为何没有制造出碳，因为在大爆炸之后的一分钟，就已经低于核聚变所需要的温度了。
所以质量数$A>12$的元素必定形成在恒星内部。
大约有一半的轻元素(C, N, F等)是在小质量的AGB星中造出来的([Kobayshi et al. 2011b](http://adsabs.harvard.edu/abs/2011MNRAS.414.3231K)，要看)。
$\mathrm{^{13}C, ^{17}O, ^{25,26}Mg}$等也会被AGB星造出来，所以也可以用在银河考古学上；依赖于金属丰度。
alpha元素(O, Mg, Si, S和Ca)则主要是在大质量恒星内部造出来的，然后被core-collapse超新星抛射到星际介质中([Kobayashi et al. 2006](https://ui.adsabs.harvard.edu/abs/2006ApJ...653.1145K/abstract)，要看)。
F, K , Sc和V可以被core-collapse超新星中的中微子过程增丰([Kobayshi et al. 2011a](https://ui.adsabs.harvard.edu/#abs/2011ApJ...739L..57K/abstract))。
与此不同的是，一般的iron-peak元素(Cr, Mn, Fe, Ni, Co, Cu, 和Zn)是在Ia型超新星中被造出来的([Kobayshi, Leung & Nomoto 2020](https://ui.adsabs.harvard.edu/#abs/2020ApJ...895..138K/abstract))。
odd-Z元素的制造和前身星的金属丰度有关，因为它们的制造依赖于$\mathrm{^{22}Ne}$的剩余中微子，而$\mathrm{^{22}Ne}$是由在He-burning中被造出来的$\mathrm{^{14}N}$造出来的。

<span style="color:red">分开氢元素/alpha元素/odd-Z元素等。</span>

Galactic chemical evolution (GCE) 模型可以用来检验这些理论并算出具体的参数(yield等; [Kobayashi, Tsujimoto & Nomoto 2000](https://ui.adsabs.harvard.edu/#abs/2000ApJ...539...26K/abstract))。
比如银河系的[α/Fe]–[Fe/H]关系可以被Ia型超新星的delay time解释，可以用于限制河外星系的恒星形成时标。
从C到Zn（除了Ti之外）的元素可以被GCE很好的模拟出来。

比Fe重的元素主要是在s和r过程中被制造出来的。
强s过程（Sr到Pb）主要在低质量AGB星的He-rich intershell中发生；弱s过程（Fe到Sr）主要在太阳丰度的大质量恒星以及高速自转的贫金属星中发生。

r过程的发生场所还在争论中。双中子星并合可能可以，但是和观测不吻合；magneto-rotational supernovae可能也行。

在这篇文章中，我们用模型模拟从C(A=12)到U(A=238)的元素演化。
讨论的元素丰度误差为0.1dex。

## The MODEL

### 元素增丰来源

### AGB星和core-collapse超新星

这里的结构是先将原理，然后确定物理过程的数据是多少。

- 星风。
年老恒星都会通过星风将壳层的一些质量抛到星际介质中。
星风的质量为$M_\mathrm{wind} = M_\mathrm{init} - M_\mathrm{remnant} - \sigma_i p_{z_i m}$，$\sigma_i p_{z_i m}$在后面的yield表里有（<span style="color:red">为什么是减去？yield只是算超新星爆发的时候的抛出物吗？</span>）。

- AGB星。
原始质量为$0.9$到$8M_\odot$的恒星会经过AGB阶段。
The third dredge-up (TDU) 会将恒星内部已经合成好的元素带到恒星表面来，将$^{12}\mathrm{C}$和s过程的元素丰度提高。
对于初始质量$\gt 4M_\odot$的恒星，在AGB阶段它的对流区底部温度足够高以至于可以进行中子捕获核聚变，可以将刚合成好的元素(如$^{14}\mathrm{N}$, $^{23}\mathrm{Na}$和$\mathrm{Al}$)带到恒星大气中来。
本文根据不同的文章取了不同Z下的yield；后同。

- Super-AGB星。
其实就是大质量的AGB星；它们可以形成更重的元素，所以yield是不同的。

- Core-collapse超新星。
3D模拟的结果比1D还是差一点。
需要看看Nomoto的annual review（已下载）。
yield的误差来自于恒星演化中的各个物理过程，以及最后的collapse