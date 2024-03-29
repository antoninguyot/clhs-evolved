<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function REVAPPEND, NRECONC

### Syntax
`revappend list tail => result-list`  
`nreconc list tail => result-list`  


### Arguments and Values
- **list** : a proper list.   
- **tail** : an object.   
- **result-list** : an object.   


### Description
revappend constructs a copy[2] of list, but with the elements in reverse order. It then appends (as if by nconc) the tail to that reversed list and returns the result.  
nreconc reverses the order of elements in list (as if by nreverse). It then appends (as if by nconc) the tail to that reversed list and returns the result.  
The resulting list shares list structure with tail.



### Examples
```lisp 
(let ((list-1 (list 1 2 3))
       (list-2 (list 'a 'b 'c)))
   (print (revappend list-1 list-2))
   (print (equal list-1 '(1 2 3)))
   (print (equal list-2 '(a b c))))
>>  (3 2 1 A B C) 
>>  T
>>  T
=>  T

 (revappend '(1 2 3) '()) =>  (3 2 1)
 (revappend '(1 2 3) '(a . b)) =>  (3 2 1 A . B)
 (revappend '() '(a b c)) =>  (A B C)
 (revappend '(1 2 3) 'a) =>  (3 2 1 . A)
 (revappend '() 'a) =>  A   ;degenerate case

 (let ((list-1 '(1 2 3))
       (list-2 '(a b c)))
   (print (nreconc list-1 list-2))
   (print (equal list-1 '(1 2 3)))
   (print (equal list-2 '(a b c))))
>>  (3 2 1 A B C) 
>>  NIL
>>  T
=>  TSide Effects:
revappend does not modify either of its arguments. nreconc is permitted to modify list but not tail.
 Although it might be implemented differently, nreconc is constrained to have side-effect behavior equivalent to:
 (nconc (nreverse list) tail)
```
