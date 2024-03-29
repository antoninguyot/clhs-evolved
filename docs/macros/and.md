<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro AND

### Syntax
`and form* => result*`  


### Arguments and Values
- **form** : a form.   
- **results** : the values resulting from the evaluation of the last form, or the symbols nil or t.   


### Description
The macro and evaluates each form one at a time from left to right. As soon as any form evaluates to nil, and returns nil without evaluating the remaining forms. If all forms but the last evaluate to true values, and returns the results produced by evaluating the last form.  
If no forms are supplied, (and) returns t.  
and passes back multiple values from the last subform but not from subforms other than the last.



### Examples
```lisp 
(if (and (>= n 0)
          (< n (length a-simple-vector))
          (eq (elt a-simple-vector n) 'foo))
     (princ "Foo!"))
 (setq temp1 1 temp2 1 temp3 1) =>  1 
 (and (incf temp1) (incf temp2) (incf temp3)) =>  2 
 (and (eql 2 temp1) (eql 2 temp2) (eql 2 temp3)) =>  true
 (decf temp3) =>  1 
 (and (decf temp1) (decf temp2) (eq temp3 'nil) (decf temp3)) =>  NIL 
 (and (eql temp1 temp2) (eql temp2 temp3)) =>  true
 (and) =>  T
```
