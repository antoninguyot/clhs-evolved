<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function ABORT, CONTINUE, MUFFLE-WARNING, STORE-VALUE, USE-VALUE

### Syntax
`abort &optional condition =>|`  
`continue &optional condition => nil`  
`muffle-warning &optional condition =>|`  
`store-value value &optional condition => nil`  
`use-value value &optional condition => nil`  


### Arguments and Values
- **value** : an object.   
- **condition** : a condition object, or nil.   


### Description
Transfers control to the most recently established applicable restart having the same name as the function. That is, the function abort searches for an applicable abort restart, the function continue searches for an applicable continue restart, and so on.  
If no such restart exists, the functions continue, store-value, and use-value return nil, and the functions abort and muffle-warning signal an error of type control-error.  
 When condition is non-nil, only those restarts are considered that are either explicitly associated with that condition, or not associated with any condition; that is, the excluded restarts are those that are associated with a non-empty set of conditions of which the given condition is not an element. If condition is nil, all restarts are considered.



### Examples
```lisp 
;;; Example of the ABORT retart

 (defmacro abort-on-error (&body forms)
   `(handler-bind ((error #'abort))
      ,@forms)) =>  ABORT-ON-ERROR
 (abort-on-error (+ 3 5)) =>  8
 (abort-on-error (error "You lose."))
>>  Returned to Lisp Top Level.

;;; Example of the CONTINUE restart

 (defun real-sqrt (n)
   (when (minusp n)
     (setq n (- n))
     (cerror "Return sqrt(~D) instead." "Tried to take sqrt(-~D)." n))
   (sqrt n))

 (real-sqrt 4) =>  2
 (real-sqrt -9)
>>  Error: Tried to take sqrt(-9).
>>  To continue, type :CONTINUE followed by an option number:
>>   1: Return sqrt(9) instead.
>>   2: Return to Lisp Toplevel.
>>  Debug> (continue)
>>  Return sqrt(9) instead.
=>  3
 
 (handler-bind ((error #'(lambda (c) (continue))))
   (real-sqrt -9)) =>  3

;;; Example of the MUFFLE-WARNING restart

 (defun count-down (x)
   (do ((counter x (1- counter)))
       ((= counter 0) 'done)
     (when (= counter 1)
       (warn "Almost done"))
     (format t "~&~D~%" counter)))
=>  COUNT-DOWN
 (count-down 3)
>>  3
>>  2
>>  Warning: Almost done
>>  1
=>  DONE
 (defun ignore-warnings-while-counting (x)
   (handler-bind ((warning #'ignore-warning))
     (count-down x)))
=>  IGNORE-WARNINGS-WHILE-COUNTING
 (defun ignore-warning (condition)
   (declare (ignore condition))
   (muffle-warning))
=>  IGNORE-WARNING
 (ignore-warnings-while-counting 3)
>>  3
>>  2
>>  1
=>  DONE

;;; Example of the STORE-VALUE and USE-VALUE restarts

 (defun careful-symbol-value (symbol)
   (check-type symbol symbol)
   (restart-case (if (boundp symbol)
                     (return-from careful-symbol-value 
                                  (symbol-value symbol))
                     (error 'unbound-variable
                            :name symbol))
     (use-value (value)
       :report "Specify a value to use this time."
       value)
     (store-value (value)
       :report "Specify a value to store and use in the future."
       (setf (symbol-value symbol) value))))
 (setq a 1234) =>  1234
 (careful-symbol-value 'a) =>  1234
 (makunbound 'a) =>  A
 (careful-symbol-value 'a)
>>  Error: A is not bound.
>>  To continue, type :CONTINUE followed by an option number.
>>   1: Specify a value to use this time.
>>   2: Specify a value to store and use in the future.
>>   3: Return to Lisp Toplevel.
>>  Debug> (use-value 12)
=>  12
 (careful-symbol-value 'a)
>>  Error: A is not bound.
>>  To continue, type :CONTINUE followed by an option number.
>>    1: Specify a value to use this time.
>>    2: Specify a value to store and use in the future.
>>    3: Return to Lisp Toplevel.
>>  Debug> (store-value 24)
=>  24
 (careful-symbol-value 'a)
=>  24

;;; Example of the USE-VALUE restart

 (defun add-symbols-with-default (default &rest symbols)
   (handler-bind ((sys:unbound-symbol
                    #'(lambda (c)
                        (declare (ignore c)) 
                        (use-value default))))
     (apply #'+ (mapcar #'careful-symbol-value symbols))))
=>  ADD-SYMBOLS-WITH-DEFAULT
 (setq x 1 y 2) =>  2
 (add-symbols-with-default 3 'x 'y 'z) =>  6Side Effects:
A transfer of control may occur if an appropriate restart is available, or (in the case of the function abort or the function muffle-warning) execution may be stopped.
```
