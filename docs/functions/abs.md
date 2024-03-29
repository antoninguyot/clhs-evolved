<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function ABS

### Syntax
`abs number => absolute-value`  


### Arguments and Values
- **number** : a number.   
- **absolute-value** : a non-negative real.   


### Description
abs returns the absolute value of number.  
If number is  a real,  the result is of the same type as number.  
If number is a complex, the result is a positive  real  with the same magnitude as number. The result can be a float even if number's components are rationals and an exact rational result would have been possible. Thus the result of (abs #c(3 4)) can be either 5 or 5.0, depending on the implementation.



### Examples
```lisp 
(abs 0) =>  0
 (abs 12/13) =>  12/13
 (abs -1.09) =>  1.09
 (abs #c(5.0 -5.0)) =>  7.071068
 (abs #c(5 5)) =>  7.071068
 (abs #c(3/5 4/5)) =>  1 or approximately 1.0
 (eql (abs -0.0) -0.0) =>  true
```
