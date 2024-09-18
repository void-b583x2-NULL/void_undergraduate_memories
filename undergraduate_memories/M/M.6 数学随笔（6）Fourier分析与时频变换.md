# M.6 数学随笔（6）Fourier分析与时频变换

这个专题很久就想做了，因为本校本专业的信号与系统课程的教学质量实在不是一般的差。有两位老师的课很好，给过我莫大的帮助，但除开他们，我的信号处理相关知识几乎是自学b站的课程的。我也将b站课程的精华浓缩在了一份pdf里（已上传，见），但还是要单开一个专栏讲讲如何运用这些公式。

**例6.1** （1）（Bessel问题）求$\sum\limits_{n=1}^\infty\frac 1{n^2}$
（2）求$\sum\limits_{n=1}^\infty\frac 1{n^4}$。

分析：考虑$f(x)=x^2在[-\pi,\pi]$上的Fourier展开与Parseval等式。

解：（1）因为$x^2$是偶函数，于是$b_n=0$，则$f(x)=\frac {a_0}2+\sum\limits_{n=1}^\infty a_n\cos nx, -\pi\le x\le \pi$，其中$a_n=\frac 1\pi\int_{-\pi}^\pi x^2\cos nx \mathrm dx$，当$n=0$时$a_n=\frac 23\pi^2$，否则分部积分计算得$a_n=(-1)^n\frac 4{n^2}$。于是$f(x)=\frac{\pi^2}3+4\sum\limits_{n=1}^\infty \frac{(-1)^n}{n^2}\cos nx$。令$x=\pi$，即得$\pi^2=\frac{\pi^2}3+4\sum\limits_{n=1}^\infty\frac 1{n^2}$，解得$\sum\limits_{n=1}^\infty\frac 1{n^2}=\frac{\pi^2}6$。
（2）根据Parseval等式$\frac{a_0^2}2+\sum\limits_{n=1}^\infty(a_n^2+b_n^2)=\frac 1\pi\int_{-\pi}^\pi[f(x)]^2\mathrm dx$，有$\frac 29{\pi^4}+16\sum\limits_{n=1}^\infty\frac 1{n^4}=\frac 25\pi^4$，解得 $\sum\limits_{n=1}^\infty\frac 1{n^4}=\frac{\pi^4}{90}$

**例6.2** （Borwein积分）（1）已知$\int_{-\infty}^{+\infty}\frac{\sin x}{x}\cdot\frac{\sin \frac x3}{\frac x3}\mathrm dx$收敛到$A$，求$A$的值。
（2）试求出最小的$n$，使得$\int_{-\infty}^{+\infty}\prod\limits_{k=1}^n\frac{\sin \frac x{2k-1}}{\frac x{2k-1}}\mathrm dx< A$。

本例是3b1b专门做视频介绍过的问题，具有很典型的意义，也不失为一道出色的Fourier变换习题。

解：（1）定义$g_\tau(x)=\mathbf 1[|x|\le \frac \tau2]$为宽度为$\tau$关于y轴轴对称的矩形窗函数，则$Sa(t)=\frac{\sin t}{t}$的Fourier变换为$\pi g_2(\omega)$。根据尺度变换，得$Sa(\lambda t),\lambda>0$的Fourier变换为$\frac {\pi}\lambda g_2(\frac \omega \lambda)=\frac {\pi}\lambda\mathbf1 [\left|\frac\omega\lambda\right|\le1]=\frac {\pi}\lambda g_{2\lambda}(\omega)$
根据卷积定理$\mathcal F[f(t)g(t)]=\frac 1{2\pi}F(\mathrm j\omega)*G(\mathrm j\omega)$，得$\int_{-\infty}^{+\infty}\frac{\sin x}{x}\cdot\frac{\sin \frac x3}{\frac x3}\mathrm dx=\frac 1{2\pi}\cdot\pi g_2(\omega)*3\pi g_{\frac 23}(\omega)|_{\omega=0}$。

现在考虑右侧的矩形窗卷积。事实上，使用卷积定义，容易推得$f(t)*g_{2\tau}(t)=\int_{-\tau}^{\tau}f(x+t)\mathrm dx$。代入上式并令$t=0$，有$\int_{-\infty}^{+\infty}\frac{\sin x}{x}\cdot\frac{\sin \frac x3}{\frac x3}\mathrm dx=\frac 32\pi\int_{-\frac 13}^{\frac 13}\mathrm dx=\pi$。

（2）考虑函数列$f_1(x)=\pi g_2(\omega), f_n(x)=\frac {2n-1}2f_{n-1}(x)* g_{\frac2{2n-1}}(x)(n\ge 2)$，以下证明：若$f_n(x)=\pi$，则$|x|\le2-\sum\limits_{k=0}^{n-1}\frac 1{2k+1}$，否则$0\le f_n(x)<\pi$。

使用数学归纳法，$n=1$时结论成立。现在设$n=m\in\N$时结论仍然成立，考虑$m=n+1$时。

$f_{m+1}(x)=\frac {2m+1}2f_{m}(x)* g_{\frac2{2m+1}}(x)=\frac {2m+1}2\int_{-\frac 1{2m+1}}^{\frac 1{2m+1}}f(x+t)\mathrm dt\ge 0$。

当$|x|\le 2-\sum\limits_{k=0}^{m}\frac 1{2k+1}$时，$|x\pm t|\le |x| + \frac 1{2m+1}\le 2-\sum\limits_{k=0}^{m-1}\frac 1{2k+1}$，此时$f_m(x+t)=\pi$，于是$f_{m+1}(x)=\frac {2m+1}2\int_{-\frac 1{2m+1}}^{\frac 1{2m+1}}\pi\mathrm dt=\pi$；
当$x>2-\sum\limits_{k=0}^{m}\frac 1{2k+1}$时，$x+\frac 1{2m+1}>2-\sum\limits_{k=0}^{m-1}\frac 1{2k+1}$，在区间$\left(2-\sum\limits_{k=0}^{m-1}\frac 1{2k+1}, x+\frac 1{2m+1}\right]$上$f_m(x)<\pi$，于是$f_{m+1}(x)<\pi$；

完全类似地证明$x<-\left(2-\sum\limits_{k=0}^{m}\frac 1{2k+1}\right)$时，$f_{m+1}(x)<\pi$。

根据数学归纳法，命题得证。

根据（1）中的推导，有$\int_{-\infty}^{+\infty}\prod\limits_{k=1}^n\frac{\sin \frac x{2k-1}}{\frac x{2k-1}}\mathrm dx=f_n(0)$。当$n=8$时，$2-\sum\limits_{k=0}^{7}\frac 1{2k+1}<0$，此时$f_8(0)<\pi$。

注：这里的证明严谨地说明了矩形窗函数“越卷上底越短”的特点，且事实上减小的量与矩形窗的宽度不无关系。另外将这里的$\{\frac 1{2n-1}\}$换成任意正数列，证明依然成立。

**例6.3** 考虑方波信号$x(t)=\mathrm {sgn}(\sin2\pi f t)$，其中$f=10^6$。
（1）求该信号的Fourier变换
（2）将该信号通过理想低通滤波器后得到$1\mathrm{MHz}$的标准正弦波信号，求低通滤波器截止频率的最大值。

分析：来自真实的信号与系统课程答疑。本题只要熟悉公式和定义，细心计算，应当毫无难度。

解：（1）$f(t)$的周期$T=\frac1f = 10^{-6}\mathrm s$。考虑$f(t)$的复系数Fourier级数展开$f(t)=\sum\limits_{k=-\infty}^{\infty}F(\mathrm jk\Omega)\mathrm e^{\mathrm jk\Omega t}$，其中$\Omega=\frac {2\pi}T$。

令系数$F_k=F(\mathrm jk\Omega)$，则$f(t)$的Fourier变换$F(\mathrm j\omega)=2\pi\sum\limits_{k=-\infty}^{\infty}F_k\delta(\omega-k\Omega)$。

现在计算$F(\mathrm jk\Omega)=\frac 1T\int_{-\frac T2}^{\frac T2}f(t)\mathrm e^{-\mathrm jk\Omega t}\mathrm dt$。注意到$\int_{-\frac T2}^{0}f(t)\mathrm e^{-\mathrm jk\Omega t}\mathrm dt=-\int_0^{\frac T2}\mathrm e^{\mathrm jk\Omega t}\mathrm dt, \int_0^{\frac T2}f(t)\mathrm e^{-\mathrm jk\Omega t}\mathrm dt=\int_0^{\frac T2}\mathrm e^{-\mathrm jk\Omega t}\mathrm dt$，于是
$F(\mathrm jk\Omega)=-\frac{2\mathrm j}T\int_0^{\frac T2}\sin k\Omega t\mathrm dt=-\frac{\mathrm j}{k\Omega T}(1-\cos k\pi)=-\frac{2\mathrm j}{k\pi}\mathbf 1[k=2m+1],m\in \Z$

代入化简整理，有$F(\mathrm j\omega)=4\mathrm j\sum\limits_{k=0}^\infty\frac 1{2k+1}\{\delta[\omega+(2k+1)\Omega]-\delta[\omega-(2k+1)\Omega]\}$，其中$\Omega=2\pi\cdot10^6$

注 注意到$f(t)$为奇函数，也可以将其展开为三角形式的Fourier级数后利用正弦函数的变换对进行计算。

（2）注意到$F(\mathrm j\omega)$的频谱比$\Omega$高的最小值为$3\Omega$，因此为了保证经过低通滤波器后只留下$\Omega$的一倍，最大的截止频率即为$3\mathrm{MHz}$。

**例6.4** 一个线性时不变系统可以由微分方程$y''(t)+3y'(t)+2y(t)=x'(t)+3x(t)$描述，试求出$x(t)=\mathrm e^{-3t}\epsilon(t)$且系统初值$y(0^-)=1,y'(0^-)=2$时的全响应、零输入分量、零状态分量，并指出自由响应与强迫响应分量。

分析：提供时域解法与L变换两种解法。注意各个概念的定义。

解1（时域解法，比较麻烦）
$x'(t)=\mathrm e^{-3t}[\delta(t)-3\epsilon(t)]=\delta(t)-3\mathrm e^{-3t}\epsilon (t)$，等式右侧退化为$\delta(t)$。

首先考虑零输入响应，即$t>0$时。此时齐次微分方程$y''(t)+3y'(t)+2y(t)=0$的解系$y_{zi}(t)=C_1\mathrm e^{-t}+C_2\mathrm e^{-2t}$，又零输入时状态连续，代入解得$y_{zi}(t)=4\mathrm e^{-t}-3\mathrm{e}^{-2t}$。

再考虑零状态响应，由于冲激项仅可能在最高阶求导中获得，因此只有$y''_{zs}(t)$中有冲激项。对上式两端在$[0^-,0^+]$上积分，除了冲激项之外积分结果为零，于是得到$y'_{zs}(0^+)-y'_{zs}(0^-)=1$，解得$y'_{zs}(0^+)=1$。

在零状态下，$y_{zs}(0^+)=0,y'_{zs}(0^+)=1$，零状态响应在$0^+$处应当连续，且$0^+$时刻输入退化为零，因此响应的解符合齐次微分方程解$y_{zs}(t)=C_3\mathrm e^{-t}+C_4\mathrm e^{-2t}$的形式，（注：如果$0^+$后输入有别的形式，则应具体解对应的微分方程）于是代入$0^+$时刻的条件可得$y_{zs}(t)=\mathrm e^{-t}-\mathrm e^{-2t}$。

综上，$y(t)=y_{zi}(t)+y_{zs}(t)=5\mathrm e^{-t}-4\mathrm e^{-2t}$，以上均有$t\ge 0$。

自由响应为响应的通解项，此处同全响应；强迫响应为特解项，此处为零。

注 此即“冲激系数匹配法”。

解2（L变换求解）

考虑$\mathcal L[f'(t)]=sF(s)-f(0^-)$，对原方程两边进行Laplace变换，以下默认$t\ge 0$。

零状态方程：$s^2Y(s)+3sY(s)+2Y(s)=sX(s)+3X(s), X(s)=\frac 1{s+3}$，此即$Y_{zs}(s)=\frac {s+3}{s^2+3s+2}=\frac 1{s+1}-\frac 1{s+2}$，于是$y_{zs}(t)=\mathrm e^{-t}-\mathrm e^{-2t}$。

零输入方程：$\mathcal L[f''(t)]=s\mathcal L[F'(s)]-f'(0^-)=s^2F(s)-sf(0^-)-f'(0^-)$，化简方程得$0=[s^2Y(s)-s-2]+3[sY(s)-1]+2Y(s)=(s^2+3s+2)Y(s)-(s+5)$，于是$Y_{zi}(s)=\frac {s+5}{s^2+3s+2}=\frac 4{s+1}-\frac 3{s+2}$，从而$y_{zi}(t)=4\mathrm e^{-t}-3\mathrm{e}^{-2t}$。

其余与解法1相同。

使用L变换只需要代入求解即可，难度降低，操作简单。

**例6.5** 考虑某因果离散时间系统函数$H(z)=\frac {z+1}{(z+\frac 12)(z+\frac 13)}$，给定输入信号$x[n]=2$，求输出信号$y[n]$。

分析：本题初看起来比较难以下手，但由于输入信号未限定为因果信号，我们可以认为这个输入已经自无穷远的过去通入了相当长的时间，即给出一个输入后我们去无穷远的未来观测响应，因此问题转化为求系统的稳态响应。

解：设输入为$x^*[n]=2\epsilon[n]$，则其z变换$X(z)=\frac{2z}{z-1}$。

$Y(z)=X(z)H(z)=\frac {2z(z+1)}{(z-1)(z+\frac 12)(z+\frac 13)}=z\left(\frac {A}{z-1}+\frac  B{z+\frac 12}+\frac C{z+\frac 13}\right)$

注意到其后两项分别对应$B(-\frac 12)^n,C(-\frac 13)^n$的z变换，这两项在无穷远处衰减到零，因此只需要求稳态分量$A$。使用[M.4](./M.4%20数学随笔（4）积分计算与逼近.md)的方法可以计算出$A=2$，因此所求输出为$y[n]=2$。

**例6.6** 已知一信号$x(t)$的单边Laplace变换可以表示为$\sum\limits_{i=1}^N\frac {A_i}{s-p_i}$的形式，对其按周期$T$采样得离散信号$x[n]=f(nT)$，求其单边z变换。

分析：事实上直接使用定义即可。

解：$f(t)=\sum\limits_{i=1}^N{A_i}\mathrm e^{p_it}, x[n]=\sum\limits_{i=1}^N{A_i}\mathrm e^{p_inT}$，于是$X[z]=\sum\limits_{n=0}^\infty\sum\limits_{i=1}^N{A_i}\mathrm e^{p_inT}z^{-n}=\sum\limits_{i=1}^N\sum\limits_{n=0}^\infty{A_i}\mathrm (e^{p_iT}z^{-1})^n=\sum\limits_{i=1}^N\frac A{1-\mathrm e^{p_iT}z^{-1}}$

其实，信号与系统完全可以作为一门应用数学去学习、理解。个人认为只要概念掌握清楚，则不太应该存在什么过多的问题。