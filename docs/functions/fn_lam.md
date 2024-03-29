<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function FUNCTION-LAMBDA-EXPRESSION

### Syntax
`function-lambda-expression function => lambda-expression, closure-p, name`  


### Arguments and Values
- **function** : a function.   
- **lambda-expression** : a lambda expression or nil.   
- **closure-p** : a generalized boolean.   
- **name** : an object.   


### Description
Returns information about function as follows:  
The primary value, lambda-expression, is function's defining lambda expression, or nil if the information is not available. The lambda expression may have been pre-processed in some ways, but it should remain a suitable argument to compile or function. Any implementation may legitimately return nil as the lambda-expression of any function.  
The secondary value, closure-p, is nil if function's definition was enclosed in the null lexical environment or something non-nil if function's definition might have been enclosed in some non-null lexical environment. Any implementation may legitimately return true as the closure-p of any function.  
The tertiary value, name, is the ``name'' of function. The name is intended for debugging only and is not necessarily one that would be valid for use as a name in defun or function, for example. By convention, nil is used to mean that function has no name. Any implementation may legitimately return nil as the name of any function.



### Examples
```lisp 
The following examples illustrate some possible return values, but are not intended to be exhaustive:
 (function-lambda-expression #'(lambda (x) x))
=>  NIL, false, NIL
OR=>  NIL, true, NIL
OR=>  (LAMBDA (X) X), true, NIL
OR=>  (LAMBDA (X) X), false, NIL

 (function-lambda-expression
    (funcall #'(lambda () #'(lambda (x) x))))
=>  NIL, false, NIL
OR=>  NIL, true, NIL
OR=>  (LAMBDA (X) X), true, NIL
OR=>  (LAMBDA (X) X), false, NIL
 
 (function-lambda-expression 
    (funcall #'(lambda (x) #'(lambda () x)) nil))
=>  NIL, true, NIL
OR=>  (LAMBDA () X), true, NIL
NOT=>  NIL, false, NIL
NOT=>  (LAMBDA () X), false, NIL
  
 (flet ((foo (x) x))
   (setf (symbol-function 'bar) #'foo)
   (function-lambda-expression #'bar))
=>  NIL, false, NIL
OR=>  NIL, true, NIL
OR=>  (LAMBDA (X) (BLOCK FOO X)), true, NIL
OR=>  (LAMBDA (X) (BLOCK FOO X)), false, FOO
OR=>  (SI::BLOCK-LAMBDA FOO (X) X), false, FOO
 
 (defun foo ()
   (flet ((bar (x) x))
     #'bar))
 (function-lambda-expression (foo))
=>  NIL, false, NIL
OR=>  NIL, true, NIL
OR=>  (LAMBDA (X) (BLOCK BAR X)), true, NIL
OR=>  (LAMBDA (X) (BLOCK BAR X)), true, (:INTERNAL FOO 0 BAR)
OR=>  (LAMBDA (X) (BLOCK BAR X)), false, "BAR in FOO"Side Effects: None.
```
