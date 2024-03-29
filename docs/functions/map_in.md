<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MAP-INTO

### Syntax
`map-into result-sequence function &rest sequences => result-sequence`  


### Arguments and Values
- **result-sequence** : a proper sequence.   
- **function** : a designator for a function of as many arguments as there are sequences.   
- **sequence** : a proper sequence.   


### Description
Destructively modifies result-sequence to contain the results of applying function to each element in the argument sequences in turn.  
result-sequence and each element of sequences can each be either a list or a vector. If result-sequence and each element of sequences are not all the same length, the iteration terminates when the shortest sequence (of any of the sequences or the result-sequence) is exhausted. If result-sequence is a vector with a fill pointer, the fill pointer is ignored when deciding how many iterations to perform, and afterwards the fill pointer is set to the number of times function was applied. If result-sequence is longer than the shortest element of sequences, extra elements at the end of result-sequence are left unchanged. If result-sequence is nil, map-into immediately returns nil, since nil is a sequence of length zero.  
If function has side effects, it can count on being called first on all of the elements with index 0, then on all of those numbered 1, and so on.



### Examples
```lisp 
(setq a (list 1 2 3 4) b (list 10 10 10 10)) =>  (10 10 10 10)
 (map-into a #'+ a b) =>  (11 12 13 14)
 a =>  (11 12 13 14)
 b =>  (10 10 10 10)
 (setq k '(one two three)) =>  (ONE TWO THREE)
 (map-into a #'cons k a) =>  ((ONE . 11) (TWO . 12) (THREE . 13) 14)
 (map-into a #'gensym) =>  (#:G9090 #:G9091 #:G9092 #:G9093)
 a =>  (#:G9090 #:G9091 #:G9092 #:G9093)
```
