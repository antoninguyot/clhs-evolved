<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MAKE-LIST

### Syntax
`make-list size &key initial-element => list`  


### Arguments and Values
- **size** : a non-negative integer.   
- **initial-element** : an object. The default is nil.   
- **list** : a list.   


### Description
Returns a list of length given by size, each of the elements of which is initial-element.



### Examples
```lisp 
(make-list 5) =>  (NIL NIL NIL NIL NIL)
 (make-list 3 :initial-element 'rah) =>  (RAH RAH RAH)
 (make-list 2 :initial-element '(1 2 3)) =>  ((1 2 3) (1 2 3))
 (make-list 0) =>  NIL ;i.e.,  ()
 (make-list 0 :initial-element 'new-element) =>  NILSide Effects: None.
```
