---
title: A Class is Always A Pure Interface
date: 2024-09-19
---

在目前的设计中，
一个 `define-class` 所定义的 class，
都是纯粹的 interface。

一个 class 一定是 flat 的，
可以继承一个或多个 super class，
但是 super class 没有具体的 method，
因此也没有需要 override super class 的 method 的问题。

但是注意，
generic function 要求我们用 nominal subtyping，
而不能用 structural subtyping。

因为我们需 nominal 信息来在运行时做 dispatching。

```scheme
(define (display (self bordered-figure))
  (display (as-figure self))
  (display-border self))
```
