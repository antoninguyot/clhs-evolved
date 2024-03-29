<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PACKAGE-NAME

### Syntax
`package-name package => name`  


### Arguments and Values
- **package** : a package designator.   
- **name** : a string  or nil.   


### Description
package-name returns the string that names package,  or nil if the package designator is a package object that has no name (see the function delete-package).



### Examples
```lisp 
(in-package "COMMON-LISP-USER") =>  #<PACKAGE "COMMON-LISP-USER">
 (package-name *package*) =>  "COMMON-LISP-USER"
 (package-name (symbol-package :test)) =>  "KEYWORD"
 (package-name (find-package 'common-lisp)) =>  "COMMON-LISP"
 (defvar *foo-package* (make-package "FOO"))
 (rename-package "FOO" "FOO0")
 (package-name *foo-package*) =>  "FOO0"Side Effects: None.
```
