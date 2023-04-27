# Understanding and Computing the Hilbert Regularity
使用 Gröbner 基攻击 AOC 时，最相关的问题是：Gröbner 基计算有多复杂？ 一种常用的估计是基于多项式系统的正则度。 直观上，正则度是在 Gröbner 基计算期间出现的最高次数多项式的次数。 （这个指标是否适合评估 AOC 的安全性是另一回事。）

不幸的是，不同的作者对术语“规律性程度”的定义不同。 在这篇文章中，我使用了 Bardet 等人的理解。 [1,2]，这与定义明确的 Hilbert 正则性一致。

我首先介绍所需的概念，然后通过一些示例使它们更加具体。 最后，有一些代码可以用来计算希尔伯特正则性。

## 希尔伯特正则的定义

在有限域  $\mathbb{F}$ 上，$R=\mathbb{x_0,...,x_{n-1}}$ 是一个多项式环， $i\subseteq R$ 是一个多项式理想。

一个商环 $R/I$ 的仿射Hilbert 函数 定义为
$$
HF_{R/I}(s)=dim_F(R_{\le s}/I_{\le s})
$$

对于一些足够大的 $s_0$ ，Hilbert 函数对于 所有 $s\ge s_0$ 能表达成一个多项式变量为 $s$ 。这个多项式记为 $HP_{R/I}(s)$,称为Hilbert 多项式。

Hilbert 正则是最小的 $s_0$ ，使得所有的 $s\ge s_0$. $s$ 在Hilbert 函数上的评估 等价于 Hilbert 多项式在 $s$ 上的评估。

$$
HF_{R/I}(s)=dim_F(R_{\le s})-dim_F(I_{\le s})
$$

# 1 Introduction

## 

## 1.2 Our Contributions and Results

Paper Outline

#  Preliminaries

## Notations

## GB

## CICO Problem




