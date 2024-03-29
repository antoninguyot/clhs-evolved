<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function LISP-IMPLEMENTATION-TYPE, LISP-IMPLEMENTATION-VERSION

### Syntax
`lisp-implementation-type <no arguments> => description`  
`lisp-implementation-version <no arguments> => description`  


### Arguments and Values
- **description** : a string or nil.   


### Description
lisp-implementation-type and lisp-implementation-version identify the current implementation of Common Lisp.  
lisp-implementation-type returns a string that identifies the generic name of the particular Common Lisp implementation.  
lisp-implementation-version returns a string that identifies the version of the particular Common Lisp implementation.  
If no appropriate and relevant result can be produced, nil is returned instead of a string.



### Examples
```lisp 
(lisp-implementation-type)
=>  "ACME Lisp"
OR=>  "Joe's Common Lisp"
 (lisp-implementation-version)
=>  "1.3a"
=>  "V2"
OR=>  "Release 17.3, ECO #6"Side Effects: None.
```
