(define-datatype nat () ()
  (zero nat)
  (add1 ((prev nat)) nat))

(check (add1 zero) nat)
(check (add1 (add1 zero)) nat)

(claim add (-> nat nat nat))
(define (add x y)
  (match x
    (zero y)
    ((add1 ,prev) (add1 (add prev)))))
