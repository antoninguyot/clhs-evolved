<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PATHNAMEP

### Syntax
`pathnamep object => generalized-boolean`  


### Arguments and Values
- **object** : an object.   
- **generalized-boolean** : a generalized boolean.   


### Description
Returns true if object is of type pathname; otherwise, returns false.



### Examples
```lisp 
(setq q "test")  =>  "test"
 (pathnamep q) =>  false
 (setq q (pathname "test"))
=>  #S(PATHNAME :HOST NIL :DEVICE NIL :DIRECTORY NIL :NAME "test" :TYPE NIL
       :VERSION NIL)
 (pathnamep q) =>  true 
 (setq q (logical-pathname "SYS:SITE;FOO.SYSTEM"))
=>  #P"SYS:SITE;FOO.SYSTEM"
 (pathnamep q) =>  trueSide Effects: None.
```
