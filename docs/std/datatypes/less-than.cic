(define-datatype less-than () ((j nat) (k nat))
  (zero-smallest ((n nat))
                 (less-than zero (add1 n)))
  (add1-smaller ((j nat)
                 (k nat)
                 (prev-smaller (less-than j k)))
                (less-than (add1 j) (add1 k))))

less-than
(less-than (add1 zero))
(less-than (add1 zero) (add1 (add1 zero)))
