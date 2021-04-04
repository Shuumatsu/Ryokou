---
title: Type System | Polymorphic Recursion
---

Type inference for polymorphic recursion is undecidable, 这意味着即使一个 function 是 well-typed，编译器也无法推导出其类型

For example:
```
data Nested a = Cons a (Nested [a]) | Epsilon

length' Epsilon = 0
length' (Cons _ rest) = 1 + length' rest
```
会产生一个 type error，因为 length 被应用到了两个不同的类型上 `Nested a` and `Nested [a]`.

The solution is to assert that the type is indeed `Nested a -> Int`.
```
length' :: Nested a -> Int
length' Epsilon = 0
length' (Cons _ rest) = 1 + length' rest
```

---

> :a[https://stackoverflow.com/questions/40247339/polymorphic-recursion-syntax-and-uses]{href=https://stackoverflow.com/questions/40247339/polymorphic-recursion-syntax-and-uses .nav}
