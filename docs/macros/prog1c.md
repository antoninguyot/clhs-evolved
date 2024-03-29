<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro PROG1, PROG2

### Syntax
`prog1 first-form form* => result-1`  
`prog2 first-form second-form form* => result-2`  


### Arguments and Values
- **first-form** : a form; evaluated as described below.   
- **second-form** : a form; evaluated as described below.   
- **forms** : an implicit progn; evaluated as described below.   
- **result-1** : the primary value resulting from the evaluation of first-form.   
- **result-2** : the primary value resulting from the evaluation of second-form.   


### Description
prog1 evaluates first-form and then forms, yielding as its only value the primary value yielded by first-form.  
prog2 evaluates first-form, then second-form, and then forms, yielding as its only value the primary value yielded by first-form.



### Examples
```lisp 
(setq temp 1) =>  1
 (prog1 temp (print temp) (incf temp) (print temp))
>>  1
>>  2
=>  1
 (prog1 temp (setq temp nil)) =>  2
 temp =>  NIL
 (prog1 (values 1 2 3) 4) =>  1 
 (setq temp (list 'a 'b 'c))
 (prog1 (car temp) (setf (car temp) 'alpha)) =>  A
 temp =>  (ALPHA B C)
 (flet ((swap-symbol-values (x y)
          (setf (symbol-value x) 
                (prog1 (symbol-value y)
                       (setf (symbol-value y) (symbol-value x))))))
   (let ((*foo* 1) (*bar* 2))
     (declare (special *foo* *bar*))
     (swap-symbol-values '*foo* '*bar*)
     (values *foo* *bar*)))
=>  2, 1
 (setq temp 1) =>  1
 (prog2 (incf temp) (incf temp) (incf temp)) =>  3
 temp =>  4
 (prog2 1 (values 2 3 4) 5) =>  2Side Effects: None.
```
