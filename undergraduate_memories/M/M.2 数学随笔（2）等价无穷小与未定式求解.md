# M.2 数学随笔（2）等价无穷小与未定式求解

这期专栏想简单聊聊未定式极限求解。很多人喜欢无脑L‘Hospital（中译洛必达）或者Taylor展开至某一阶之后展开暴算，但很多时候这样的努力会化简为繁。

未定式处理的核心，其实是比较分子分母的阶。因为这种未定总是体现在分子分母存在同阶的项恰好能够抵消，需要计算的便是剩下的余项。因此，熟练使用等价无穷小往往能解决非常多的问题。毕竟，等价无穷小的本质是一阶Taylor展开，不需要那么多繁杂的计算。

举个简单的例子。

例2.1 计算极限$\lim\limits_{x\rightarrow0}\frac{(1+x)^{\frac1x}-\mathrm e}{x}$

这道题据说经常作为钓鱼题出现。我们考虑一下问题的本质，实际上就是分子的常数项$\mathrm e$消掉了，欲计算关于$x$一阶小量的系数。了解了这一点之后，解题就会变得十分简单。

解：考虑$(1+x)^{\frac 1x}-\mathrm e = \mathrm e[\frac{\ln(1+x)}x-1]=\mathrm e\cdot\frac {x-\frac {x^2}2+o(x^2)-x}x$，于是

$\lim\limits_{x\rightarrow0}\frac{(1+x)^{\frac1x}-\mathrm e}{x}=\mathrm e\cdot\frac {x-\frac {x^2}2+o(x^2)-x}{x^2}=-\frac {\mathrm e}2$

（未完待续）


