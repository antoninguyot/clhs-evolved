<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function FUNCTIONP

### Syntax
`functionp object => generalized-boolean`  


### Arguments and Values
- **object** : an object.   
- **generalized-boolean** : a generalized boolean.   


### Description
Returns true if object is of type function; otherwise, returns false.



### Examples
```lisp 
(functionp 'append) =>  false
 (functionp #'append) =>  true
 (functionp (symbol-function 'append)) =>  true
 (flet ((f () 1)) (functionp #'f)) =>  true
 (functionp (compile nil '(lambda () 259))) =>  true
 (functionp nil) =>  false
 (functionp 12) =>  false
 (functionp '(lambda (x) (* x x))) =>  false
 (functionp #'(lambda (x) (* x x))) =>  trueSide Effects: None.
```
