<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Special Operator PROGV

### Syntax
`progv symbols values form* => result*`  


### Arguments and Values
- **symbols** : a list of symbols; evaluated.   
- **values** : a list of objects; evaluated.   
- **forms** : an implicit progn.   
- **results** : the values returned by the forms.   


### Description
progv creates new dynamic variable bindings and executes each form using those bindings. Each form is evaluated in order.  
progv allows binding one or more dynamic variables whose names may be determined at run time. Each form is evaluated in order with the dynamic variables whose names are in symbols bound to corresponding values. If too few values are supplied, the remaining symbols are bound and then made to have no value. If too many values are supplied, the excess values are ignored. The bindings of the dynamic variables are undone on exit from progv.



### Examples
```lisp 
(setq *x* 1) =>  1
 (progv '(*x*) '(2) *x*) =>  2
 *x* =>  1

Assuming *x* is not globally special,

 (let ((*x* 3)) 
    (progv '(*x*) '(4) 
      (list *x* (symbol-value '*x*)))) =>  (3 4)
```
