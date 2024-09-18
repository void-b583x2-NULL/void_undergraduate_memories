# M.4 数学随笔（4）积分计算与逼近

其实积分计算实在没有什么能讲的，无非是被积函数化为有理函数与有理函数化为部分分式之和。当然，积分计算是有技巧的，以下举几例说明。

在此之前，有如下几组关于二次根式的积分公式，希望在常用积分表之外专门记忆，能够简化许多运算量：$(a>0)$

$$
\begin{aligned}
\int \frac{\mathrm dx}{\sqrt{a^2-x^2}}&=\arcsin\frac xa+C\\
\int \frac{\mathrm dx}{\sqrt{x^2\pm a^2}}&=\ln\left|x+\sqrt{x^2\pm a^2}\right|+C \\
\int\sqrt{a^2-x^2}\mathrm dx &= \frac x2\sqrt{a^2-x^2}+\frac {a^2}2\arcsin\frac xa+C\\
\int\sqrt{x^2\pm a^2}\mathrm dx &= \frac x2\sqrt{x^2\pm a^2} \pm \frac {a^2}2\ln\left|x+\sqrt{x^2\pm a^2}\right|+C
\end{aligned}
$$

**例4.1** 计算积分$\int\frac{\sin^2x}{\cos^3x}\mathrm dx$。

解1 熟知三角万能公式，令$t=\tan\frac x2$，则$\sin x=\frac{2t}{1+t^2}, \cos x=\frac{1-t^2}{1+t^2}, x=2\arctan t, \mathrm dx=\frac 2{1+t^2}\mathrm dt$，则$\int\frac{\sin^2x}{\cos^3x}\mathrm dx=\int{\left(\frac{2t}{1+t^2}\right)}^2\cdot{\left(\frac{1+t^2}{1-t^2}\right)}^3\cdot\frac 2{1+t^2}\mathrm dt=\int\frac{8t^2}{(1-t^2)^3}\mathrm dt$，但这样进行有理函数分式分解计算量过大。

解2 注意到$\int\frac{\sin^2x}{\cos^3x}\mathrm dx=\int\frac{\sin^2x\cos x}{\cos^4x}\mathrm dx=\int\frac {\sin^2x}{(1-\sin^2x)^2}\mathrm d\sin x\overset{t=\sin x}{=}\int\frac{t^2}{(1-t^2)^2}\mathrm dt$

考虑$\frac{t^2}{(1-t^2)^2}=-\frac 14\left(\frac 1{1+t}+\frac 1{1-t}\right)+\frac 14\left[\frac 1{(1+t)^2}+\frac 1{(1-t)^2}\right]$

则

$$
\begin{aligned}
\int\frac{t^2}{(1-t^2)^2}\mathrm dt
&=-\frac 14\ln\frac {1+\sin x}{1-\sin x}+\frac 14\left(\frac 1{1-\sin x}
-\frac 1{1+\sin x}\right)+C\\
&=-\frac14\ln\left(\frac {1+\sin x}{\cos x}\right)^2+
\frac 14\cdot\frac{2\sin x}{1-\sin^2 x}+C\\
&=\frac 12\tan x\sec x-\frac 12\ln|\tan x+\sec x|+C
\end{aligned}
$$

注：有理函数拆解分式技巧。以下借助CASIO fx-991进行完成。

考虑$f(x)=\frac{P(x)}{Q(x)}=\frac A{x-p_i}+\frac{B}{(x-p_1)^2}+R(x)$，其中$P,Q$为关于$x$的整式，$R(x)$不含以$p_1$为极点的项。

事实上，考察函数$f^*(x)=f(x)(x-p_1)^2=\frac {P(x)}{Q(x)}(x-p_1)^2=A(x-p_1)+B+R(x)(x-p_1)^2$。虽然这个函数在$x=p_1$处没有定义，但补充定义$f^*(p_1)=B$后$p_1$事实上是$f^*$的一个可去间断点。利用这一特性，我们可以直接在计算器中输入$\frac {P(x)}{Q(x)}(x-p_1)^2$的代数形式，随后代入$x=p_1+\Delta x$（$\Delta x$是一个任意小量，因为分母为零时计算器会报错，同时注意太小的$\Delta x$会导致计算器精度出现问题从而结果出现问题），求得对应的系数$B$。

至于$A$呢？标准做法是考虑$[f^*(x)]'=A+[R'(x)(x-p_1)+2R(x)](x-p_1)$，代入$x=p_1$求得$B$。但是这样的做法过于麻烦，我们可以在计算器上直接输入$\left[\frac{P(x)}{Q(x)}-\frac B{(x-p_1)^2}\right](x-p_1)$后代入$x=p_1+\Delta x$计算即得$A$。

以本题为例，欲求得$\frac 1{1+t},\frac1{(1+t)^2}$的系数，可以在计算器中输入$\frac{x^2}{(1-x^2)^2}(1+x)^2$后代入$x=-1.0001$计算出其系数为$\frac 14$，然后输入$\left[\frac{x^2}{(1-x^2)^2}-\frac 14\cdot\frac 1{(1+x)^2}\right](1+x)$代入$x=-1.0001$可计算出系数为$-\frac14$。

//TODO：学习复变函数后考虑其与留数的联系

然而这种解法虽然是通性通法，构成了重要的有理函数积分法，其计算量仍然有些大了。本题的正解是使用分部积分。

解3 $\int\frac{\sin^2x}{\cos^3x}\mathrm dx=\int\tan^2x\sec x\mathrm dx=\int\tan x\mathrm d\sec x=\tan x\sec x-\int\sec x\mathrm d\tan x$

而$\int\sec x\mathrm d\tan x=\int\sec^3x\mathrm dx=\int\frac{\sin^2x+\cos^2x}{\cos^3x}\mathrm dx=\int\frac{\sin^2x}{\cos^3x}\mathrm dx+\int\sec x\mathrm dx$

于是记原积分为$I$，有$I=\tan x\sec x-(I+\int\sec x\mathrm dx)$，从而$I=\frac 12(\tan x\sec x-\ln|\tan x+ \sec x|)+C$。

分部积分法有时能有非常惊人的作用。下面再看一例：

**例4.2** 设 $f(x)$在$[0,1]$上导数连续，$f(0)+f(1)=0$。证明$|\int_0^1f(x)\mathrm dx|\le\frac 12\int_0^1|f'(x)|\mathrm dx$。

分析：使用分部积分凑出$f'(x)$是本题的精髓。

证明：$\int_0^1f(x)\mathrm dx=xf(x)|_0^1-\int_0^1x\mathrm df(x)=f(1)-\int_0^1xf'(x)\mathrm dx$

另一方面，$\int_0^1f(x)\mathrm dx=\int_1^0f(1-t)\mathrm d(1-t)=\int_0^1f(1-t)\mathrm dt$（此即区间再现公式）

于是$\int_0^1f(x)\mathrm dx=xf(1-x)|_0^1-\int_0^1x\mathrm df(1-x)=f(0)+\int_0^1xf'(1-x)\mathrm dx$

两式相加，有$2\int_0^1f(x)\mathrm dx=\int_0^1xf'(1-x)\mathrm dx-\int_0^1xf'(x)\mathrm dx$

现在考虑$\int_0^1xf'(1-x)\mathrm dx=\int_0^1(1-x)f'(x)\mathrm dx$，得$2\int_0^1f(x)\mathrm dx=\int_0^1(1-2x)f'(x)\mathrm dx$

在$[0,1]$上恒有$|1-2x|\le1$，于是

$|\int_0^1f(x)\mathrm dx|\le\frac 12\int_0^1|f'(x)|\mathrm dx$。

以下讨论一类题目，涉及定积分值的估计，一般使用区间分点累加进行逼近。通过不同的题目我们将能看到，这个估计与真实值的差距往往是可控的。

**例4.3** $f(x)$在$[a,b]$上二阶导数连续，证明$\lim\limits_{n\rightarrow\infty} n^2[\int_a^bf(x)\mathrm dx-\frac{b-a}n\sum\limits_{k=1}^nf\left(a+\frac {2k-1}{2n}(b-a)\right)]=\frac {(b-a)^2}{24}[f'(b)-f'(a)]$

分析：本题结论指出使用区间中点的估计与真实值的差距仅仅是一个关于区间个数的二阶无穷小量。解答本题需要较强的分析学知识，关系到定积分的定义。

证明：记$x_k=a+\frac kn(b-a), 0\le k\le n$，这$n+1$个点将$[a,b]$分成了$n$个区间，再令$\xi_k=a+\frac {2k-1}{2n}(b-a)\in (x_{k-1},x_k)$，于是$B_n=\int_a^bf(x)\mathrm dx-\frac{b-a}n\sum\limits_{k=1}^nf\left(a+\frac {2k-1}{2n}(b-a)\right)=\sum\limits_{k=1}^n\int_{x_{k-1}}^{x_k}\left[f(x)-f(\xi_k)\right]\mathrm dx$

现在将$f(x)$在$\xi_k$处展开成Taylor公式$f(x)=f(\xi_k)+f'(\xi_k)(x-\xi_k)+\frac{f''(\eta_k)}2(x-\xi_k)^2$，$\eta_k$介于$x,\xi_k$之间，则上式化为$\sum\limits_{k=1}^n\int_{x_{k-1}}^{x_k}\left[f'(\xi_k)(x-\xi_k)+\frac{f''(\eta_k)}2(x-\xi_k)^2\right]\mathrm dx$

上式中第一项，由于在每个区间上$x-\xi_k\in[-\frac{b-a}{2n},\frac{b-a}{2n}]$，积分结果为$0$。现在考虑第二项。不妨设$f''(\eta_k)$在区间$[x_{k-1},x_k]$上的最大最小值分别为$M_k,m_k$，结合此时$\int_{x_{k-1}}^{x_k}(x-\xi_k)^2\mathrm dx=\int_{-\frac{b-a}{2n}}^{\frac{b-a}{2n}}x^2\mathrm dx=\frac{(b-a)^3}{12n^3}$，得到

$
\frac{(b-a)^3}{24n^3}\sum\limits_{k=1}^nm_k\le B_n \le 
\frac{(b-a)^3}{24n^3}\sum\limits_{k=1}^nM_k\\
\frac{(b-a)^2}{24}\cdot\frac{b-a}n\sum\limits_{k=1}^nm_k\le n^2B_n \le 
\frac{(b-a)^2}{24}\cdot\frac{b-a}n\sum\limits_{k=1}^nM_k
$

注意到$f''(x)$连续，从而可积。事实上，在每个小区间上总存在介点$\epsilon_k,\zeta_k,f(\zeta_k)=M_k,f(\epsilon_k)=m_k$，符合定积分的定义。令$n\rightarrow\infty$并考虑夹逼定理，即有$\lim\limits_{n\rightarrow\infty}n^2B_n=\frac{(b-a)^2}{24}\int_a^bf''(x)\mathrm dx=\frac {(b-a)^2}{24}[f'(b)-f'(a)]$，得证。

注：上式正符合在分划$\pi$由$\{x_k\}$给出时的Darboux上和与下和，但虽然很显然，并没有定理保证可积函数的Darboux上下和收敛于其定积分值，本题函数是连续的，可以规避掉这个问题。

**例4.4** 已知$[0,\pi]$上的连续函数$f(x)$，试求$\lim\limits_{n\rightarrow\infty} \int_0^\pi f(x)|\sin nx|\mathrm dx$。

分析：$f(x)$连续时可以使用积分中值定理，使用由$\{\frac {k\pi} n\}$构成的划分。

证明：令$x_k=\frac {k\pi}n,0\le k\le n$将$[0,\pi]$划分为$k$等分，在区间$I_k=[x_{k-1},x_k]$上$\exists \xi_k\in I_k$，$\int_{x_{k-1}}^{x_k}f(x)|\sin nx|\mathrm dx=f(\xi_k)\int_{x_{k-1}}^{x_k}|\sin nx|\mathrm dx$

在$I_k$上，$\int_{x_{k-1}}^{x_k}|\sin nx|\mathrm dx=\frac 2n$，于是对于给定的划分$\pi=\{\frac {k\pi} n\}$，$\int_0^\pi f(x)\mathrm dx=\lim\limits_{n\rightarrow\infty}\sum\limits_{k=1}^nf(\xi_k)\frac \pi n$，于是$\lim\limits_{n\rightarrow\infty} \int_0^\pi f(x)|\sin nx|\mathrm dx=\lim\limits_{n\rightarrow\infty}\sum\limits_{k=1}^nf(x_k)\frac 2n=\frac 2\pi\int_0^\pi f(x)\mathrm dx$

注：如果将$f(x)$放宽为可积函数，将乘积拓广为任意周期函数，将区间拓广为任意区间，将得到Riemann引理。该引理证明复杂，可自行查阅相关资料。

**例4.5** 已知$f(x)$在$[0,1]$上可导，$f(0)=f(1),\int_0^1f(x)\mathrm dx=0$且$f'(x)\ne 1$。求证：$\forall n\in\N, \left|\sum\limits_{k=0}^{n-1}f(\frac kn)\right|< \frac12$

分析：仍然是熟悉的区间点求和估计，但这里$n$不再趋于无穷。本题的精髓是构造函数使之为单调函数，从而单调函数的区间单侧点累加与积分值必然存在严格大小关系。

证明：根据Darboux定理，导函数具有介值性，因此$f'(x)<1$。构造$g(x)=f(x)-x$，则$\int_0^1g(x)\mathrm dx=-\frac 12$，且$g'(x)<0$，故$g(x)$严格单调递减。由于$\sum\limits_{k=0}^{n-1}f(\frac kn)=\sum\limits_{k=0}^{n-1}g(\frac kn)+\frac{n-1}2$，考虑$\sum\limits_{k=0}^{n-1}g(\frac kn)$的估计。

因为在区间$(\frac {k-1}n,\frac kn]$上，$g(x)<g(\frac {k-1}n)$，所以$\frac 1n\sum\limits_{k=0}^{n-1}g(\frac kn) > \int_0^1g(x)\mathrm dx = -\frac 12$。又因为在$[\frac{k-1}n,\frac kn)$上$g(x)>g(\frac kn)$，于是$\frac 1n\sum\limits_{k=1}^{n}g(\frac kn) < \int_0^1g(x)\mathrm dx = -\frac 12$。注意到$\frac 1n\sum\limits_{k=1}^{n}g(\frac kn) = \frac 1n\sum\limits_{k=0}^{n-1}g(\frac kn)+\frac 1n[g(1)-g(0)]=\frac 1n\sum\limits_{k=0}^{n-1}g(\frac kn) + \frac 1n$，从而$-\frac 12< \frac 1n\sum\limits_{k=0}^{n-1}g(\frac kn)< \frac 1n -\frac 12$。

整理相加，可得$\sum\limits_{k=0}^{n-1}f(\frac kn)\in(-\frac 12,\frac12)$，即证。

注：函数$f(x)$在$I$上严格单调递增（或递减）的充要条件是：
（1）$f'(x)\ge 0 (f'(x)\le0),x\in I$；
（2）$\forall [\alpha,\beta] \subset I, f(x)$不恒为$0$。
因此$f'(x)<0,\forall x\in I$可以推得$f(x)$在$I$上严格单调递减，但反之不然。