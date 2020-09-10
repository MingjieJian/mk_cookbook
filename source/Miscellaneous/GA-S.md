# 銀河考古学总结 - 附录"

这里主要讲讲銀河考古学总结用到的论文图片背后的故事。论文不一定细读，但是至少要到能解释图片怎么来的、结果意味着什么的地步。

## 1 序章

### [Hopkins & Beacom 2006](http://adsabs.harvard.edu/abs/2006ApJ...651..142H)中的Fig. 1
![](/img/in-post/post-GA/1-hb06.png)

- 不同来源的数据给出了一致的结果
- SFR(Stellar Forming Rate)：一个点；SFH(Stellar Forming History)：一条线
- 通过不同方法可以探测星系的光度（不同波段），或者通过一些特征线等可以推断出星系的恒星形成率
- 观测到的SN II数量为SFH提供了一个下限（因为有被挡住的）
- 超级神冈探测器可以探测到弥散的超新星中微子背景，这提供了一个上限（大概是有多少恒星才能有多少超新星？）
- SFH应该与同时间的恒星质量密度(stellar mass density)匹配，但是在高红移处恒星质量密度显著低于SFH；这可能是我们的假设以及遮挡引起的。如果低红移处也有问题的话可能是因为IMF：SFR是从大质量恒星的光度得到的，而恒星质量密度主要是从小质量恒星处的到的，所以将这两个联系在一起的IMF的正确性就很重要了。当然从下图来说(b)使用的IMF更好一点，至少低红移处一致了。
![](/img/in-post/post-GA/1s-1-hb06.png)
*HB06, Fig.5. (a)、(b)使用的是[SalA和BG IMF](http://adsabs.harvard.edu/abs/2003ApJ...593..258B)*
- 金属的质量密度就更难观测了
- 模型和观测的超新星出现率还是挺一致的，而且观测到的有阻挡，所以比模型低是正常的。
- delay time控制的是SN Ia的拐点。
![](/img/in-post/post-GA/1s-2-hb06.png)
*HB06, Fig.7. 上面是SN II、下面是SN Ia的出现率。(a)、(b)使用的是[SalA和BG IMF](http://adsabs.harvard.edu/abs/2003ApJ...593..258B)*

----

- 什么是SFH的归一化？为什么要归一化？是指Fig. 1的那条曲线吗？<br>
  我认为这里的归一化指的是对SFH的限制，比如上下限；当然给出具体曲线也是归一化的一种。
- Salpeter IMF是什么样子的基于什么假设？<br>
  未查，参考[论文](http://adsabs.harvard.edu/abs/2003ApJ...593..258B)


### [Buonanno+1994](http://adsabs.harvard.edu/abs/1994A%26A...290...69B)中的Fig. 11
M3的CMD有不少版本，挺不一样的，比较一下应该会有意思。
![](/img/in-post/post-GA/1-b94.png)

- 完整性：文中给出了一个计算完整性的方法(section 2.4)；限于时间问题没有细看。我自己的想法是可以模拟一个恒星数密度关系然后看投影之后能看到多少恒星。操作层面来说，我们只能观测一个甜甜圈的范围，太里面的因为不完整其实不能拿来画图。
- CMD示意图给出了对图中各部分的解释:
![](/img/in-post/post-GA/1s-3.png)
[来源](http://www.astro.caltech.edu/~george/ay20/eaa-globcl.pdf)
- 演化顺序：MS->TO->RGB->HB->AGB
- RC其实是HB
- MS、RGB的位置以及宽度可以推断金属丰度（大小以及弥散）
- 和我的印象不一样的是，AGB是这些成分里面演化到最晚期的
- TO可以用来测量年龄，是星团里面最准确的年龄推断
- HB的位置由元素丰度（主要）、氦闪时He核质量以及包层质量决定；所以恒星在RGB阶段经历的质量流失是不一样的。次要原因还没有明确定论
- 金属丰度越高、包层质量越大、He核质量越小，HB越红（参见[这里](http://adsabs.harvard.edu/abs/1987ApJS...65...95S)、[这里](http://adsabs.harvard.edu/abs/1990ApJ...350..155L)）
- 由上，RHB和BHB也可以用来推断年龄
- HB中间是不稳定gap，是RR Lyrae（参见[这里](http://adsabs.harvard.edu/abs/1996ARA&A..34..551G)）
- BSS可能是两恒星的合并或者质量交换得来的，它们基本上处于星团的核心部位
