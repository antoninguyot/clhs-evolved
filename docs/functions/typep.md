<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function TYPEP

### Syntax
`typep object type-specifier &optional environment => generalized-boolean`  


### Arguments and Values
- **object** : an object.   
- **type-specifier** : any type specifier except values, or a type specifier list whose first element is either function or values.   
- **environment** : an environment object. The default is nil, denoting the null lexical environment and the and current global environment.   
- **generalized-boolean** : a generalized boolean.   


### Description
Returns true if object is of the type specified by type-specifier; otherwise, returns false.  
A type-specifier of the form (satisfies fn) is handled by applying the function fn to object.  
 (typep object '(array type-specifier)), where type-specifier is not *, returns true if and only if object is an array that could be the result of supplying type-specifier as the :element-type argument to make-array. (array *) refers to all arrays regardless of element type, while (array type-specifier) refers only to those arrays that can result from giving type-specifier as the :element-type argument to make-array. A similar interpretation applies to (simple-array type-specifier) and (vector type-specifier). See Section 15.1.2.1 (Array Upgrading).  
(typep object '(complex type-specifier)) returns true for all complex numbers that can result from giving numbers of type type-specifier to the function complex, plus all other complex numbers of the same specialized representation. Both the real and the imaginary parts of any such complex number must satisfy:  
 (typep realpart 'type-specifier)  
 (typep imagpart 'type-specifier)  
See the function upgraded-complex-part-type.



### Examples
```lisp 
(typep 12 'integer) =>  true
 (typep (1+ most-positive-fixnum) 'fixnum) =>  false
 (typep nil t) =>  true
 (typep nil nil) =>  false
 (typep 1 '(mod 2)) =>  true
 (typep #c(1 1) '(complex (eql 1))) =>  true
;; To understand this next example, you might need to refer to
;; Section 12.1.5.3 (Rule of Canonical Representation for Complex Rationals).
 (typep #c(0 0) '(complex (eql 0))) =>  false
 Let Ax and Ay be two type specifiers that denote different types, but for which
 (upgraded-array-element-type 'Ax)
 (upgraded-array-element-type 'Ay)
 (typep (make-array 0 :element-type 'Ax) '(array Ax)) =>  true
 (typep (make-array 0 :element-type 'Ay) '(array Ay)) =>  true
 (typep (make-array 0 :element-type 'Ax) '(array Ay)) =>  true
 (typep (make-array 0 :element-type 'Ay) '(array Ax)) =>  true
```
