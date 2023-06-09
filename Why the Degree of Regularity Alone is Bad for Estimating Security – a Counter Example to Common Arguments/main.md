# Why the Degree of Regularity Alone is Bad for Estimating Security – a Counter Example to Common Arguments 为什么单凭规律性程度不利于安全性评估——常见论点的反例


设计为代数简单的密码原语——AOC——可能特别容易受到代数攻击。 此类中最具威胁的攻击向量之一是 Gröbner 基分析。 对于被认为是安全的密码或哈希函数，从原语派生的任何多项式系统的 Gröbner 基础需要难以计算。

不幸的是，在计算完成之前，通常不知道为特定多项式系统计算 Gröbner 基的复杂性。 但是，存在一些复杂性界限。 最常用的界限之一是基于多项式系统的正则 degree。

通常，计算多项式系统的正则 degree与计算 Gröbner 基本身一样困难。 幸运的是，对于“平均”正则确定系统，正则degree等于 **麦考利界限**。

对于 $\mathcal{F}=\{f_0,...,f_{s-1}\}\subset \mathbb{F}[x_0,...,x_{n-1}]$ 有 $d_{reg}=1+\sum_{i=0}^{s-1}deg(f_i)-1$

## 当前的 AOC 如何论证对 Gröbner 基分析的抵制

Poseidon [6] 论文中提到了 Macaulay 界，并隐含地假设由 Poseidon 产生的多项式系统是一个正则序列。 我自己的实验表明这个假设是错误的。 类似地，GMiMC [1] 使用 Macaulay 界限并隐含地假设系统的规律性。 我自己的实验表明这个假设也是错误的。 Ciminion [4] 的作者明确假设派生系统是规则的，但错误地将其描述为“最佳对抗场景”，而事实恰恰相反。 此外，我自己的实验表明多项式序列是不规则的。 对于 Rescue [2]，作者对轮数减少的变体执行 Gröbner 基础攻击，表明 Rescue 产生的系统是不规则的。 然后他们推断观察到的度数来估计整轮基元的规律性程度。

总之，可以观察到两种方法：
1. 假定系统的正则性，然后使用 Macaulay 界限来计算正则 degree，
2. 从舍入减少的变体中推断规律性程度。 然后，这两种方法都使用正则 degree来估计计算 Gröbner 基的复杂性。 这通常是通过查看最有效的 Gröbner 基算法 F5 的复杂性边界来完成的。 这个界限是

$$
O\left(\binom{n + d_\text{reg}}{n}^\omega\right)
$$

其中 $n$ 是多项式的变量个数，但是得到的复杂度是上界而不是下界

## 正则degree 是不充分的
我将举出一系列越来越复杂和越来越不正常的例子，说明**从麦考利界得出的正则 degree不足以准确估计计算 Gröbner 基的具体复杂性**。 以下所有系统的理想都是维度 0 ，这意味着相应的公共解决方案集是非空的并且包含有限多个元素。 这准确地反映了对加密原语建模的多项式系统的属性。

### 系统已经是GB
我们想要计算 $\mathcal{F}_{gb}=\{x^7,y^7,z^7\}\subset \mathbb{F}[x,y,z]$ 。
$\mathcal{F}$ 是一个正则序列，那么其正则degree为 
$$
d_{reg}=1+\sum_{i=0}^2(7-1)=19
$$
因此，或者上面粗略的论点是这样的，像 F4 或 F5 这样的 Gröbner 基算法应该必须在能够输出 Gröbner 基之前对最多 19 次的多项式执行计算。

然而 ，$\mathcal{F}$ 已经是GB了，不需要再进行计算。

### 系统可以拆分

从密码原语导出多项式系统很少会给你一个 Gröbner 基——尽管也有例外，比如 GMiMC。 相反，让我们看看下面的多项式系统。

$$
\mathcal{F}_\text{indep} = \left\{\begin{aligned}  &u^2 v   w   + u^2,     && x^2 y   z   + x^2,\\   &u   v^2 w   + v^2 + 1, && x   y^2 z   + y^2 + 1,\\   &u   v   w^2 + w^2,     && x   y   z^2 + z^2\\ \end{aligned}\right\} \subseteq \mathbb{F}[u,v,w,x,y,z].
$$

其中变量 $u,v,w$ 所在的多项式和 $x,y,z$ 所在的多项式 是独立的。那么系统的麦考利边界，这个事实是无关紧要的。
因为 $\mathcal{F}_\text{indep}$ 是一个正则系统，那么我们根据麦考利边界计算出其正则degree
$$
d_\text{reg} = 1 + \sum_{i=0}^5 4 – 1 = 19
$$
然而，magma 和 FGb 的 F4 实现以及 F5 的 python 实现在找到 Gröbner 基之前只计算 5 次或更低的多项式——他们没有被这种人为增加复杂性的尝试所愚弄。
### 换个系统

对之前的多项式系统进行一些调整 
$$
\mathcal{F}_\text{invlv} = \left\{ \begin{aligned}    &u^2 v   w   + u^2,     && x^2 y   z   + x^2,\\    &u   v^2 w   + v^2 + 1, && x   y^2 z   + y^2 + 1,\\    &u   v   w^2 + w^2,     && u^4 + z^4\\  \end{aligned}  \right\} \subseteq \mathbb{F}[u,v,w,x,y,z].
$$

两个多项式系统不同在最后一个多项式 $(u^4+z^4)$ 连接两个独立的子系统。  

两个多项式系统的 **Macaulay bound** 都是 $d_{reg}=19$

你现在可能已经猜到了：在 $\mathcal{F}_{invlv}$ 的 Gröbner 基计算中出现的最高多项式不是 $19$。Magma 的 $F_4$ 报告最大次数为 $6$，$FGb$ 仅达到 $5$，python-$F_5$ 也是如此。

我将多项式系统描述为一次可以从几个输入多项式计算 Gröbner 基元素的多项式系统具有低“参与度”。 到目前为止，还没有数学上严格的方法来定义这个概念，但上面的例子应该给出一个粗略的直觉。 我的观察表明，低参与意味着计算 Gröbner 基的复杂性低。

笔记。 以上反例并没有反驳一般多项式系统的正则性程度与麦考利界的相等性——它们只是表明序列的正则性不是充分要求。