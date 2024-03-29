<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro DO, DO*

### Syntax
`do ({var | (var [init-form [step-form]])}*) (end-test-form result-form*) declaration* {tag | statement}* => result*`  
`do* ({var | (var [init-form [step-form]])}*) (end-test-form result-form*) declaration* {tag | statement}* => result*`  


### Arguments and Values
- **var** : a symbol.   
- **init-form** : a form.   
- **step-form** : a form.   
- **end-test-form** : a form.   
- **result-forms** : an implicit progn.   
- **declaration** : a declare expression; not evaluated.   
- **tag** : a go tag; not evaluated.   
- **statement** : a compound form; evaluated as described below.   
- **results** : if a return or return-from form is executed, the values passed from that form; otherwise, the values returned by the result-forms.   


### Description
do iterates over a group of statements while a test condition holds. do accepts an arbitrary number of iteration vars which are bound within the iteration and stepped in parallel. An initial value may be supplied for each iteration variable by use of an init-form. Step-forms may be used to specify how the vars should be updated on succeeding iterations through the loop. Step-forms may be used both to generate successive values or to accumulate results. If the end-test-form condition is met prior to an execution of the body, the iteration terminates. Tags label statements.  
do* is exactly like do except that the bindings and steppings of the vars are performed sequentially rather than in parallel.  
Before the first iteration, all the init-forms are evaluated, and each var is bound to the value of its respective init-form, if supplied. This is a binding, not an assignment; when the loop terminates, the old values of those variables will be restored. For do, all of the init-forms are evaluated before any var is bound. The init-forms can refer to the bindings of the vars visible before beginning execution of do. For do*, the first init-form is evaluated, then the first var is bound to that value, then the second init-form is evaluated, then the second var is bound, and so on; in general, the kth init-form can refer to the new binding of the jth var if j < k, and otherwise to the old binding of the jth var.  
At the beginning of each iteration, after processing the variables, the end-test-form is evaluated. If the result is false, execution proceeds with the body of the do (or do*) form. If the result is true, the result-forms are evaluated in order as an implicit progn, and then do or do* returns.  
At the beginning of each iteration other than the first, vars are updated as follows. All the step-forms, if supplied, are evaluated, from left to right, and the resulting values are assigned to the respective vars. Any var that has no associated step-form is not assigned to. For do, all the step-forms are evaluated before any var is updated; the assignment of values to vars is done in parallel, as if by psetq. Because all of the step-forms are evaluated before any of the vars are altered, a step-form when evaluated always has access to the old values of all the vars, even if other step-forms precede it. For do*, the first step-form is evaluated, then the value is assigned to the first var, then the second step-form is evaluated, then the value is assigned to the second var, and so on; the assignment of values to variables is done sequentially, as if by setq. For either do or do*, after the vars have been updated, the end-test-form is evaluated as described above, and the iteration continues.  
The remainder of the do (or do*) form constitutes an implicit tagbody. Tags may appear within the body of a do loop for use by go statements appearing in the body (but such go statements may not appear in the variable specifiers, the end-test-form, or the result-forms). When the end of a do body is reached, the next iteration cycle (beginning with the evaluation of step-forms) occurs.  
An implicit block named nil surrounds the entire do (or do*) form. A return statement may be used at any point to exit the loop immediately.  
Init-form is an initial value for the var with which it is associated. If init-form is omitted, the initial value of var is nil. If a declaration is supplied for a var, init-form must be consistent with the declaration.  
Declarations can appear at the beginning of a do (or do*) body. They apply to code in the do (or do*) body, to the bindings of the do (or do*) vars, to the step-forms, to the end-test-form, and to the result-forms.



### Examples
```lisp 
(do ((temp-one 1 (1+ temp-one))
       (temp-two 0 (1- temp-two)))
      ((> (- temp-one temp-two) 5) temp-one)) =>  4

 (do ((temp-one 1 (1+ temp-one))
       (temp-two 0 (1+ temp-one)))     
      ((= 3 temp-two) temp-one)) =>  3

 (do* ((temp-one 1 (1+ temp-one))
        (temp-two 0 (1+ temp-one)))
       ((= 3 temp-two) temp-one)) =>  2                     

 (do ((j 0 (+ j 1)))
     (nil)                       ;Do forever.
   (format t "~%Input ~D:" j)
   (let ((item (read)))
     (if (null item) (return)   ;Process items until NIL seen.
         (format t "~&Output ~D: ~S" j item))))
>>  Input 0: banana
>>  Output 0: BANANA
>>  Input 1: (57 boxes)
>>  Output 1: (57 BOXES)
>>  Input 2: NIL
=>  NIL

 (setq a-vector (vector 1 nil 3 nil))
 (do ((i 0 (+ i 1))     ;Sets every null element of a-vector to zero.
      (n (array-dimension a-vector 0)))
     ((= i n))
   (when (null (aref a-vector i))
     (setf (aref a-vector i) 0))) =>  NIL
a-vector =>  #(1 0 3 0)
 (do ((x e (cdr x))
      (oldx x x))
     ((null x))
   body)
 (do ((x foo (cdr x))
      (y bar (cdr y))
      (z '() (cons (f (car x) (car y)) z)))
     ((or (null x) (null y))
      (nreverse z)))
 (defun list-reverse (list)
        (do ((x list (cdr x))
             (y '() (cons (car x) y)))
            ((endp x) y)))
As an example of nested iterations, consider a data structure that is a list of conses. The car of each cons is a list of symbols, and the cdr of each cons is a list of equal length containing corresponding values. Such a data structure is similar to an association list, but is divided into ``frames''; the overall structure resembles a rib-cage. A lookup function on such a data structure might be:
 (defun ribcage-lookup (sym ribcage)           
        (do ((r ribcage (cdr r)))
            ((null r) nil)
          (do ((s (caar r) (cdr s))
               (v (cdar r) (cdr v))) 
              ((null s))
            (when (eq (car s) sym)
              (return-from ribcage-lookup (car v)))))) =>  RIBCAGE-LOOKUP
```
