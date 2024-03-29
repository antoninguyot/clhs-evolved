<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function INTERSECTION, NINTERSECTION

### Syntax
`intersection list-1 list-2 &key key test test-not => result-list`  
`nintersection list-1 list-2 &key key test test-not => result-list`  


### Arguments and Values
- **list-1** : a proper list.   
- **list-2** : a proper list.   
- **test** : a designator for a function of two arguments that returns a generalized boolean.   
- **test-not** : a designator for a function of two arguments that returns a generalized boolean.   
- **key** : a designator for a function of one argument, or nil.   
- **result-list** : a list.   


### Description
intersection and nintersection return a list that contains every element that occurs in both list-1 and list-2.  
nintersection is the destructive version of intersection. It performs the same operation, but may destroy list-1 using its cells to construct the result.   list-2 is not destroyed.  
The intersection operation is described as follows. For all possible ordered pairs consisting of one element from list-1 and one element from list-2, :test or :test-not are used to determine whether they satisfy the test. The first argument to the :test or :test-not function is an element of list-1; the second argument is an element of list-2. If :test or :test-not is not supplied, eql is used. It is an error if :test and :test-not are supplied in the same function call.  
If :key is supplied (and not nil), it is used to extract the part to be tested from the list element. The argument to the :key function is an element of either list-1 or list-2; the :key function typically returns part of the supplied element. If :key is not supplied or nil, the list-1 and list-2 elements are used.  
For every pair that satifies the test, exactly one of the two elements of the pair will be put in the result. No element from either list appears in the result that does not satisfy the test for an element from the other list. If one of the lists contains duplicate elements, there may be duplication in the result.  
There is no guarantee that the order of elements in the result will reflect the ordering of the arguments in any particular way. The result list may share cells with, or be eq to, either list-1 or list-2 if appropriate.



### Examples
```lisp 
(setq list1 (list 1 1 2 3 4 a b c "A" "B" "C" "d")
       list2 (list 1 4 5 b c d "a" "B" "c" "D")) 
  =>  (1 4 5 B C D "a" "B" "c" "D")
 (intersection list1 list2) =>  (C B 4 1 1)
 (intersection list1 list2 :test 'equal) =>  ("B" C B 4 1 1)
 (intersection list1 list2 :test #'equalp) =>  ("d" "C" "B" "A" C B 4 1 1) 
 (nintersection list1 list2) =>  (1 1 4 B C)
 list1 =>  implementation-dependent ;e.g.,  (1 1 4 B C)
 list2 =>  implementation-dependent ;e.g.,  (1 4 5 B C D "a" "B" "c" "D")
 (setq list1 (copy-list '((1 . 2) (2 . 3) (3 . 4) (4 . 5))))
=>  ((1 . 2) (2 . 3) (3 . 4) (4 . 5)) 
 (setq list2 (copy-list '((1 . 3) (2 . 4) (3 . 6) (4 . 8))))
=>  ((1 . 3) (2 . 4) (3 . 6) (4 . 8)) 
 (nintersection list1 list2 :key #'cdr) =>  ((2 . 3) (3 . 4)) 
 list1 =>  implementation-dependent ;e.g.,  ((1 . 2) (2 . 3) (3 . 4)) 
 list2 =>  implementation-dependent ;e.g.,  ((1 . 3) (2 . 4) (3 . 6) (4 . 8))Side Effects:
 nintersection can modify list-1,  but not list-2.
```
