(define-datatype fin () ((n nat))
  (zero-fin ((implicit k nat)) (fin (nat:add1 k)))
  (add1-fin ((implicit k nat)) (-> (fin k) (fin (nat:add1 k)))))
