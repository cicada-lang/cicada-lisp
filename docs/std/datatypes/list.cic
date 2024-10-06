(define-datatype list (element type) ()
  (null-list (list element))
  (cons-list ((head element)
              (tail (list element)))
             (list element)))

(claim length (implicit ((element type)) (-> (list element) nat)))
(define (length (implicit element) a-list)
  (match a-list
    ((null-list) zero)
    ((cons-list ,head ,tail) (add1 (length tail)))))
