<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Accessor MASK-FIELD

### Syntax
`mask-field bytespec integer => masked-integer`  
`(setf (mask-field bytespec place) new-masked-integer)`  


### Arguments and Values
- **bytespec** : a byte specifier.   
- **integer** : an integer.   
- **masked-integer, new-masked-integer** : a non-negative integer.   


### Description
mask-field performs a ``mask'' operation on integer. It returns an integer that has the same bits as integer in the byte specified by bytespec, but that has zero-bits everywhere else.  
setf may be used with mask-field to modify a byte within the integer that is stored in a given place. The effect is to perform a deposit-field operation and then store the result back into the place.



### Examples
```lisp 
(mask-field (byte 1 5) -1) =>  32
 (setq a 15) =>  15
 (mask-field (byte 2 0) a) =>  3
 a =>  15
 (setf (mask-field (byte 2 0) a) 1) =>  1
 a =>  13Side Effects: None.
```
