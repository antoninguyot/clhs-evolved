<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MAKE-SYMBOL

### Syntax
`make-symbol name => new-symbol`  


### Arguments and Values
- **name** : a string.   
- **new-symbol** : a fresh, uninterned symbol.   


### Description
make-symbol creates and returns a fresh, uninterned symbol whose name is the given name. The new-symbol is neither bound nor fbound and has a null property list.  
It is implementation-dependent whether the string that becomes the new-symbol's name is the given name or a copy of it. Once a string has been given as the name argument to make-symbol, the consequences are undefined if a subsequent attempt is made to alter that string.



### Examples
```lisp 
(setq temp-string "temp") =>  "temp"
 (setq temp-symbol (make-symbol temp-string)) =>  #:|temp|
 (symbol-name temp-symbol) =>  "temp"
 (eq (symbol-name temp-symbol) temp-string) =>  implementation-dependent
 (find-symbol "temp") =>  NIL, NIL
 (eq (make-symbol temp-string) (make-symbol temp-string)) =>  falseSide Effects: None.
```
