<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Accessor BIT, SBIT

### Syntax
`bit bit-array &rest subscripts => bit`  
`sbit bit-array &rest subscripts => bit`  
`(setf (bit bit-array &rest subscripts) new-bit)`  
`(setf (sbit bit-array &rest subscripts) new-bit)`  


### Arguments and Values
- **bit-array** : for bit, a bit array; for sbit, a simple bit array.   
- **subscripts** : a list of valid array indices for the bit-array.   
- **bit** : a bit.   


### Description
bit and sbit access the bit-array element specified by subscripts.  
These functions ignore the fill pointer when accessing elements.



### Examples
```lisp 
(bit (setq ba (make-array 8 
                            :element-type 'bit 
                            :initial-element 1))
       3) =>  1
 (setf (bit ba 3) 0) =>  0
 (bit ba 3) =>  0
 (sbit ba 5) =>  1
 (setf (sbit ba 5) 1) =>  1
 (sbit ba 5) =>  1
```
