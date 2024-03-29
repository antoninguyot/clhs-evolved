<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function ASSOC, ASSOC-IF, ASSOC-IF-NOT

### Syntax
`assoc item alist &key key test test-not => entry`  
`assoc-if predicate alist &key key => entry`  
`assoc-if-not predicate alist &key key => entry`  


### Arguments and Values
- **item** : an object.   
- **alist** : an association list.   
- **predicate** : a designator for a function of one argument that returns a generalized boolean.   
- **test** : a designator for a function of two arguments that returns a generalized boolean.   
- **test-not** : a designator for a function of two arguments that returns a generalized boolean.   
- **key** : a designator for a function of one argument, or nil.   
- **entry** : a cons that is an element of alist, or nil.   


### Description
assoc, assoc-if, and assoc-if-not return the first cons in alist whose car satisfies the test, or nil if no such cons is found.  
For assoc, assoc-if, and assoc-if-not, if nil appears in alist in place of a pair, it is ignored.



### Examples
```lisp 
(setq values '((x . 100) (y . 200) (z . 50))) =>  ((X . 100) (Y . 200) (Z . 50))
 (assoc 'y values) =>  (Y . 200)
 (rplacd (assoc 'y values) 201) =>  (Y . 201)
 (assoc 'y values) =>  (Y . 201)
 (setq alist '((1 . "one")(2 . "two")(3 . "three"))) 
=>  ((1 . "one") (2 . "two") (3 . "three"))
 (assoc 2 alist) =>  (2 . "two")
 (assoc-if #'evenp alist) =>  (2 . "two")
 (assoc-if-not #'(lambda(x) (< x 3)) alist) =>  (3 . "three")
 (setq alist '(("one" . 1)("two" . 2))) =>  (("one" . 1) ("two" . 2))
 (assoc "one" alist) =>  NIL
 (assoc "one" alist :test #'equalp) =>  ("one" . 1)
 (assoc "two" alist :key #'(lambda(x) (char x 2))) =>  NIL 
 (assoc #\o alist :key #'(lambda(x) (char x 2))) =>  ("two" . 2)
 (assoc 'r '((a . b) (c . d) (r . x) (s . y) (r . z))) =>   (R . X)
 (assoc 'goo '((foo . bar) (zoo . goo))) =>  NIL
 (assoc '2 '((1 a b c) (2 b c d) (-7 x y z))) =>  (2 B C D)
 (setq alist '(("one" . 1) ("2" . 2) ("three" . 3)))
=>  (("one" . 1) ("2" . 2) ("three" . 3))
 (assoc-if-not #'alpha-char-p alist
               :key #'(lambda (x) (char x 0))) =>  ("2" . 2)
```
