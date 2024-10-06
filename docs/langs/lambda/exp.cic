(define-datatype exp () ()
  (var-exp ((name string)) exp)
  (ap-exp ((target exp) (arg exp)) exp)
  (fn-exp ((name string) (body exp)) exp))

(define-datatype value () ()
  ...)

(define-datatype env () ()
  (empty-env env)
  (cons-env ((name string)
             (a-value value)
             (rest-env env))
            env))

(define-datatype dict ((element type)) ()
  (null-dict (dict element))
  (cons-dict ((name string)
              (value element)
              (rest env))
             env))

(claim evaluate (-> env exp exp))
(define (evaluate an-env an-exp)
  (match an-exp
    ((var-exp ,name) ...)
    ((ap-exp ,target ,arg) ...)
    ((fn-exp ,name ,body) ...)))
