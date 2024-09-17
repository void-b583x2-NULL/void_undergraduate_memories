# M.6 数学随笔（6）Fourier级数与时频变换

这个专题很久就想做了，因为本校本专业的信号与系统课程的教学质量实在不是一般的差。有两位老师的课很好，给过我莫大的帮助，但除开他们，我的信号处理相关知识几乎是自学b站的课程的。我也将b站课程的精华浓缩在了一份pdf里（已上传，见），但还是要单开一个专栏讲讲如何运用这些公式。

例6.1 （1）（Bessel问题）求$\sum\limits_{n=1}^\infty\frac 1{n^2}$
（2）求$\sum\limits_{n=1}^\infty\frac 1{n^4}$。

例6.2 （Borwein积分）（1）已知$\int_{-\infty}^{+\infty}\frac{\sin x}{x}\cdot\frac{\sin 3x}{3x}\cdot \frac{\sin 5x}{5x}\mathrm dx$收敛到$A$，求$A$的值。
（2）试求出最小的$n$，使得$\int_{-\infty}^{+\infty}\prod\limits_{k=1}^n\frac{\sin (2k-1)x}{(2k-1)x}\mathrm dx< A$。

例6.3 考虑方波信号$x(t)=\mathrm {sgn}(\sin2\pi\Omega t)$，其中$\Omega=10^6$。
（1）求该信号的Fourier变换
（2）将该信号通过理想低通滤波器后得到$1\mathrm{MHz}$的标准正弦波信号，求低通滤波器截止频率的最大值。

（未完待续）