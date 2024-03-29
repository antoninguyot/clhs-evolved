<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function ARRAY-ELEMENT-TYPE

### Syntax
`array-element-type array => typespec`  


### Arguments and Values
- **array** : an array.   
- **typespec** : a type specifier.   


### Description
Returns a type specifier which represents the actual array element type of the array, which is the set of objects that such an array can hold. (Because of array upgrading, this type specifier can in some cases denote a supertype of the expressed array element type of the array.)



### Examples
```lisp 
(array-element-type (make-array 4)) =>  T
 (array-element-type (make-array 12 :element-type '(unsigned-byte 8))) 
=>  implementation-dependent
 (array-element-type (make-array 12 :element-type '(unsigned-byte 5)))
=>  implementation-dependent
 (array-element-type (make-array 5 :element-type '(mod 5)))
```
