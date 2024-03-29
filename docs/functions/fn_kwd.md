<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Standard Generic Function FUNCTION-KEYWORDS

### Syntax
`function-keywords method => keys, allow-other-keys-pMethod Signatures:`  
`function-keywords (method standard-method)`  


### Arguments and Values
- **method** : a method.   
- **keys** : a list.   
- **allow-other-keys-p** : a generalized boolean.   


### Description
Returns the keyword parameter specifiers for a method.  
Two values are returned: a list of the explicitly named keywords and a generalized boolean that states whether &allow-other-keys had been specified in the method definition.



### Examples
```lisp 
(defmethod gf1 ((a integer) &optional (b 2)
                 &key (c 3) ((:dee d) 4) e ((eff f)))
   (list a b c d e f))
=>  #<STANDARD-METHOD GF1 (INTEGER) 36324653>
 (find-method #'gf1 '() (list (find-class 'integer))) 
=>  #<STANDARD-METHOD GF1 (INTEGER) 36324653>
 (function-keywords *)
=>  (:C :DEE :E EFF), false
 (defmethod gf2 ((a integer))
   (list a b c d e f))
=>  #<STANDARD-METHOD GF2 (INTEGER) 42701775>
 (function-keywords (find-method #'gf1 '() (list (find-class 'integer))))
=>  (), false
 (defmethod gf3 ((a integer) &key b c d &allow-other-keys)
   (list a b c d e f))
 (function-keywords *)
=>  (:B :C :D), true
```
