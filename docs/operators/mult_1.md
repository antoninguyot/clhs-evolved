<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Special Operator MULTIPLE-VALUE-PROG1

### Syntax
`multiple-value-prog1 first-form form* => first-form-results`  


### Arguments and Values
- **first-form** : a form; evaluated as described below.   
- **form** : a form; evaluated as described below.   
- **first-form-results** : the values resulting from the evaluation of first-form.   


### Description
multiple-value-prog1 evaluates first-form and saves all the values produced by that form. It then evaluates each form from left to right, discarding their values.



### Examples
```lisp 
(setq temp '(1 2 3)) =>  (1 2 3)
 (multiple-value-prog1
    (values-list temp)
    (setq temp nil)
    (values-list temp)) =>  1, 2, 3Side Effects: None.
```
