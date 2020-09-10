# TOPCAT大型星表筛选交叉方法"

* any words
{:toc}

TOPCAT是个神器。师兄说的好，要是把它用6了，编程工作减少一半。它在星表读入输出、交叉、画图中具有的非常多的功能使得我们可以方便地获取数据、进行初步处理并查看某些参数的分布。这里通过两个有关Gaia的教程（[1](https://github.com/mbtaylor/tctuto/releases/download/asterics-vo-school-4/tctuto.pdf)、[2](http://docs.g-vo.org/adql-gaia/html/)）介绍一下如何获取像Gaia DR2这样的星表。这里默认读者已经有TOPCAT的基本使用经验。

## 星团证认：M4

### 一、获取M4附近的Gaia数据

这里我们将会用到Cone Search。这是专用于获取某个坐标附近一定角距离的程序。如果想获取多个坐标附近的源的话，用Multicone就可以了（当然得准备一个位置和搜索半径的表）。

1. 打开VO|Cone Search<br>
![](/img/in-post/post-topcat/1.png)
2. 在**Keyword**中输入`gaia dr2`并点击**Find Service**<br>
![](/img/in-post/post-topcat/2.png)
3. 在搜索结果中选择`ARI-Gaia`并在下面的**Object Name**中输入`M4`并点击**Resove**，在**Radius**中填入`1`(degree)
![](/img/in-post/post-topcat/3.png)
4. 点击**OK**并等待一会，TOPCAT就会将我们要的星表准备好了，44662个源
5. 回到主界面点击`Sky Plot`，看一下这个星表的空间分布
![](/img/in-post/post-topcat/4.png)
*你看这个Gaia它又大又圆*

至于实际上应该选择哪个星表，我的建议是在TAP窗口中搜索并看看星表的各种参数以及列名再确定。

### 二、通过自行挑出星团成员

这样下下来的星表包含了M3的成员星以及非常多的前景场星，而且它们混在了一起，所以我们需要通过星团成员星有相似的移动速度这个条件来将成员星挑出来。要注意这个方法只是为了演示，因为M4的自行非常大所以才能这样做，其他的星团基本上不行。

1. 回到主界面点击`Plane Plot`，并将x与y轴设为`pmra`与`pmdec`
![](/img/in-post/post-topcat/5.png)
2. 场星一般都是太阳附近的恒星，所以它们相对太阳应该没有整体的运动。所以中心不在(0,0)的那坨星就是星团的成员星了；将他们框起来并命名为`comoving`
![](/img/in-post/post-topcat/6.png)

### 三、验证成员星

这里我们将成员星与非成员星的自行画出来看一下。

1. 打开**Row Subset**，选中**comoving**，然后点击创建互补subset的按钮，瞬间就多了个**not_comoving**
![](/img/in-post/post-topcat/7.png)
2. 打开**SKy Plot**，将**subsets**选为**comoving**与**NOT_comoving**并换一下位置
![](/img/in-post/post-topcat/8.png)
3. 在**Frame**中加入**Sky Vector**，然后将**Delta Longitude**设为`pmra`以及**Delta Latitude设为`pmdec`，你就会发现
![](/img/in-post/post-topcat/9.png)
*好多头发！*
4. 将**Scale**调小，就可以看到两个subset不同的自行规律了
![](/img/in-post/post-topcat/10.png)

### 四、确定M4的视差

1. 打开上述两个subset的**Histogram Plot**，x轴设为`parallax`
![](/img/in-post/post-topcat/11.png)
2. 在**Forms**中添加**Add Gaussian**，就可以看到这两个subset的视差平均值了
![](/img/in-post/post-topcat/12.png)
![](/img/in-post/post-topcat/13.png)
$$ d_{\mathrm{M4}} = 1000 / \mathrm{Mean} = 2000 pc$$

要注意的是因为Gaia的视差误差不小（特别对于远的恒星来说），所以直接计算视差的倒数作为距离是不合适的。这里可以这样做是因为我们有很多恒星在同一个距离上。

## 相空间的星团证认：毕星团

这个例子使用相空间（3维速度空间）的密度来找星团。

### 获取太阳附近的Gaia数据

1. 打开TAP窗口，搜索`gaia`并选择**GAIA**
2. 选择`gaiadr2_gata_source`
3. 在ADQL Text窗口输入：
```
SELECT ra, dec, pmra, pmdec, parallax, radial_velocity, bp_rp,
phot_g_mean_mag + 5*log10(parallax/100) as g_abs
FROM gaiadr2.gaia_source WHERE parallax > 15 AND parallax_over_error > 5
AND radial_velocity IS NOT NULL
```

## TAP教程

### 下载整个星表

SELECT * FROM "table_name"

星表的名字可以先去Vizier搜链接，然后在TAP上找，就有了。

### 选择星表的前n行：SELECT

`SELECT TOP 1 1+1 AS result FROM gaiadr1.tgas_source`
![](/img/in-post/post-topcat/T-1.png)

`SELECT [TOP setLimit] selectList FROM fromClause [WHERE conditions] [GROUP BY columns] [ORDER BY columns] `<br>
`选择 行内容 列内容 AS 结果列名 FROM 源星表`

`SELECT TOP 10 * FROM gaiadr1.tgas_source`
![](/img/in-post/post-topcat/T-2.png)

`*`表示全部列都要（握拳）。

---

### 排序：ORDER BY

```
SELECT TOP 5 source_id, parallax
  FROM gaiadr1.tgas_source
  ORDER BY parallax
```
![](/img/in-post/post-topcat/T-3.png)

降序的话可以这样写：
```
SELECT TOP 5 source_id, parallax
  FROM gaiadr1.tgas_source
  ORDER BY parallax DESC
```

```
SELECT TOP 5 source_id, phot_g_mean_mag , parallax
  FROM gaiadr1.tgas_source
  ORDER BY phot_g_mean_mag, parallax
```

第二个排序列名的作用暂未确定。噢顺便，首行不缩进是因为：好看。

练习：在gaiadr1.tgas_source中选出最亮的20颗星的id和视星等

---

### 表达式的一些内容
- SQL中的名字是大小写敏感的
- 浮点数形式：`4.5e-8`
- 字符串必须用单引号括起来（双引号不行）
- 运算符号们
  - 加减乘除：`+-*/`；次幂：`POWER(), SQRT(x),  SQUARE(x)`
  - 不等号：`=, <, >, <=, >=`；注意不是`==`
  - 和或否：`AND, OR, NOT`
  - 字符串相加：`||`（未验证）
  - 格式化字符串：`LIKE()`；支持`%, _, *, ?`等（未验证）
  - `COS, ASIN, ATAN, ATAN2, COS, SIN, TAN`
  - `EXP, LOG`(natural logarithm),`LOG10`
  - `FLOOR(x), CEILING(x), ROUND(x), ROUND(x, n), TRUNCATE(x), TRUNCATE(x,n)`；n表示截止到多少位小数
  - `DEGREES(rads), RADIANS(degs)`
  - `RAND(seed)`
  - `MOD(x,y)`

```
SELECT TOP 10
  source_id,
  SQRT(POWER(pmdec_error,2)+POWER(pmra_error,2)) AS pm_errTot
  FROM gaiadr1.tgas_source
  ORDER BY pm_errTot
```

自己算出来的东西`pm_errTot`马上就可以拿来排序。

练习：Select the source id, position, proper motion in arcsec/yr and mag g for the 20 fastest stars in tgas_source.

---

### 有条件选择：WHERE

```
SELECT source_id, ra, dec
  FROM gaiadr1.tgas_source
  WHERE
  phot_g_mean_flux > 13
  AND parallax < 0.2
```

练习：Select the absolute magnitude, position and the source id for the 20 stars with the largest observed apparent magnitude in the g band from the table tgas_source (in case you don’t remember: The absolute magnitude is M= 5 + 5log π+ m with the parallax in arcsec π and the apparent magnitude m (check the units!). This will fail. Try to fix it.

---

### 交叉证认：JOIN

```
SELECT TOP 10 h1.ra, h1.dec, h1.hip, t1.hip
  FROM hipparcos AS h1
  JOIN tycho2 AS t1
  USING (hip)
```

```
FROM hipparcos AS h1
  JOIN tycho2 AS t1
  USING (hip)
```

Don't execute them.这俩是假例子。这俩的结果应该是内积。

---

### 更复杂的交叉证认：JOIN ON

```
SELECT TOP 20 source_id, h.hip
  FROM gaiadr1.tgas_source AS tgas
  LEFT OUTER JOIN hipparcos as h ON (tgas.phot_g_mean_mag BETWEEN h.hpmag -0.05 AND h.hpmag+0.05)
```

这里就不是内积了，是留左表，同时交叉条件改成了星等差在$$ \pm 0.05 $$之内。
（会出现1对n的情况吗？）

举一反三，肯定还有`INNER JOIN`（和`JOIN`一样）、`RIGHT OUTER JOIN`和`FULL OUTER JOIN`。

---

### 令人头大的交叉证认：基于位置

```
SELECT TOP 5
  source_id, tgas.ra, tgas.dec, tm.raj2000, tm.dej2000, hmag, e_hmag
  FROM gaiadr1.tgas_source as tgas
  JOIN twomass AS tm
  ON 1=CONTAINS (
     POINT('ICRS', tm.raj2000, tm.dej2000),
     CIRCLE('ICRS', tgas.ra, tgas.dec, 1.5/3600))
```

如果历元不同的话，最好不要在查询中转换历元（位置加减自行），而是将交叉半径扩大，然后用WHERE去解决历元的问题：

```
SELECT
   TOP 30
   *
   FROM ppmxl AS m
   JOIN gaiadr2.gaia_source AS g
   ON 1=CONTAINS(POINT('ICRS', m.raj2000, m.dej2000),
                 CIRCLE('ICRS', g.ra, g.dec, 30./3600.))
   WHERE 1=CONTAINS(POINT('ICRS',
   m.raj2000+m.pmra*COS(RADIANS(m.dej2000))*15,
   m.dej2000+m.pmde*15),
   CIRCLE('ICRS', g.ra, g.dec, 0.5/3600.))
```

### 俄罗斯套娃：查询中的查询

```
SELECT count(*) as n, round((hmag-jmag)*2) as bin
  FROM (SELECT TOP 4000 * FROM twomass) AS q
  GROUP BY bin
  ORDER BY bin
```

`(SELECT TOP 4000 * FROM twomass)`就是一个小的查询，用括号括起来就行了

## TOPCAT使用的某些tips

### 表格

  Column Window中的 ![](/img/in-post/post-topcat/T-4.png) 可以为subset在总表中添加布尔值标识
