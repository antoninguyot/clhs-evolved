<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function /

### Syntax
`/ number => reciprocal`  
`/ numerator &rest denominators+ => quotient`  


### Arguments and Values
- **number, denominator** : a non-zero number.   
- **numerator, quotient, reciprocal** : a number.   


### Description
The function / performs division or reciprocation.  
If no denominators are supplied, the function / returns the reciprocal of number.  
If at least one denominator is supplied, the function / divides the numerator by all of the denominators and returns the resulting quotient.  
If each argument is either an integer or a ratio, and the result is not an integer, then it is a ratio.  
The function / performs necessary type conversions.  
If any argument is a float then the rules of floating-point contagion apply; see Section 12.1.4 (Floating-point Computations).



### Examples
```lisp 
(/ 12 4) =>  3
 (/ 13 4) =>  13/4
 (/ -8) =>  -1/8
 (/ 3 4 5) =>  3/20
 (/ 0.5) =>  2.0
 (/ 20 5) =>  4
 (/ 5 20) =>  1/4
 (/ 60 -2 3 5.0) =>  -2.0
 (/ 2 #c(2 2)) =>  #C(1/2 -1/2)
```
