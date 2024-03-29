<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Accessor FILL-POINTER

### Syntax
`fill-pointer vector => fill-pointer`  
`(setf (fill-pointer vector) new-fill-pointer)`  


### Arguments and Values
- **vector** : a vector with a fill pointer.   
- **fill-pointer, new-fill-pointer** : a valid fill pointer for the vector.   


### Description
Accesses the fill pointer of vector.



### Examples
```lisp 
(setq a (make-array 8 :fill-pointer 4)) =>  #(NIL NIL NIL NIL)
 (fill-pointer a) =>  4
 (dotimes (i (length a)) (setf (aref a i) (* i i))) =>  NIL
 a =>  #(0 1 4 9)
 (setf (fill-pointer a) 3) =>  3
 (fill-pointer a) =>  3
 a =>  #(0 1 4)
 (setf (fill-pointer a) 8) =>  8
 a =>  #(0 1 4 9 NIL NIL NIL NIL)Side Effects: None.
```
