<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function ARRAYP

### Syntax
`arrayp object => generalized-boolean`  


### Arguments and Values
- **object** : an object.   
- **generalized-boolean** : a generalized boolean.   


### Description
Returns true if object is of type array; otherwise, returns false.



### Examples
```lisp 
(arrayp (make-array '(2 3 4) :adjustable t)) =>  true
 (arrayp (make-array 6)) =>  true
 (arrayp #*1011) =>  true
 (arrayp "hi") =>  true
 (arrayp 'hi) =>  false
 (arrayp 12) =>  false
```
