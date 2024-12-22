# M.1 数学随笔（1）极限与连续性证明

*命题1：如果$a>b$，则存在$c$，使得$a>c>b$。证明：取$c=\frac12(a+b)$即可。*

*命题2：$a=b$的充要条件是$\forall \epsilon>0,|a-b|\le\epsilon$。证明：必要性显然。对于充分性，不妨若$a>b$，则取$\epsilon=\frac {a-b}2>0,|a-b|>\epsilon$，矛盾。*

这两条都是十分显然的定理，因为我们知道实数是稠密的。但就它们，就足够加深对极限和连续的理解了。

回顾极限的定义：以函数趋于一点的极限为例，$\forall \epsilon>0, \exists\delta > 0,\forall x:0<|x-x_0|<\delta, |f(x)-A|<\epsilon$，则记$\lim\limits_{x\rightarrow x_0}f(x)=A$。特别的，若$A=f(x_0)$，则$f(x)$在$x_0$处连续。

那极限本质上是在说一件什么事情呢？也就是说，在$x\rightarrow x_0$的过程中，$f(x)$离A的距离被限制得不会太远。如果我们在连续函数上任取两个函数值不相等的点，那我们总有办法用一根分界线分开这两个点及其相关邻域。不过在此之前，我们先回顾一下一条看起来十分显然的命题：

**例1.0**. 给定正数$M>0$，证明：$\lim\limits_{x\rightarrow x_0}f(x)=A$与$\forall \epsilon>0, \exists\delta > 0,\forall x:0<|x-x_0|<\delta, |f(x)-A|<M\epsilon$等价。

分析：考虑“两步存在”构建命题桥梁。这里很多人会想描述成“因为$\epsilon$是任意的，所以$M\epsilon$是任意的”之类的表述，但这种表述在数学上是不规范的。本随笔专栏的一大目标也是将这种很直观但说不清楚的事情用严谨的数学语言表述。

证明：充分性。$\forall\epsilon>0,\exists\epsilon_1=M\epsilon$，*对这个$\epsilon_1>0$，*$\exists\delta>0,\forall x:0<|x-x_0|<\delta, |f(x)-A|<\epsilon_1=M\epsilon$。

必要性。$\forall\epsilon>0,\exists\epsilon_2=\frac\epsilon M$，对这个$\epsilon_2>0，\exists\delta>0,\forall x:0<|x-x_0|<\delta, |f(x)-A|<M\epsilon_2=\epsilon$，于是$\lim\limits_{x\rightarrow x_0}f(x)=A$。

这样就把说不清楚的任意性的问题绕开了。

**例1.1**. 证明：连续周期函数若不是常值函数，则一定存在一个最小正周期。

本题是数学分析课上老师留的思考题，当时我自己想出了一种做法。后来查询网络，在两年后网络发布的一则视频里看到了一个类似的证明思路。要点仍然是连续性的定义以及其带来的如上性质。

实际上，我们需要想象在这个连续过程里发生了什么。即如果这个周期任意小，对于一个连续函数而言会发生什么。考虑下图：

![](./figs/M-1-1.png)

由于标称的两个点受到矩形的限制，其函数值的变化局限在了两个完全不相同的值附近。如果这时还要求一个太小的周期，显然左框挪动的步长太小，挪到右边一定会发生函数值不相等的矛盾。

基于以上思考，结合实数基本定理，我们可以写出如下的证明：

证明：考虑周期函数$f(x)$的正周期集合$S=\{T|T>0,f(x+T)-f(x)\equiv0\}$。

首先说明:$\exists\delta>0$，使得$\forall t\in (0,\delta),t\notin S$。

考虑$f(x)$上两点$(x_1,f(x_1)),(x_2,f(x_2))$，满足$x_1\neq x_2$，$f(x_1)\neq f(x_2)$。不妨$x_1<x_2$且$f(x_1)<f(x_2)$，因为若此时$f(x_1)>f(x_2)$，任意取一个$T_0\in S$，根据取整不等式$[x]\le x<[x]+1$有$x_1'=x_1+([\frac{x_2-x_1}{T_0}]+1)T_0>x_2$且$f(x_1')=f(x_1)>f(x_2)$，取$x_2,x_1'$为新的$x_1,x_2$代入证明即可。

考虑$\epsilon=\frac{f(x_2)-f(x_1)}{2}>0$，记$M=\frac{f(x_2)+f(x_1)}{2}$则$\exists\delta>0,\forall x\in(x_2-\delta,x_2+\delta),f(x)>f(x_2)-\epsilon=M$。

若$\exists \delta_0<\delta,\delta_0\in S$，考虑$x_1'=x_1+[\frac{x_2-x_1}{\delta_0}]{\delta_0}$，由$x-1<[x]\le x$可知$x_2-\delta<x_2-\delta_0<x_1'\le x_2$，于是$f(x_1)=f(x_1')>M$，矛盾。

因此$\delta>0$是$S$的一个正下界。由确界原理，可知$S$有下确界$\inf S\ge \delta>0$。下证$\inf S\in S$。

事实上，根据下确界的定义，若$\inf S\notin S$，则对上述$\delta>0$，$\exists t_1\in(\inf S,\inf S+\delta),t_1\in S; \exists t_2\in(\inf S,t_1), t_2\in S$。于是$0<t_1-t_2<\delta$，又$\forall x,f(x)=f(x+t_1)=f(x+t_1-t_2)$得$t_1-t_2\in S$，从而矛盾。

因此$\inf S\in S$是所求的最小正周期。

如果能用图像画出一个问题想要探究什么，数学证明便只需要将文字转化为数学语言描述即可。再举一个竞赛题改编的题目：

**例1.2** （第十三届全国大学生数学竞赛非数学类初赛T2改）已知数列$\{x_n\}$满足$x_1=8, x_n^2-2(x_n+1)x_{n+1}+15=0$，求证$\{x_n\}$极限存在并求极限。

首先考虑这个东西到底是什么。$x_{n+1}=\frac{x_n^2+15}{2(x_n+1)}$看上去像是个二次除以一次的式子，似乎暗含一个对勾函数。配个方，$x_{n+1}=\frac{(x_n+1)^2+14-2x_n}{2(x_n+1)}=\frac{x_n+1}2-1+\frac{8}{x_n+1}$，于是$\{x_n+1\}$满足简单函数递推关系，即$f(x)=\frac x2+\frac 8x,y_n=x_n+1,y_{n+1}=f(y_n)$。考虑对勾函数与$y=x$的图像（图中将$y$标成了$x$）：

![](./figs/M-1-2.png)

如上作图迭代，可以观察到$y_n$收敛到了函数的不动点（与$y=x$的交点）。从图像形态我们可以猜测两点：$y_n>4$，且单调递减，从而向这个方向发展证明即可。

证明：

$y_n$推导略。下证$y_n>4$且$y_n$单调递减：

1. $y_1>4$。对$y_k>4$，有$y_{k+1}=\frac {y_k}2+\frac8{y_k}\ge4$，又等号当且仅当$y_k=4$取到，于是$y_{k+1}>4$。

2. 考虑$y_{n+1}-y_n=\frac 8{y_n}-\frac{y_n}2$，当$y_n>4$时$\frac 8{y_n}<\frac{y_n}2$恒成立，于是$y_{n+1}<y_n$。

根据单调有界定理，$\{y_n\}$存在极限。对递推式两边取极限舍去负根可得$\lim\limits_{n\rightarrow\infty}y_n=4$，因此所求极限为$3$。

**例1.3** 已知$f(x)$在$x=0$处连续，$f(0)=0,\lim\limits_{x\rightarrow 0}\frac{f(2x)-f(x)}x=A$。证明$f(x)$在$x=0$处可导，并求$f'(0)$。

错误解答：$A=\lim\limits_{x\rightarrow 0}\frac{f(2x)-f(x)}x=\lim\limits_{x\rightarrow 0}\left[2\cdot\frac{f(2x)-f(0)}{2x}-\frac{f(x)-f(0)}x\right]=2f'(0)-f'(0)=f'(0)$

看似运用了导数定义，实则我们并没有证明$f$在$x=0$处可导，不能保证两项极限存在，这样使用定义是错误的。注意到以上步骤中并没有用到$f(x)$在$x=0$处连续的信息，我们需要利用这一条件。

证明：因为 $\lim\limits_{x\rightarrow 0}\frac{f(2x)-f(x)}x=A$，即$\forall \epsilon>0,\exists \delta>0,\forall x\in (-\delta,\delta):\left|\frac{f(2x)-f(x)}x-A\right|<\epsilon$，此时有$|f(2x)-f(x)-Ax|<\epsilon|x|$成立。

考虑$\frac x{2^k}\in(-\delta,\delta),k\in\N$，可得$|f(\frac x{2^{k-1}})-f(\frac x{2^k})-A\frac x{2^k}|<\frac \epsilon{2^k}|x|$

现在考虑$x>0$的情形，即$\frac {A-\epsilon}{2^k}x<f(\frac x{2^{k-1}})-f(\frac x{2^k})<\frac {A+\epsilon}{2^k}x$

自$k=1$累加到$n$，得$(1-\frac 1{2^n})(A-\epsilon) x<f(x)-f(\frac x{2^n})<(1-\frac 1{2^n})(A+\epsilon) x$

又$f(x)$在$x=0$处连续，对给定的$x$令$n\rightarrow\infty$，有$(A-\epsilon)x\le f(x)-f(0)\le(A+\epsilon)x$，再由$f(0)=0$得$A-\epsilon\le\frac{f(x)}x\le A+\epsilon$，可知$\lim\limits_{x\rightarrow0^+}\frac{f(x)}x=A$，于是$f_+'(0)=A$。

完全类似地可以证明$f_-'(0)=A$，所以$f'(0)=A$。

**例1.4** 设$f(x)$在$[a,+\infty)$可导且有无数个互异零点$\{x_n\}$，$f(x)$在其零点处导数不为零。证明：$\lim\limits_{n\rightarrow\infty}x_n=+\infty$。

分析：容易想见如果其无数个零点能挤在一起，似乎会引发问题。因此直接反证。

证明：假设$\{x_n\}$不是正无穷大，则必然存在一子列有上界。否则，取自然数集$\N$，对其每一项都能找到一个子列$\{x_{n_k}'\},k\in\N$，且$\{x_{n_k}'\}$中存在大于$k$的项，于是这些项构成了一个趋于正无穷大的子列，此时$\{x_n\}$是正无穷大。注意到$x_n\ge a$，则$\{x_n\}$有下界。

现在由致密性定理，$\{x_n\}$的给定子列存在收敛子列$\{x_{n_k}\}$，不妨设$\lim\limits_{k\rightarrow\infty}x_{n_k}=x_0$。

由于$f(x)$是连续的，则$f(x_0)=\lim\limits_{k\rightarrow\infty}f(x_{n_k})=0$。

因为$f'(x_0)\ne 0$，不妨$f'(x_0)>0$（另一边完全同理），则$\lim\limits_{x\rightarrow x_0}\frac{f(x)}{x-x_0}>0$，于是$\exists\delta>0,\forall x\in(x_0-\delta,x_0)\cup(x_0,x_0+\delta):\frac{f(x)}{x-x_0}>0$，这表明$f(x)\ne0$。

但是由于$\lim\limits_{k\rightarrow\infty}x_{n_k}=x_0$，而$x_{n_k}$互异，因此$k$充分大时必定$\exists k,x_{n_k}\in(x_0-\delta,x_0)\cup(x_0,x_0+\delta)$。于是产生矛盾。

综上，命题得证。

注：这里其实用到了极限的另一个理解：若数列中不存在项等于其收敛值，则必然存在无穷多项与收敛值任意近，证明可参考例1.1中关于$\inf S\in S$的证明。

疑问：仅由题目条件能否推出$\{x_n\}$可数无穷？（否则这个记号似乎不严格）

**例1.5** 已知$f(x)$在$[a,b]$上非负且连续，令$M=\max\limits_{x\in[a,b]}f(x)$，证明$\lim\limits_{n\rightarrow\infty}\left[\int_a^bf^n(x)\mathrm dx\right]^{\frac 1n}=M$

分析：本题事实上是想说明定积分值完全被$M$附近的值占据了，但是这件事似乎不太好说。为此，我们考虑最大值点附近的一个邻域，函数值均在$M$附近。

证明：显然$\left[\int_a^bf^n(x)\mathrm dx\right]^{\frac 1n}\le\left(\int_a^bM^n\mathrm dx\right)^\frac 1n=M(b-a)^\frac 1n$，下面考虑另外一边。

考虑$x_0=\argmax\limits_{x\in[a,b]}f(x)$，因为$f(x)$连续，于是$\forall \epsilon>0,\exists \delta^*>0:\forall x\in(x_0-\delta^*, x_0+\delta^*)\cap[a,b]\overset{def}{=}[\alpha,\beta],f(x)>M-\epsilon$。于是$\left[\int_a^bf^n(x)\mathrm dx\right]^{\frac 1n}\ge\left[\int_\alpha^\beta (M-\epsilon)^n\mathrm dx\right]^\frac 1n=(M-\epsilon)(\beta-\alpha)^\frac 1n$。

令$n\rightarrow\infty$，由夹逼定理知$M-\epsilon\le\lim\limits_{n\rightarrow\infty}\left[\int_a^bf^n(x)\mathrm dx\right]^{\frac 1n}\le M$

由$\epsilon$的任意性（参见开头命题2），即证。
