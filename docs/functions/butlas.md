<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function BUTLAST, NBUTLAST

### Syntax
`butlast list &optional n => result-list`  
`nbutlast list &optional n => result-list`  


### Arguments and Values
- **list** : a list,  which might be a dotted list but must not be a circular list.   
- **n** : a non-negative integer.   
- **result-list** : a list.   


### Description
butlast returns a copy of list from which the last n  conses  have been omitted. If n is not supplied, its value is 1. If there are fewer than n  conses  in list, nil is returned and, in the case of nbutlast, list is not modified.  
nbutlast is like butlast, but nbutlast may modify list. It changes the cdr of the cons n+1 from the end of the list to nil.



### Examples
```lisp 
(setq lst '(1 2 3 4 5 6 7 8 9)) =>  (1 2 3 4 5 6 7 8 9)
 (butlast lst) =>  (1 2 3 4 5 6 7 8)
 (butlast lst 5) =>  (1 2 3 4)
 (butlast lst (+ 5 5)) =>  NIL
 lst =>  (1 2 3 4 5 6 7 8 9)
 (nbutlast lst 3) =>  (1 2 3 4 5 6)
 lst =>  (1 2 3 4 5 6)
 (nbutlast lst 99) =>  NIL
 lst =>  (1 2 3 4 5 6)
 (butlast '(a b c d)) =>  (A B C)
 (butlast '((a b) (c d))) =>  ((A B))
 (butlast '(a)) =>  NIL
 (butlast nil) =>  NIL
 (setq foo (list 'a 'b 'c 'd)) =>  (A B C D)
 (nbutlast foo) =>  (A B C)
 foo =>  (A B C)
 (nbutlast (list 'a)) =>  NIL
 (nbutlast '()) =>  NIL
```
