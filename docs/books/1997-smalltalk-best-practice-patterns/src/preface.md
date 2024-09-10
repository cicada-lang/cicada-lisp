一个例子是这段代码：

```smalltalk
Station>>computePart: aPart
  ^self multiplyPartTimesRate: aPart

Station>>multiplyPartTimesRate: aPart
  ^Part
    amount: aPart amount * self rate
    date: aPart date
```

> I said, “we seem to be using a lot of the Part’s data in
> multiplyPartTimesRate:. Why don’t we move this code into Part?”
> “But we didn’t design Parts to do arithmetic!” “Since the code
> seems to be telling us to do this, let’s try it.”

```smalltalk
Part>>* aRate
  ^Part
    amount: amount * aRate
    date: date

Station>>computePart: aPart
  ^aPart * self rate
```

对应于 TypeScript 可能是：

```typescript
class Part {
  amount: number
  date: Date
}

class Station {
  rate: number

  computePart(aPart) {
    return this.multiplyPartTimesRate(aPart)
  }

  multiplyPartTimesRate(aPart) {
    return Part({
      amount: aPart.amount * this.rate,
      date: aPart.date,
    })
  }
}
```

改成：

```typescript
class Part {
  amount: number
  date: Date

  mul(aRate) {
    return Part({
      amount: this.amount * aRate,
      date: this.date,
    })
  }
}

class Station {
  rate: number

  computePart(aPart) {
    return aPart.mul(this.rate)
  }
}
```

用想像的 cicada-lisp：

```scheme
(define-class part ()
  (claim amount number)
  (claim date date)
  (define (mul a-rate)
    (create part
      :amount (number-mul amount a-rate)
      :date date)))

(define-class station ()
  (claim rate number)
  (define (compute-part a-part)
    (a-part :mul rate)))
```

可以发现，在想像中的 cicada-lisp 中，
如果用之前的 cicada 的语义，
那么 `(claim date date)` 这种 class 中的 statement 是有问题的。
因为这相当于是引入局部变量，而不是引入一个 property name。

在 cicada-lisp 中，`define-class` 时，
不能有 define，只能有 claim。

```scheme
(define-class part ()
  :amount number
  :date date)

(define (part-mul (a-part part) (a-rate number))
  (create part
    :amount (number-mul (a-part :amount) a-rate)
    :date (a-part :date)))

(define-class station ()
  :rate number)

(define (station-compute-part
         (a-station station)
         (a-part part))
  (part-mul a-part (a-station :rate)))
```

函数类型应该在 claim 中声明，
而不应该在 define 中声明：

```scheme
(define-class part ()
  :amount number
  :date date)

(claim part-mul (-> part number part))
(define (part-mul a-part a-rate)
  (create part
    :amount (number-mul (a-part :amount) a-rate)
    :date (a-part :date)))

(define-class station ()
  :rate number)

(claim station-compute-part (-> station part part))
(define (station-compute-part a-station a-part)
  (part-mul a-part (a-station :rate)))
```
