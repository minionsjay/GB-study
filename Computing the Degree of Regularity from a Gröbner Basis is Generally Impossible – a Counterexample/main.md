# Computing the Degree of Regularity from a Gröbner Basis is Generally Impossible – a Counterexample

计算生成零维理想的 正则序列 的 正则degree很容易——
**麦考利界**就是我们正在寻找的答案。 如果多项式系统不满足这些条件，问题就稍微复杂一些。 具体来说：*计算多项式系统的正则 degree 通常与计算其 Gröbner 基一样困难。*

这可能表明从 Gröbner 基计算 正则degree 很容易。 毕竟，我们已经完成了所有艰苦的工作！ 不幸的是，通常情况并非如此，下面的示例将说明这一点。

在这篇博文中，我将交替使用“正则degree”和“计算 Gröbner 基时达到的最高程度”。 虽然这在一般情况下并非如此，但度数足够接近，足以让下面的论点仍然有效。

考虑一个多项式系统 $\mathcal{F}=\{x^2y+1,xy^2\}\subset \mathbb{F}[x,y]$ ，我们使用 Buchberger 算法定义在 degrevlex 上计算 GB
$$
S-Poly(x^2y+1,xy^2)=\frac{x^2y^2}{x^2y}\cdot (x^2y+1)-\frac{x^2y^2}{x^2y}\cdot xy^2=y
$$
保持跟踪，我们计算了一个 4 次多项式，即使最高次的单项式没有进入最终结果。 更进一步，我们找到了 Gröbner 基础：

$$
\text{S-Poly}(x^2y + 1, y) = \frac{x^2y}{x^2y}\cdot (x^2y + 1) – \frac{x^2y}{y}\cdot y = x^2y + 1 – x^2y = 1.
$$

似乎 $\mathcal{F}$ 是不一致的，约简后的 Gröbner 变为 $\{1\}$ ，这意味着 $<\mathcal{F}>$ 的零点是空集。
很高兴知道。 $\mathcal{F}$ 的正则degree为 4，在计算第一个 S-多项式时达到。


已经很明显，从这个 Gröbner 基计算正则 degree是不可能的。假设多项式系统为 $\mathcal{F}_a=\{x^ay+1,xy^a\}$ ，$a$ 为正整数。那么对其计算 约简的GB为 $\{1\}$。然而，在计算所述 Gröbner 基时出现的最高阶多项式的次数——无论是使用 Buchberger 算法、F4、F5 还是 Mutant XL——是 $2a$

识别可以很容易地从其 Gröbner 基推导出正则 degree 的多项式系统的类别是一个有趣的问题。 一致性系统是这样的一个类吗？ 跨越零维理想的一致系统？ 系统的规律性是否起作用？ 上面的例子只是表明一般情况下是不可能的。

