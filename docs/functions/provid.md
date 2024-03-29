<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PROVIDE, REQUIRE

### Syntax
`provide module-name => implementation-dependent`  
`require module-name &optional pathname-list => implementation-dependent`  


### Arguments and Values
- **module-name** : a string designator.   
- **pathname-list** : nil, or a designator for a non-empty list of pathname designators. The default is nil.   


### Description
provide adds the module-name to the list held by *modules*, if such a name is not already present.  
require tests for the presence of the module-name in the list held by *modules*. If it is present, require immediately returns.  Otherwise, an attempt is made to load an appropriate set of files as follows: The pathname-list argument, if non-nil, specifies a list of pathnames to be loaded in order, from left to right. If the pathname-list is nil, an implementation-dependent mechanism will be invoked in an attempt to load the module named module-name; if no such module can be loaded, an error of type error is signaled.  
Both functions use string= to test for the presence of a module-name.



### Examples
```lisp 
;;; This illustrates a nonportable use of REQUIRE, because it
;;; depends on the implementation-dependent file-loading mechanism.

(require "CALCULUS")

;;; This use of REQUIRE is nonportable because of the literal 
;;; physical pathname.  

(require "CALCULUS" "/usr/lib/lisp/calculus")

;;; One form of portable usage involves supplying a logical pathname,
;;; with appropriate translations defined elsewhere.

(require "CALCULUS" "lib:calculus")

;;; Another form of portable usage involves using a variable or
;;; table lookup function to determine the pathname, which again
;;; must be initialized elsewhere.

(require "CALCULUS" *calculus-module-pathname*)Side Effects:
provide modifies *modules*.
```
