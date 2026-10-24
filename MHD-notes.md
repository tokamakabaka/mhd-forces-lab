---
title: "体积力、表面力与磁流体力学"
subtitle: "从场的动量守恒、Maxwell 应力到流体元运动方程"
author: "MHD Fluid Lab"
date: "2026-10-19"
lang: zh-CN
---

# 0. 阅读约定

本文使用 SI 单位制，讨论非相对论、准中性的单流体/多流体等离子体。矢量用粗体表示，张量用双箭头或粗体大写字母表示；$\mathbf u$ 与 $\mathbf v$ 都表示流体速度，引用图片公式时保留 $\mathbf u$ 与 $n,m,\mathbf F,p,\overleftrightarrow{\Pi},\mathbf R$ 的原符号。

本文的核心线索是：

1. 电磁场本身携带动量，电磁力可以写成 **Maxwell 应力张量的散度**；
2. 对流体元使用 Cauchy 应力与散度定理，可以把边界上的表面力写成体积内的力密度；
3. 图片中的 $mn\,d\mathbf u/dt=n\mathbf F-\nabla p-\nabla\cdot\overleftrightarrow{\Pi}+\mathbf R$ 与常见的 MHD 动量方程是同一本账，只是按“每粒子/每体积”记法不同；
4. 在非相对论 MHD 极限下，场的动量与位移电流可以忽略，电磁力主要剩下 $\mathbf J\times\mathbf B$，并可进一步分解为磁压与磁张力。

## 0.1 一条主线：表面力还是体积力？

本文用两条动量方程反复练习同一个判断：

- **表面力**：通过边界接触传递，总力是牵引力对面积的积分，几何相似时 $F_{\rm surface}\propto L^2$。压力与粘性是典型例子。
- **体积力**：作用在体积内每个质量元/电荷元上，总力是力密度对体积的积分，几何相似时 $F_{\rm body}\propto L^3$。重力与洛伦兹力是典型例子。

| 控制体账本 | 电磁场动量方程 | MHD 动量方程 |
|---|---|---|
| 表面通量 | $\displaystyle \oint_{\partial V}\mathbf T\cdot\mathbf n\,dS$（Maxwell 应力） | $\displaystyle \oint_{\partial V}\boldsymbol\sigma\cdot\mathbf n\,dS$（压力 + 粘性） |
| 体积源 | $\displaystyle \int_V\mathbf f\,dV$，$\mathbf f=\rho_e\mathbf E+\mathbf J\times\mathbf B$ | $\displaystyle \int_V(\mathbf J\times\mathbf B+\rho\mathbf g)\,dV$ |
| 体积惯性/动量 | $\displaystyle \frac{d}{dt}\int_V\mathbf g\,dV$，$\mathbf g=\varepsilon_0\mathbf E\times\mathbf B$（不是力） | $\displaystyle \frac{d}{dt}\int_V\rho\mathbf v\,dV$（不是力） |
| 判断 | $\mathbf T$ 是表面场应力，$\mathbf f$ 是体积力 | $p,\boldsymbol\tau$ 是表面力，$\mathbf J\times\mathbf B,\rho\mathbf g$ 是体积力 |

**关键：** 散度定理可以把表面力改写成体积分，但不会改变它的物理身份。判断看两件事——是否需要边界接触，以及总力随 $L^3$ 还是 $L^2$ 标度。

# 1. 场的动量守恒与 Maxwell 应力

## 1.1 洛伦兹力密度

单位体积内，电荷与电流受到的电磁力为

$$
\mathbf f=\rho_e\mathbf E+\mathbf J\times\mathbf B,
$$

其中 $\rho_e$ 是体电荷密度，$\mathbf J$ 是电流密度。若把电荷看成离散粒子，单个粒子受力为

$$
\mathbf F=q(\mathbf E+\mathbf u\times\mathbf B).
$$

这正是图片中 $n\mathbf F$ 的来源：$n$ 是数密度，$n\mathbf F$ 是单位体积的电磁力。

## 1.2 场携带动量

电磁场不是被动的数学背景。场的动量密度为

$$
\mathbf g=\varepsilon_0\mathbf E\times\mathbf B=\frac{1}{c^2}\mathbf S,
\qquad
\mathbf S=\frac{1}{\mu_0}\mathbf E\times\mathbf B,
$$

其中 $\mathbf S$ 是坡印廷矢量。场动量可以与粒子机械动量相互转化；在电磁波、充电电容器、磁体与电荷的组合中，场动量都真实地参与总动量守恒。

## 1.3 Maxwell 应力张量

定义 Maxwell 应力张量

$$
T_{ij}
=
\varepsilon_0\left(E_iE_j-\frac12\delta_{ij}E^2\right)
+
\frac{1}{\mu_0}\left(B_iB_j-\frac12\delta_{ij}B^2\right).
$$

它是一个对称张量。将其写成并矢形式：

$$
\mathbf T
=
\varepsilon_0\left(\mathbf E\mathbf E-\frac12E^2\mathbf I\right)
+
\frac{1}{\mu_0}\left(\mathbf B\mathbf B-\frac12B^2\mathbf I\right).
$$

对任意控制体 $V$，场的动量账本为

$$
\int_V\mathbf f\,dV
+
\frac{d}{dt}\int_V\mathbf g\,dV
=
\oint_{\partial V}\mathbf T\cdot\mathbf n\,dS.
$$

等价地，局域形式为

$$
\mathbf f+\frac{\partial\mathbf g}{\partial t}
=
\nabla\cdot\mathbf T.
$$

**读法：** 左边是“粒子受力 + 场动量变化”，右边是应力穿过边界的通量。若场是静态的，$\partial\mathbf g/\partial t=0$，于是

$$
\mathbf f=\nabla\cdot\mathbf T.
$$

这说明：静态电磁力可以完全用边界上的 Maxwell 应力通量来解释。体积内的力与边界上的应力，是同一本账的两种记法。

## 1.4 场动量与表面力/体积力的类比

Maxwell 应力 $\mathbf T$ 是**表面通量**，单位是 N m$^{-2}$；$\mathbf f$ 是**体积力密度**，单位是 N m$^{-3}$。二者通过散度定理联系：

$$
\int_V \mathbf f\,dV=\oint_{\partial V}\mathbf T\cdot\mathbf n\,dS
\quad(\text{静态场}).
$$

这与流体中的压力/粘性完全平行：边界上的牵引力 $\mathbf t(\mathbf n)=\boldsymbol\sigma\cdot\mathbf n$ 是表面力，取散度后得到体积内的力密度 $\nabla\cdot\boldsymbol\sigma$。**“写成体积分”不等于“物理上变成体积力”**，这是本文反复强调的区分。

## 1.5 非相对论 MHD 极限

在非相对论 MHD 中，电场能、位移电流和场动量项相对于磁压都是小量。只保留磁场部分：

$$
\mathbf T_M=\frac{1}{\mu_0}\left(\mathbf B\mathbf B-\frac12B^2\mathbf I\right).
$$

由 $\nabla\times\mathbf B=\mu_0\mathbf J$ 和 $\nabla\cdot\mathbf B=0$：

$$
\nabla\cdot\mathbf T_M
=
\frac{(\mathbf B\cdot\nabla)\mathbf B}{\mu_0}
-\nabla\left(\frac{B^2}{2\mu_0}\right)
=
\mathbf J\times\mathbf B.
$$

这就是 MHD 中的洛伦兹体积力。它还可以拆成：

$$
\mathbf J\times\mathbf B
=
-\nabla\left(\frac{B^2}{2\mu_0}\right)
+
\frac{(\mathbf B\cdot\nabla)\mathbf B}{\mu_0}.
$$

第一项是**磁压梯度**，第二项是**磁张力**。两者各自都有沿磁场方向的分量，但平行分量恰好抵消，因此净洛伦兹力垂直于 $\mathbf B$。

## 1.6 磁压与磁张力的直观图像

- **磁压**：把磁力线想成沿磁场方向排列的弹性带。磁场强的地方“带子”更密，会向磁场弱的方向施加侧向压力，$p_m=B^2/(2\mu_0)$。
- **磁张力**：沿磁力线方向存在张力 $B^2/\mu_0$。磁力线弯曲时，张力指向曲率中心，试图把弯曲拉直。
- 对曲率半径为 $R$ 的弯曲磁力线，横向张力尺度约为 $B^2/(\mu_0R)$。

这些是帮助记忆的类比，不是新的物理力；它们只是同一个 $\mathbf J\times\mathbf B$ 的不同记账方式。

# 2. 从场到流体元：图片方程的符号与含义

## 2.1 图片中的方程

图片给出的流体元运动方程为

$$
mn\frac{d\mathbf u}{dt}
=
n\mathbf F-\nabla p-\nabla\cdot\overleftrightarrow{\Pi}+\mathbf R.
$$

左侧 $mn\,d\mathbf u/dt$ 是单位体积的动量变化率：$mn=\rho$ 是质量密度，$d\mathbf u/dt$ 是随体加速度。右侧每一项都是单位体积的力，单位 N m$^{-3}$。

## 2.2 符号逐一解释

| 符号 | 含义 | 说明 |
|---|---|---|
| $n$ | 数密度 | 单位体积的粒子数，m$^{-3}$ |
| $m$ | 单粒子质量 | $mn=\rho$ 是质量密度 |
| $\mathbf u$ | 流体元速度 | $d\mathbf u/dt$ 是随体加速度 |
| $\mathbf F$ | 单个粒子受力 | 电磁场中 $\mathbf F=q(\mathbf E+\mathbf u\times\mathbf B)$ |
| $p$ | 各向同性压强 | 压强张量的对角部分，给出法向表面力 |
| $\overleftrightarrow{\Pi}$ | 偏应力/非对角压强张量 | 粘性、剪切、各向异性压力；给出偏斜的表面力 |
| $\mathbf R$ | 异种粒子碰撞摩擦 | $\alpha$ 粒子与不同 $\beta$ 粒子碰撞失去的动量；同类粒子碰撞因动量守恒相互抵消 |

图片特别强调：

- $n\mathbf F$ 是**电磁场力**，其中 $\mathbf F=q(\mathbf E+\mathbf u\times\mathbf B)$，属于体积力；
- $-\nabla p$ 是**热压力**，$p$ 是压强张量的对角项，属于表面力；
- $-\nabla\cdot\overleftrightarrow{\Pi}$ 是**粘滞力**，$\overleftrightarrow{\Pi}$ 是压强张量的非对角项，属于表面力；
- $\mathbf R$ 是异种粒子弹性碰撞造成的摩擦阻力，是体积力；同类粒子碰撞由于动量守恒，对 $\mathbf R$ 没有贡献。

若把完整压强张量写成

$$
\mathbf P=p\mathbf I+\overleftrightarrow{\Pi},
$$

则压力与偏应力合在一起给出

$$
-\nabla\cdot\mathbf P=-\nabla p-\nabla\cdot\overleftrightarrow{\Pi}.
$$

这也是图片中 $-\nabla p-\nabla\cdot\overleftrightarrow{\Pi}$ 的来源。

## 2.3 与常见 MHD 方程的对应

对单组分流体，$\mathbf R=0$，$mn=\rho$，$\mathbf u=\mathbf v$。对多组分等离子体，把各物种的方程相加，可以得到单流体方程。对应关系如下：

| 图片写法 | 物理含义 | 常见 MHD 写法 |
|---|---|---|
| $mn$ | 质量密度 | $\rho$ |
| $\mathbf u$ | 流体速度 | $\mathbf v$ |
| $n\mathbf F$ | 电磁力密度 | $\rho_e\mathbf E+\mathbf J\times\mathbf B$；准中性 MHD 中主要为 $\mathbf J\times\mathbf B$ |
| $-\nabla p$ | 各向同性压力 | $-\nabla p$ |
| $-\nabla\cdot\overleftrightarrow{\Pi}$ | 偏应力/粘性力 | $\nabla\cdot\boldsymbol\tau$ |
| $\mathbf R$ | 异种粒子摩擦 | 常略去；或作为阻力、电阻、离子—中性粒子摩擦保留 |
| （可加）$\rho\mathbf g$ | 重力 | $\rho\mathbf g$ |

使用映射时要注意符号约定。若采用

$$
\boldsymbol\sigma=-p\mathbf I+\boldsymbol\tau,
\qquad
\mathbf t(\mathbf n)=\boldsymbol\sigma\cdot\mathbf n,
$$

则粘性力密度为 $+\nabla\cdot\boldsymbol\tau$。图片把偏应力写成 $-\nabla\cdot\overleftrightarrow{\Pi}$，因此若两种写法的偏应力相同，必须有

$$
\overleftrightarrow{\Pi}=-\boldsymbol\tau.
$$

这只是符号约定，不是物理差异。

## 2.4 为什么 $\mathbf R$ 是体积力？

$\mathbf R$ 来自粒子碰撞造成的动量交换。它作用在每个粒子上，大小与局部密度、碰撞频率和相对速度有关，因此是单位体积的力密度。它与边界接触无关，不需要通过流体元的表面传递。同类粒子之间的碰撞满足动量守恒，不会产生净摩擦；只有不同种类粒子之间的碰撞才会留下 $\mathbf R$。

在单流体 MHD 中，电子—离子摩擦与电阻耗散有关，离子—中性粒子摩擦则常见于部分电离等离子体。具体形式取决于碰撞模型，不能把 $\mathbf R$ 简单等同于 $\eta\mathbf J$；后者只是电阻性 Ohm 定律中的一项。

## 2.5 把图片方程写成随体导数

如果速度场是宏观连续场，$d\mathbf u/dt$ 应理解为随体导数：

$$
\frac{d\mathbf u}{dt}
=
\frac{\partial\mathbf u}{\partial t}
+\mathbf u\cdot\nabla\mathbf u.
$$

于是图片方程可写成

$$
mn\left(\frac{\partial\mathbf u}{\partial t}+\mathbf u\cdot\nabla\mathbf u\right)
=
n\mathbf F-\nabla p-\nabla\cdot\overleftrightarrow{\Pi}+\mathbf R.
$$

除以 $mn$ 后，左边就是加速度，右边是各种“比力”。

# 3. 连续介质力学的两本账

## 3.1 材料体积与动量定理

取随流体运动的材料体积 $V(t)$，边界为 $\partial V$，外法向为 $\mathbf n$。动量定理为

$$
\frac{d}{dt}\int_V\rho\mathbf v\,dV
=
\int_V(\rho\mathbf g+\mathbf J\times\mathbf B)\,dV
+
\oint_{\partial V}\mathbf t(\mathbf n)\,dS.
$$

这里把重力与洛伦兹力显式写成体积力；边界牵引力 $\mathbf t(\mathbf n)$ 是表面力。

## 3.2 Cauchy 应力

牵引力不仅取决于位置，还取决于截面方向。Cauchy 应力张量 $\boldsymbol\sigma$ 定义为

$$
\mathbf t(\mathbf n)=\boldsymbol\sigma\cdot\mathbf n.
$$

对牛顿流体，

$$
\boldsymbol\sigma=-p\mathbf I+\boldsymbol\tau,
$$

其中 $p$ 是热压力，$\boldsymbol\tau$ 是粘性偏应力。

## 3.3 散度定理

对表面力积分使用散度定理：

$$
\oint_{\partial V}\boldsymbol\sigma\cdot\mathbf n\,dS
=
\int_V\nabla\cdot\boldsymbol\sigma\,dV.
$$

代入 $\boldsymbol\sigma=-p\mathbf I+\boldsymbol\tau$：

$$
\nabla\cdot\boldsymbol\sigma
=
-\nabla p+\nabla\cdot\boldsymbol\tau.
$$

于是材料体积的动量方程化为

$$
\rho\frac{D\mathbf v}{Dt}
=
-\nabla p+\nabla\cdot\boldsymbol\tau
+\mathbf J\times\mathbf B+\rho\mathbf g.
$$

每一项的单位都是 N m$^{-3}$。

## 3.4 为什么表面力可以写成体积分？

因为对流体元来说，边界力常常几乎两两抵消。均匀压力从四面八方同时挤压，合力为零；只有应力在空间上不均匀时，才留下一个正比于体积的净力。散度定理把“边界上的账”改写成“体积内的力密度”，但没有改变压力的物理来源。

关键区分：

- **体积力**：作用在每个质量元/电荷元上，总力 $\propto L^3$；如重力、$\mathbf J\times\mathbf B$。
- **表面力**：通过边界接触传递，总力 $\propto L^2$；如压力、粘性力。

## 3.5 尺度律

对几何相似、特征尺寸为 $L$ 的流体元：

$$
F_{\text{body}}\sim fL^3,
\qquad
F_{\text{surface}}\sim tL^2,
\qquad
\frac{F_{\text{surface}}}{F_{\text{body}}}\propto\frac{1}{L}.
$$

尺寸缩小 10 倍，体积力总量变成 $1/1000$，表面力总量只变成 $1/100$；表面力相对放大 10 倍。这是微尺度流动中粘性、界面效应相对重要的原因之一。

## 3.6 均匀压力为什么没有净力？

均匀压力 $p_0$ 给出

$$
\oint_{\partial V}-p_0\mathbf n\,dS
=
-\int_V\nabla p_0\,dV
=
0.
$$

它可以让流体元变形或压缩，但不会推动质心。只有压力梯度 $-\nabla p$ 才给出净力。

# 4. MHD 方程组

## 4.1 连续性方程

$$
\frac{\partial\rho}{\partial t}+\nabla\cdot(\rho\mathbf v)=0.
$$

## 4.2 动量方程

$$
\rho\left(\frac{\partial\mathbf v}{\partial t}+\mathbf v\cdot\nabla\mathbf v\right)
=
-\nabla p+\nabla\cdot\boldsymbol\tau
+\mathbf J\times\mathbf B+\rho\mathbf g.
$$

若保留异种粒子摩擦，可在右边加上 $\mathbf R$。

## 4.3 Ohm 定律与感应方程

电阻性 Ohm 定律：

$$
\mathbf E+\mathbf v\times\mathbf B=\eta\mathbf J,
\qquad
\eta=\frac{1}{\mu_0\sigma}.
$$

取旋度并利用 Faraday 定律，得到感应方程：

$$
\frac{\partial\mathbf B}{\partial t}
=
\nabla\times(\mathbf v\times\mathbf B)
+\eta\nabla^2\mathbf B.
$$

在理想 MHD（$\eta\to0$）中，磁通量被流体冻结：

$$
\frac{\partial\mathbf B}{\partial t}
=
\nabla\times(\mathbf v\times\mathbf B).
$$

## 4.4 Maxwell 方程与约束

$$
\nabla\cdot\mathbf E=\frac{\rho_e}{\varepsilon_0},
\qquad
\nabla\cdot\mathbf B=0,
$$

$$
\nabla\times\mathbf E=-\frac{\partial\mathbf B}{\partial t},
\qquad
\nabla\times\mathbf B=\mu_0\mathbf J
+\mu_0\varepsilon_0\frac{\partial\mathbf E}{\partial t}.
$$

非相对论 MHD 中通常忽略位移电流，因此

$$
\mathbf J=\frac{1}{\mu_0}\nabla\times\mathbf B.
$$

## 4.5 能量方程（示意）

忽略辐射、热传导与外部加热时，理想 MHD 的能量方程可写成

$$
\frac{\partial}{\partial t}
\left(
\frac12\rho v^2+\frac{p}{\gamma-1}+\frac{B^2}{2\mu_0}
\right)
+
\nabla\cdot\left[
\left(\frac12\rho v^2+\frac{\gamma p}{\gamma-1}\right)\mathbf v
+\frac{\mathbf E\times\mathbf B}{\mu_0}
\right]=0.
$$

各项分别对应动能、内能、磁能以及它们的通量。实际等离子体还需要热传导、辐射、粘性耗散、电阻耗散等项。

## 4.6 状态方程

$$
p=p(\rho,T),
$$

例如理想气体 $p=nkT$。在磁化、无碰撞等离子体中，压强可能是各向异性的：

$$
\mathbf P=p_\perp\mathbf I+(p_\parallel-p_\perp)\mathbf b\mathbf b,
\qquad
\mathbf b=\frac{\mathbf B}{B},
$$

此时压力项应写成 $-\nabla\cdot\mathbf P$，而不是简单的 $-\nabla p$。

# 5. 各项物理的进一步解释

## 5.1 热压力

热压力来自粒子随机运动穿过界面输运的动量。它是表面力，方向沿界面法向；大小各向同性时写成 $p\mathbf I$。

- 均匀压力：合力为零，但可以压缩/变形；
- 压力梯度：产生从高压指向低压的净力；
- 理想气体：$p=nkT$；
- 各向异性等离子体：$-\nabla\cdot\mathbf P$。

## 5.2 粘滞力

粘性是动量的扩散。速度不同的相邻流层通过剪切应力互相拖拽。牛顿流体的偏应力为

$$
\boldsymbol\tau
=
\mu\left[
\nabla\mathbf v+(\nabla\mathbf v)^{\mathsf T}
-\frac23(\nabla\cdot\mathbf v)\mathbf I
\right]
+\zeta(\nabla\cdot\mathbf v)\mathbf I.
$$

不可压时 $\nabla\cdot\mathbf v=0$，于是

$$
\nabla\cdot\boldsymbol\tau=\mu\nabla^2\mathbf v.
$$

粘性力只在应力不均匀时留下净力；均匀剪切对应两面上的力相互抵消。无滑移壁面附近形成边界层。

## 5.3 洛伦兹力

$$
\mathbf f_L=\rho_e\mathbf E+\mathbf J\times\mathbf B.
$$

准中性 MHD 中，$\rho_e\mathbf E$ 通常远小于 $\mathbf J\times\mathbf B$，因此主要保留

$$
\mathbf f_L\approx\mathbf J\times\mathbf B.
$$

它不是边界接触力，而是作用在体积内每个电流元上的体积力。

## 5.4 重力

$$
\mathbf f_g=\rho\mathbf g.
$$

重力作用于每个质量元，是体积力。它常与压力梯度、洛伦兹力一起形成静力平衡：

$$
0=-\nabla p+\mathbf J\times\mathbf B+\rho\mathbf g.
$$

## 5.5 异种粒子摩擦 $\mathbf R$

$\mathbf R$ 是不同种类粒子碰撞造成的动量交换率。它作用于体积内的粒子，因此是体积力。对同类粒子，碰撞前后总动量守恒，净摩擦为零。对电子—离子等离子体，摩擦与电阻耗散相关；对部分电离等离子体，离子—中性粒子摩擦会表现为明显的阻尼。

# 6. 磁压、磁张力与平衡

## 6.1 分解

$$
\mathbf J\times\mathbf B
=
-\nabla\left(\frac{B^2}{2\mu_0}\right)
+
\frac{(\mathbf B\cdot\nabla)\mathbf B}{\mu_0}.
$$

- 磁压：$p_m=B^2/(2\mu_0)$；
- 磁张力：沿磁力线方向，张力为 $B^2/\mu_0$；
- 两项的平行分量相消，净力垂直于 $\mathbf B$。

## 6.2 等离子体 beta

$$
\beta=\frac{p}{p_m}=\frac{2\mu_0p}{B^2}.
$$

- $\beta\ll1$：磁压主导，磁场约束强；
- $\beta\sim1$：热压与磁压相当；
- $\beta\gg1$：热压主导，磁场容易被流体拖动。

## 6.3 Z-pinch

轴向电流 $J_z$ 产生角向磁场 $B_\phi$。洛伦兹力

$$
\mathbf J\times\mathbf B=J_z\hat{\mathbf z}\times B_\phi\hat{\boldsymbol\phi}
=-J_zB_\phi\hat{\mathbf r}
$$

指向中心，形成箍缩。热压力向外抵抗，平衡时满足径向压力平衡。

## 6.4 $\theta$-pinch

角向电流与轴向磁场作用，产生径向力。它与 Z-pinch 一起构成磁约束装置的基本几何；环向场与极向场的组合则通向托卡马克。

## 6.5 无力场

若 $\mathbf J\parallel\mathbf B$，则

$$
\mathbf J\times\mathbf B=0.
$$

这种磁场称为无力场。此时磁场力为零，压力梯度也必须为零（或由其他力平衡）；无力场常见于太阳日冕和部分实验室等离子体。

# 7. 尺度与无量纲数

定义特征速度 $U$、特征长度 $L$、密度 $\rho$、动力粘度 $\mu$、电导率 $\sigma$、磁场 $B$、压力差 $\Delta p$。常用无量纲数：

$$
Re=\frac{\rho UL}{\mu},
\qquad
Rm=\mu_0\sigma UL,
\qquad
Ha=BL\sqrt{\frac{\sigma}{\mu}},
$$

$$
N=\frac{\sigma B^2L}{\rho U}=\frac{Ha^2}{Re},
\qquad
\beta=\frac{2\mu_0p}{B^2},
\qquad
v_A=\frac{B}{\sqrt{\mu_0\rho}}.
$$

物理意义：

- $Re$：惯性/粘性；
- $Rm$：感应/磁扩散；
- $Ha$：磁力/粘性（Hartmann 数）；
- $N$：磁力/惯性（相互作用参数）；
- $\beta$：热压/磁压；
- $v_A$：阿尔芬速度。

力密度尺度：

$$
f_i\sim\frac{\rho U^2}{L},
\qquad
f_p\sim\frac{\Delta p}{L},
\qquad
f_v\sim\frac{\mu U}{L^2},
\qquad
f_B\sim\frac{B^2}{\mu_0L},
\qquad
f_g\sim\rho g.
$$

注意：$f_B=B^2/(\mu_0L)$ 是磁压梯度尺度；讨论导电流体在磁场中运动时，感应制动尺度是 $\sigma UB^2$，对应 $N$。两者不是同一个量，不能混用。

# 8. 等离子体波与沙盒：静电波与 Alfvén 波

## 8.1 两种波对照

| | 静电波（Langmuir） | Alfvén 波 |
|---|---|---|
| 恢复力 | 电场力 | 磁张力 / 洛伦兹力 |
| 模型 | 1D 电子流体，固定离子 | 2D 不可压 MHD + 均匀引导场 |
| 关键量 | $n,u,E$ | $\mathbf u,A,B_0,J_z$ |
| 频率/速度 | $\omega\approx\omega_{pe}=1$（归一化） | $v_A=B_0/\sqrt{\mu_0\rho}$ |
| 磁场扰动 | 忽略（静电近似） | 核心：横向 $b_y$ |

两者都是“波”，但恢复力不同：静电波靠电荷分离产生的电场，Alfvén 波靠弯曲磁力线的张力。

## 8.2 静电波：一维电子流体

### 8.2.1 归一化方程

取 $\omega_{pe}=1$，固定离子，冷电子流体：

$$
\partial_t n+\partial_x(nu)=0,
\qquad
\partial_t u+u\,\partial_xu=-E-\nu u,
\qquad
\partial_xE=1-n.
$$

$n$ 是电子密度，$u$ 是电子速度，$E$ 是电场，$\nu$ 是唯象阻尼。压力、离子运动、磁场扰动都略去。

### 8.2.2 线性化与色散

令 $n=1+\delta n$，保留一阶项：

$$
\partial_t\delta n=-\partial_xu,
\qquad
\partial_tu=-E,
\qquad
\partial_xE=-\delta n.
$$

消去 $u,E$：

$$
\partial_t^2\delta n+\delta n=0
\quad\Longrightarrow\quad
\omega^2=1=\omega_{pe}^2.
$$

这是冷等离子体的 Langmuir 振荡：频率近似与波数无关。密度与电场有 90° 相位差。

### 8.2.3 初值与数值

初始条件：

$$
n(x,0)=1+\delta\cos(kx),
\qquad
u(x,0)=0,
\qquad
E(x,0)=-\frac{\delta}{k}\sin(kx).
$$

代码用 256 个周期网格点；连续性方程用迎风面通量，动量方程用迎风平流，电场由 $\partial_xE=1-n$ 累加并减去均值。时间步 $\Delta t=0.006$，每帧最多 3 步。增加振幅会看到非线性陡化；增加 $\nu$ 会看到衰减。模型没有 Landau 阻尼、电子热压或离子运动。

## 8.3 Alfvén 波：二维不可压 MHD + 引导场

### 8.3.1 方程

$$
\partial_t\mathbf u+\mathbf u\cdot\nabla\mathbf u
=-\nabla p+\nu\nabla^2\mathbf u+\alpha\mathbf J\times\mathbf B,
\qquad
\nabla\cdot\mathbf u=0,
$$

$$
\mathbf B=B_0\hat{\mathbf x}+\nabla\times(A\hat{\mathbf z}),
\qquad
\partial_tA+\mathbf u\cdot\nabla A=-B_0u_y+\eta\nabla^2A,
\qquad
J_z=-\nabla^2A.
$$

$A$ 是**扰动**磁通量函数；$B_0\hat x$ 是单独保留的均匀引导场。因此 $\nabla\cdot\mathbf B=0$ 自动成立，但磁力线是总场 $\mathbf B$ 的积分曲线，不是 $A$ 的闭合等值线。

### 8.3.2 线性 Alfvén 波

只保留 $u_y$ 和 $A$ 的一阶项：

$$
\partial_tA=-B_0u_y,
\qquad
\partial_tu_y=\frac{B_0}{\rho}J_z
=-\frac{B_0}{\rho}\nabla^2A.
$$

消去 $u_y$：

$$
\partial_t^2A
=\frac{B_0^2}{\rho}\nabla^2A
\quad\Longrightarrow\quad
\omega^2=\frac{B_0^2}{\rho}k^2
=v_A^2k^2.
$$

代码取 $\rho=1,\mu_0=1$，所以 $v_A=B_0$。横向速度与磁场扰动同相/反相，流体元做横向摆动，波沿 $B_0$ 传播。

### 8.3.3 初值与数值

取 $k=2\pi$、$A_0=0.06$、$B_0=0.55$：

$$
A(x,0)=A_0\cos(kx),
\qquad
u_y(x,0)=-kA_0\sin(kx),
\qquad
u_x=0.
$$

这是向右传播的 Alfvén 波初值。二维网格 $128^2$，周期边界，$\Delta t=0.03$；洛伦兹力不做归一化（`fScale=1`），因此 $\alpha=1$ 对应物理耦合。磁力线用总场 $\mathbf B$ 的 RK2 积分曲线绘制，而不是 $A$ 的等值线。

## 8.4 代码实现

| 模型 / 步骤 | 代码位置 | 作用 |
|---|---|---|
| 静电波：连续性 | `initESWave()` 的 `step()` | 迎风面通量 + 密度更新 |
| 静电波：动量 | `step()` | 迎风平流 $-E-\nu u$ |
| 静电波：电场 | `solveE()` | 积分 $\partial_xE=1-n$，减均值 |
| Alfvén：B, J | `derive()` | $B_x=B_0+\partial_yA$，$B_y=-\partial_xA$，$J_z=-\nabla^2A$ |
| Alfvén：投影 | `project(dt, 12)` | 12 次 Jacobi + 压力校正 |
| Alfvén：A 演化 | `step()` | 平流 $-B_0u_y$ + 电阻扩散 |
| Alfvén：磁力线 | `drawGuideFieldLines()` | RK2 追踪总场 B 的积分曲线 |

静电波的一步：

```text
uf = 0.5*(u[i] + u[i+1])
flux[i] = uf > 0 ? n[i]*uf : n[i+1]*uf
n_new[i] = n[i] - dt/dx*(flux[i] - flux[i-1])
u_new[i] = u[i] + dt*(-u[i]*du_dx - E[i] - damp*u[i])
solveE()
```

Alfvén 的一步：

```text
u = advect(u); v = advect(v)
derive()                    // bx = B0 + dA/dy; by = -dA/dx; J = -lap(A)
ax = alpha*J*(-by) + nu*lap(u)
ay = alpha*J*( bx) + nu*lap(v)
project(dt, 12)
A = advect(A) + dt*(-B0*v + eta*lap(A))
derive(); updateParticles(dt)
```

静电波的状态是 256 点的一维数组 `n,u,E`；Alfvén 的状态是 $128^2$ 的 `u,v,A,p,bx,by,J`。两个求解器都用周期边界，物理步进与渲染分离。

## 8.5 数值细节与限制

- 静电波：一阶迎风，256 点，$\Delta t=0.006$，每帧最多 3 步；有数值扩散。
- Alfvén：128²，$\Delta t=0.03$，12 次 Jacobi 近似投影，半拉格朗日平流有数值扩散。
- 静电波是冷电子、固定离子、静电近似；没有 Landau 阻尼、电子热压、离子运动。
- Alfvén 是二维不可压单流体；压力只是投影乘子，没有密度/热力学/三维不稳定性。
- 两者都是定性演示，不是定量预测。

## 8.6 读图

**静电波：** 看密度条纹与电场曲线。密度条纹在原地振荡，电场与密度约有 90° 相位差；增加 $\delta$ 看非线性，增加 $\nu$ 看衰减。没有磁力线参与。

**Alfvén 波：** 先看横向速度/背景电流形成的条纹，再看磁力线是否像琴弦一样上下摆动。扰动沿 $B_0$ 传播；磁张力是恢复力。切换背景到电流密度，可以看波峰处的电流片；看示踪粒子，可以看到横向摆动。

一句话：**静电波是“电场把电子拉回”，Alfvén 波是“磁张力把磁力线拉直”。**


# 9. 常见误区

1. **“压力是体积力，因为 $-\nabla p$ 出现在体积分里。”**  
   压力是表面力；$-\nabla p$ 是边界牵引力经散度定理后的力密度。

2. **“$\mathbf J\times\mathbf B$ 可以写成 $\nabla\cdot\mathbf T_M$，所以它是表面力。”**  
   数学上任何体积力都可以写成某个张量的散度。分类看物理传递：洛伦兹力作用于体积内每个电流元，不需要边界接触。

3. **“粘性只在壁面附近存在。”**  
   只要存在速度梯度，流体内部就有粘性应力。壁面只是最常见的强剪切区。

4. **“均匀压力会让流体元整体加速。”**  
   均匀压力从各面同时挤压，合力为零；只有压力梯度给出净力。

5. **“磁压和磁张力是两种独立的力。”**  
   它们只是 $\mathbf J\times\mathbf B$ 的分解；两项的平行分量相消，净力垂直于 $\mathbf B$。

6. **“物体缩小，所有力都等比缩小。”**  
   体积力 $\propto L^3$，表面力 $\propto L^2$；缩小 10 倍，表面力/体积力放大 10 倍。

7. **“图片中的 $\mathbf R$ 就是电阻。”**  
   $\mathbf R$ 是异种粒子碰撞的摩擦阻力；电阻性 Ohm 定律中的 $\eta\mathbf J$ 只是其中一种具体建模，二者不能简单画等号。

# 10. 符号表

| 符号 | 含义 |
|---|---|
| $\rho$ | 质量密度 |
| $n$ | 数密度 |
| $m$ | 单粒子质量 |
| $\mathbf u,\mathbf v$ | 流体速度 |
| $\mathbf F$ | 单粒子受力 |
| $\mathbf f$ | 力密度 |
| $p$ | 各向同性压强 |
| $\mathbf P$ | 压强张量 |
| $\overleftrightarrow{\Pi}$ | 偏应力/非对角压强张量 |
| $\boldsymbol\tau$ | 粘性偏应力 |
| $\boldsymbol\sigma$ | Cauchy 应力张量 |
| $\mathbf R$ | 异种粒子碰撞摩擦 |
| $\mathbf E,\mathbf B$ | 电场、磁场 |
| $\mathbf J$ | 电流密度 |
| $\rho_e$ | 体电荷密度 |
| $\mathbf T$ | Maxwell 应力张量 |
| $\mathbf g$ | 场动量密度 |
| $\mathbf S$ | 坡印廷矢量 |
| $\mu_0,\varepsilon_0$ | 真空磁导率、介电常数 |
| $\eta$ | 磁扩散系数 |
| $\sigma$ | 电导率 |
| $\nu$ | 运动粘度 |
| $\mu$ | 动力粘度 |
| $\beta$ | 等离子体 beta |
| $v_A$ | 阿尔芬速度 |

# 11. 参考文献

1. L. D. Landau, E. M. Lifshitz, *Fluid Mechanics*, 2nd ed.
2. P. A. Davidson, *Introduction to Magnetohydrodynamics*.
3. J. P. Freidberg, *Ideal MHD*.
4. J. D. Jackson, *Classical Electrodynamics*, 3rd ed.
5. S. I. Braginskii, “Transport Processes in a Plasma,” *Reviews of Plasma Physics*, Vol. 1.
6. D. D. Ryutov, “The role of magnetic tension and pressure in plasma confinement,” relevant review articles.
