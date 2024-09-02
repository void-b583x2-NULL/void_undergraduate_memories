# M.2 数学随笔（2）等价无穷小与未定式求解

这期专栏想简单聊聊未定式极限求解。很多人喜欢无脑L‘Hospital（中译洛必达）或者Taylor展开至某一阶之后展开暴算，但很多时候这样的努力会化简为繁。

未定式处理的核心，其实是比较分子分母的阶。因为这种未定总是体现在分子分母存在同阶的项恰好能够抵消，需要计算的便是剩下的余项。因此，熟练使用等价无穷小往往能解决非常多的问题。毕竟，等价无穷小在形式上是Taylor公式的低阶展开，不需要那么多繁杂的计算。

举个简单的例子。

例2.1 计算极限$\lim\limits_{x\rightarrow0}\frac{(1+x)^{\frac1x}-\mathrm e}{x}$

这道题据说经常作为钓鱼题出现。我们考虑一下问题的本质，实际上就是分子的常数项$\mathrm e$消掉了，欲计算关于$x$一阶小量的系数。了解了这一点之后，解题就会变得十分简单。

解：考虑$(1+x)^{\frac 1x}-\mathrm e = \mathrm e[\frac{\ln(1+x)}x-1]=\mathrm e\cdot\frac {x-\frac {x^2}2+o(x^2)-x}x$，于是

$\lim\limits_{x\rightarrow0}\frac{(1+x)^{\frac1x}-\mathrm e}{x}=\mathrm e\cdot\frac {x-\frac {x^2}2+o(x^2)-x}{x^2}=-\frac {\mathrm e}2$

例2.2 计算极限$\lim\limits_{x\rightarrow0}\frac{(1+x)^{\frac 1{x^2}}}{\mathrm e^{\frac 1x}}$

解1：考虑$L = \frac{\ln (1+x)}{x^2}-\frac 1x = \frac 1{x^2}[x-\frac {x^2}2+o(x^2)-x]=-\frac 12+o(1)$

于是$\lim\limits_{x\rightarrow0}\frac{(1+x)^{\frac 1{x^2}}}{\mathrm e^{\frac 1x}}=\lim\limits_{x\rightarrow0}\exp (L)=\mathrm e^{-\frac 12}$

解2：使用$\ln x\sim x-1(x\rightarrow 1)$，于是$a^b=\mathrm e^{b\ln a}\sim\mathrm e^{b(a-1)}(a\rightarrow1)$

$\lim\limits_{x\rightarrow0}\frac{(1+x)^{\frac 1{x^2}}}{\mathrm e^{\frac 1x}}=\lim\limits_{x\rightarrow0}\left[\frac{(1+x)^{\frac 1{x}}}{\mathrm e}\right]^{\frac 1x}=\exp\{{\lim\limits_{x\rightarrow 0}}\frac 1x[\frac{(1+x)^{\frac 1x}}{\mathrm e}-\mathrm 1]\}=\mathrm e^{-\frac 12}$

最后一步使用上题结论。

以上两个问题如果直接使用L‘Hospital法则处理是很有可能真要进Hospital的。固然这里是容易想到使用指对互换作为非常常用的技巧的。

例2.3 计算$\lim\limits_{x\rightarrow0}\frac{\cos(\sin x)-\cos x}{x^4}$。

此题不论是直接使用L'Hospital还是Taylor展开都会极其繁琐。相反，使用等价无穷小反而能够很快得到答案。关键在于第一步的变形。

解：熟知和差化积公式$\cos A-\cos B=-2\sin\frac{A+B}2\sin\frac{A-B}2$，得

$$
\begin{aligned}
\lim\limits_{x\rightarrow0}\frac{\cos(\sin x)-\cos x}{x^4}&=-\lim\limits_{x\rightarrow0}\frac2{x^4}\sin\frac{\sin x+x}2\sin\frac{\sin x-x}2\\
&=-\lim\limits_{x\rightarrow0}\frac2{x^4}\cdot\frac{\sin x+x}2\cdot\frac{\sin x-x}2\\
&=-\frac 12\lim\limits_{x\rightarrow0}\frac{\sin x+x}x\cdot\lim\limits_{x\rightarrow0}\frac{\sin x-x}{x^3}\\
&=-\frac 12\lim\limits_{x\rightarrow0}\frac{x+o(x)+x}x\cdot\lim\limits_{x\rightarrow0}\frac{x-\frac 16x^3-x+o(x^3)}{x^3}\\
&=\frac 12\cdot 2\cdot \frac16\\
&=\frac 16
\end{aligned}
$$

L'Hospital法则有一个离散形式，即所谓的Stolz定理，针对的对象是离散序列。具体地，若单调递增数列$\{b_n\}\rightarrow +\infty(n\rightarrow \infty)$，且关于数列$\{a_n\}$的极限$\lim\limits_{n\rightarrow \infty}\frac{a_n-a_{n-1}}{b_n-b_{n-1}}=A$，则$\lim\limits_{n\rightarrow \infty}\frac{a_n}{b_n}=A$。其证明比L’Hospital法则复杂很多，但如果将分子分母视作相应数列的差分，则其与L‘Hospital法则的分子分母同时微分是可以类比的。

例2.4 考虑数列$\{x_n\}:x_1=1,x_{n+1}=\sin x_n$，求$\lim\limits_{n\rightarrow\infty}nx_n^2$。

解：注意到$x_n>0$且$\sin x<x (x>0)$，于是数列$\{x_n\}$单调递减且有下界，极限存在。令$n\rightarrow \infty$，可得$\lim\limits_{n\rightarrow\infty}x_n=0$，从而$\frac1{x_n^2}\rightarrow\infty(n\rightarrow\infty)$，且严格递增，符合使用Stolz定理的条件。

考虑$\frac1{x_n^2}-\frac 1{x_{n-1}^2}=\frac1{\sin^2x_{n-1}^2}-\frac 1{x_{n-1}^2}$。记$x_{n-1}=x$，则

$$
\begin{aligned}
\frac1{\sin^2x^2}-\frac 1{x^2}&=
\left(\frac 1{\sin x}-\frac 1x\right)\left(\frac 1{\sin x}+\frac 1x\right)\\
&=\frac {x-\sin x}{x\sin x}\cdot \frac {x+\sin x}{x\sin x}\\
&\sim \frac {x-\sin x}{x^3}\cdot \frac {x+\sin x}{x} \\
&= \frac 13 (x\rightarrow 0)
\end{aligned}
$$

于是$\lim\limits_{n\rightarrow\infty}\frac{n-(n-1)}{\frac1{x_n^2}-\frac 1{x_{n-1}^2}}=3$，由Stolz定理得所求极限为3。

未定式的求解本质上还是先看分子分母的阶，确定大概会变成什么样子，然后使用对应的路数求解。最关键的，复杂的式子一定要记得变形在先。






















