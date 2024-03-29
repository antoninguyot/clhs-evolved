<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function REMOVE-DUPLICATES, DELETE-DUPLICATES

### Syntax
`remove-duplicates sequence &key from-end test test-not start end key => result-sequence`  
`delete-duplicates sequence &key from-end test test-not start end key => result-sequence`  


### Arguments and Values
- **sequence** : a proper sequence.   
- **from-end** : a generalized boolean. The default is false.   
- **test** : a designator for a function of two arguments that returns a generalized boolean.   
- **test-not** : a designator for a function of two arguments that returns a generalized boolean.   
- **start, end** : bounding index designators of sequence. The defaults for start and end are 0 and nil, respectively.   
- **key** : a designator for a function of one argument, or nil.   
- **result-sequence** : a sequence.   


### Description
remove-duplicates returns a modified copy of sequence from which any element that matches another element occurring in sequence has been removed.  
If sequence is a vector, the result is a vector that has the same actual array element type as sequence. If sequence is a list, the result is a list.  
delete-duplicates is like remove-duplicates, but delete-duplicates may modify sequence.  
The elements of sequence are compared pairwise, and if any two match, then the one occurring earlier in sequence is discarded, unless from-end is true, in which case the one later in sequence is discarded.  
remove-duplicates and delete-duplicates return a sequence of the same type as sequence with enough elements removed so that no two of the remaining elements match. The order of the elements remaining in the result is the same as the order in which they appear in sequence.  
remove-duplicates returns a sequence that may share with sequence or may be identical to sequence if no elements need to be removed.  
 delete-duplicates, when sequence is a list, is permitted to setf any part, car or cdr, of the top-level list structure in that sequence. When sequence is a vector, delete-duplicates is permitted to change the dimensions of the vector and to slide its elements into new positions without permuting them to produce the resulting vector.



### Examples
```lisp 
(remove-duplicates "aBcDAbCd" :test #'char-equal :from-end t) =>  "aBcD"
 (remove-duplicates '(a b c b d d e)) =>  (A C B D E)
 (remove-duplicates '(a b c b d d e) :from-end t) =>  (A B C D E)
 (remove-duplicates '((foo #\a) (bar #\%) (baz #\A))
     :test #'char-equal :key #'cadr) =>  ((BAR #\%) (BAZ #\A))
 (remove-duplicates '((foo #\a) (bar #\%) (baz #\A)) 
     :test #'char-equal :key #'cadr :from-end t) =>  ((FOO #\a) (BAR #\%))
 (setq tester (list 0 1 2 3 4 5 6))
 (delete-duplicates tester :key #'oddp :start 1 :end 6) =>  (0 4 5 6)Side Effects:
delete-duplicates might destructively modify sequence.
```
