<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro DO-SYMBOLS, DO-EXTERNAL-SYMBOLS, DO-ALL-SYMBOLS

### Syntax
`do-symbols (var [package [result-form]]) declaration* {tag | statement}* => result*`  
`do-external-symbols (var [package [result-form]]) declaration* {tag | statement}* => result*`  
`do-all-symbols (var [result-form]) declaration* {tag | statement}* => result*`  


### Arguments and Values
- **var** : a variable name; not evaluated.   
- **package** : a package designator; evaluated.  The default in do-symbols and do-external-symbols is the current package.   
- **result-form** : a form; evaluated as described below. The default is nil.   
- **declaration** : a declare expression; not evaluated.   
- **tag** : a go tag; not evaluated.   
- **statement** : a compound form; evaluated as described below.   
- **results** : the values returned by the result-form if a normal return occurs, or else, if an explicit return occurs, the values that were transferred.   


### Description
do-symbols, do-external-symbols, and do-all-symbols iterate over the symbols of packages. For each symbol in the set of packages chosen, the var is bound to the symbol, and the statements in the body are executed. When all the symbols have been processed, result-form is evaluated and returned as the value of the macro.  
do-symbols iterates over the symbols accessible in package.  Statements may execute more than once for symbols that are inherited from multiple packages.  
do-all-symbols iterates on every registered package. do-all-symbols will not process every symbol whatsoever, because a symbol not accessible in any registered package will not be processed. do-all-symbols may cause a symbol that is present in several packages to be processed more than once.  
do-external-symbols iterates on the external symbols of package.  
When result-form is evaluated, var is bound and has the value nil.  
 An implicit block named nil surrounds the entire do-symbols, do-external-symbols, or do-all-symbols form.  return or return-from may be used to terminate the iteration prematurely.  
If execution of the body affects which symbols are contained in the set of packages over which iteration is occurring, other than to remove the symbol currently the value of var by using unintern, the consequences are undefined.  
For each of these macros, the scope of the name binding does not include any initial value form, but the optional result forms are included.  
Any tag in the body is treated as with tagbody.



### Examples
```lisp 
(make-package 'temp :use nil) =>  #<PACKAGE "TEMP">
 (intern "SHY" 'temp) =>  TEMP::SHY, NIL ;SHY will be an internal symbol
                                         ;in the package TEMP
 (export (intern "BOLD" 'temp) 'temp)  =>  T  ;BOLD will be external  
 (let ((lst ()))
   (do-symbols (s (find-package 'temp)) (push s lst))
   lst)
=>  (TEMP::SHY TEMP:BOLD)
OR=>  (TEMP:BOLD TEMP::SHY)
 (let ((lst ()))
   (do-external-symbols (s (find-package 'temp) lst) (push s lst))
   lst) 
=>  (TEMP:BOLD)
 (let ((lst ()))                                                     
   (do-all-symbols (s lst)
     (when (eq (find-package 'temp) (symbol-package s)) (push s lst)))
   lst)
=>  (TEMP::SHY TEMP:BOLD)
OR=>  (TEMP:BOLD TEMP::SHY)Side Effects: None.
```
