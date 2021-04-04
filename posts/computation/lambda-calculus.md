---
title: Computation | Lambda Calculus
---

- bound var: a var that's associated with some `λ`
- free var: a var not associated with any `λ
直观上来说，如果 `x` is bound 则 `x` 在一个左边为 `x` 的 `λ` 的子树

A closed term is one in which all identifiers are bound.

---

In the pure lambda calculus, any abstraction is a value. Remember, an abstraction `λx. e` is a function; in the pure lambda calculus, the only values are functions. 

In an applied lambda calculus with integers and arithmetic operations, values also include integers. Intuitively, a value is an expression that can not be reduced/executed/simplified any further.

---

### substitution

**α-equivalence**: we can change the name of bound variables without changing the meaning of functions. \
Thus `λx. x` is the same function as `y. y`

Expressions e1 and e2 that differ only in the name of bound variables are called α-equivalent ("alpha equivalent"), sometimes written `e1 =α e2`.

---

**β-equivalence**: We write `e1{e2/x}` to mean expression `e1` with all free occurrences of `x` replaced with `e2`.

```
((λx.λy.x)y)z
        ->  ((λy.x)[y/x])z   // substitute y for x in the body of "λy.x"
        ->  ((λy'.x)[y/x])z  // after alpha reduction
        ->  (λy'.y)z         // first beta-reduction complete!
        ->  y[z/y']          // substitute z for y' in "y"
        ->  y                // second beta-reduction complete!
```

we call ((λx.λy.x)y)z and y are beta-equivalent

Note that the term "beta-*reduction*" is perhaps misleading, since doing beta-reduction does not always produce a smaller lambda expression. In fact, a beta-reduction can:
- not change: `(λx.xx)(λx.xx) → (λx.xx)(λx.xx)`
- increase: `(λx.xxx)(λx.xxx) → (λx.xxx)(λx.xxx)(λx.xxx) → (λx.xxx)(λx.xxx)(λx.xxx)(λx.xxx)`
- decrease: `(λx.xx)(λa.λb.bbb) → (λa.λb.bbb)(λa.λb.bbb) → λb.bbb`

### normal form 

We say that a lambda expression without redexes (applications of a function to an argument) is in **normal form**, and that a lambda expression **has** a normal form iff there is some sequence of beta-reductions and/or expansions that leads to a normal form.


`(λx.λy.y)((λz.zz)(λz.zz))`. This lambda expression contains two redexes:
- the whole expression
- the argument itself: `((λz.zz)(λz.zz))`
如果我们先对 argument 做 beta reduction 则永远不会得到 norm form 但是如果先对第一个 redex 做则可以

**leftmost-outermost** or **normal-order-reduction (NOR)** 能够保证得到 norm form (如果存在的话)
Definition: An outermost redex is a redex that is not contained inside another one. (Similarly, an innermost redex is one that has no redexes inside it.)
In terms of the abstract-syntax tree, an "apply" node represents an outermost redex iff
- it represents a redex (its left child is a lambda), and
-- it has no ancestor "apply" node in the tree that also represents a redex.

```
                            apply  <-- not a redex
                           /     \
an outermost redex --> apply      apply <-- another outermost redex
                      /    \      /    \
                     λ     ...   λ      apply  <-- redex, but not outermost
                    / \         / \     /   \     
                  ... ...      ... ... λ    ...
```

If it is a function that ignores its argument, then reducing that redex can make other redexes (those that define the argument) "go away"; however, reducing an argument will never make the function "go away".

### Evaluation strategy

- call by value: leftmost-innermost (applicative-order reduction (AOR))
- call by name: leftmost-outermost (normal-order-reduction (NOR))
- call by need: like call by name but the result of the evaluation is saved and is then reused for each subsequent use of the formal.