<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function FIND-PACKAGE

### Syntax
`find-package name => package`  


### Arguments and Values
- **name** : a string designator or a package object.   
- **package** : a package object or nil.   


### Description
If name is a string designator, find-package locates and returns the package whose name or nickname is name. This search is case sensitive. If there is no such package, find-package returns nil.  
 If name is a package object, that package object is returned.



### Examples
```lisp 
(find-package 'common-lisp) =>  #<PACKAGE "COMMON-LISP">
 (find-package "COMMON-LISP-USER") =>  #<PACKAGE "COMMON-LISP-USER">
 (find-package 'not-there) =>  NILSide Effects: None.
```
