<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function SIGNAL

### Syntax
`signal datum &rest arguments => nil`  


### Arguments and Values
- **datum, arguments** : designators for a condition of default type simple-condition.   


### Description
Signals the condition denoted by the given datum and arguments. If the condition is not handled, signal returns nil.



### Examples
```lisp 
(defun handle-division-conditions (condition)
   (format t "Considering condition for division condition handling~%")
   (when (and (typep condition 'arithmetic-error)
              (eq '/ (arithmetic-error-operation condition)))
     (invoke-debugger condition)))
HANDLE-DIVISION-CONDITIONS
 (defun handle-other-arithmetic-errors (condition)
   (format t "Considering condition for arithmetic condition handling~%")
   (when (typep condition 'arithmetic-error)
     (abort)))
HANDLE-OTHER-ARITHMETIC-ERRORS
 (define-condition a-condition-with-no-handler (condition) ())
A-CONDITION-WITH-NO-HANDLER
 (signal 'a-condition-with-no-handler)
NIL
 (handler-bind ((condition #'handle-division-conditions)
                  (condition #'handle-other-arithmetic-errors))
   (signal 'a-condition-with-no-handler))
Considering condition for division condition handling
Considering condition for arithmetic condition handling
NIL
 (handler-bind ((arithmetic-error #'handle-division-conditions)
                  (arithmetic-error #'handle-other-arithmetic-errors))
   (signal 'arithmetic-error :operation '* :operands '(1.2 b)))
Considering condition for division condition handling
Considering condition for arithmetic condition handling
Back to Lisp ToplevelSide Effects:
The debugger might be entered due to *break-on-signals*.
Handlers for the condition being signaled might transfer control.
```
