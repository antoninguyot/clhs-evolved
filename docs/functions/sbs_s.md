<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function SUBSTITUTE, SUBSTITUTE-IF, SUBSTITUTE-IF-NOT, NSUBSTITUTE, NSUBSTITUTE-IF, NSUBSTITUTE-IF-NOT

### Syntax
`substitute newitem olditem sequence &key from-end test test-not start end count key => result-sequence`  
`substitute-if newitem predicate sequence &key from-end start end count key => result-sequence`  
`substitute-if-not newitem predicate sequence &key from-end start end count key => result-sequence`  
`nsubstitute newitem olditem sequence &key from-end test test-not start end count key => sequence`  
`nsubstitute-if newitem predicate sequence &key from-end start end count key => sequence`  
`nsubstitute-if-not newitem predicate sequence &key from-end start end count key => sequence`  


### Arguments and Values
- **newitem** : an object.   
- **olditem** : an object.   
- **sequence** : a proper sequence.   
- **predicate** : a designator for a function of one argument that returns a generalized boolean.   
- **from-end** : a generalized boolean. The default is false.   
- **test** : a designator for a function of two arguments that returns a generalized boolean.   
- **test-not** : a designator for a function of two arguments that returns a generalized boolean.   
- **start, end** : bounding index designators of sequence. The defaults for start and end are 0 and nil, respectively.   
- **count** : an integer or nil.  The default is nil.   
- **key** : a designator for a function of one argument, or nil.   
- **result-sequence** : a sequence.   


### Description
substitute, substitute-if, and substitute-if-not return a copy of sequence in which each element that satisfies the test has been replaced with newitem.  
nsubstitute, nsubstitute-if, and nsubstitute-if-not are like substitute, substitute-if, and substitute-if-not respectively, but they may modify sequence.  
If sequence is a vector, the result is a vector that has the same actual array element type as sequence. If sequence is a list, the result is a list.  
Count, if supplied, limits the number of elements altered; if more than count elements satisfy the test, then of these elements only the leftmost or rightmost, depending on from-end, are replaced, as many as specified by count.  If count is supplied and negative, the behavior is as if zero had been supplied instead.  If count is nil, all matching items are affected.  
Supplying a from-end of true matters only when the count is provided (and non-nil); in that case, only the rightmost count elements satisfying the test are removed (instead of the leftmost).  
predicate, test, and test-not might be called more than once for each sequence element, and their side effects can happen in any order.  
The result of all these functions is a sequence of the same type as sequence that has the same elements except that those in the subsequence bounded by start and end and satisfying the test have been replaced by newitem.  
substitute, substitute-if, and substitute-if-not return a sequence which can share with sequence or may be identical to the input sequence if no elements need to be changed.  
 nsubstitute and nsubstitute-if are required to setf any car (if sequence is a list) or aref (if sequence is a vector) of sequence that is required to be replaced with newitem. If sequence is a list, none of the cdrs of the top-level list can be modified.



### Examples
```lisp 
(substitute #\. #\SPACE "0 2 4 6") =>  "0.2.4.6"
 (substitute 9 4 '(1 2 4 1 3 4 5)) =>  (1 2 9 1 3 9 5)
 (substitute 9 4 '(1 2 4 1 3 4 5) :count 1) =>  (1 2 9 1 3 4 5)
 (substitute 9 4 '(1 2 4 1 3 4 5) :count 1 :from-end t)
=>  (1 2 4 1 3 9 5)
 (substitute 9 3 '(1 2 4 1 3 4 5) :test #'>) =>  (9 9 4 9 3 4 5)

 (substitute-if 0 #'evenp '((1) (2) (3) (4)) :start 2 :key #'car)
=>  ((1) (2) (3) 0)
 (substitute-if 9 #'oddp '(1 2 4 1 3 4 5)) =>  (9 2 4 9 9 4 9)
 (substitute-if 9 #'evenp '(1 2 4 1 3 4 5) :count 1 :from-end t)
=>  (1 2 4 1 3 9 5)

 (setq some-things (list 'a 'car 'b 'cdr 'c)) =>  (A CAR B CDR C)
 (nsubstitute-if "function was here" #'fboundp some-things
                 :count 1 :from-end t) =>  (A CAR B "function was here" C)
 some-things =>  (A CAR B "function was here" C)
 (setq alpha-tester (copy-seq "ab ")) =>  "ab "
 (nsubstitute-if-not #\z #'alpha-char-p alpha-tester) =>  "abz"
 alpha-tester =>  "abz"Side Effects:
nsubstitute, nsubstitute-if, and nsubstitute-if-not modify sequence.
```
