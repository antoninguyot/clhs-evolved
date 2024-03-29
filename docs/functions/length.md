<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function LENGTH

### Syntax
`length sequence => n`  


### Arguments and Values
- **sequence** : a proper sequence.   
- **n** : a non-negative integer.   


### Description
Returns the number of elements in sequence.  
If sequence is a vector with a fill pointer, the active length as specified by the fill pointer is returned.



### Examples
```lisp 
(length "abc") =>  3
 (setq str (make-array '(3) :element-type 'character 
                            :initial-contents "abc"
                            :fill-pointer t)) =>  "abc"
 (length str) =>  3
 (setf (fill-pointer str) 2) =>  2
 (length str) =>  2
```
