---
title: 'Combinatory Logics'
---

1. 所有的变量，常量，以及组合子 $I$, $K$, $S$ 都是合法的 $CL$ 项
2. 如果 $X$ 和 $Y$ 是合法的 $CL$ 项，那么 $XY$ 也是
例如，以下字符串都是合法的 $CL$ 项 $((S(K S)) K)$, $\left(\left(S\left(K\right)\right)((S K) K)\right)$

### Weak Reduction

- $IX$ 可以变换为 $X$
- $KXY$ 可以变换为 $X$
- $SXYZ$ 可以变换为 $(XZ)(YZ)$

例如计算 $S(K S) K X Y Z$
$$
\begin{aligned}
S(K S) K X Y Z &= (K S K) (K X) Y Z \\
               &= S (K X) Y Z \\
               &= (K X Z) (Y Z) \\
               &= X (Y Z)
\end{aligned}
$$

与 $\lambda$ 项的 $\beta$ 范式一样，我们将不能再继续进行 weak reduction 的 $CL$ 项称为 :span[weak 范式(weak normal form)]{.definition}

### $CL$ 的计算能力与 $\lambda$ 演算相当

以上我们看到 $CL$ 项，似乎只能进行项的应用 (application) 操作，对应于 $\lambda$ 项的用法为 $(MN)$，然而 $CL$ 的计算能力与 $\lambda$ 演算相当。$\lambda$ 中的 abstraction 可以通过 组合子 $I$, $K$, $S$ 表示

考虑 $\lambda$ 演算的 abstraction，具体有几种情况
- $\lambda x . x$ 则等价于 $I$
- $\lambda x . M$ 如果 $M$ 中不含 $x$，则等价于 $K M$
- $\lambda x . U x$ 则等价于 U (就是 eta-conversion)
- 在上述三种情况外，一定形如 $\lambda x . U V$，则等价于 $S (\lambda . U) (\lambda . V)$
-- 在 $\lambda$ 演算中，当我们做 application 的时候，我们对 function body 做 substitution 也就是 beta-reduction；也就是说如果我们的项将对某个变量 $x$ 做 substitution，我们可以将其写成 function application 的形式。所以在这里 $U$ 被改写为了 $(\lambda . U)$

例如 $[x] . x y=S([x] . x)([x] . y)=S I(K y)$