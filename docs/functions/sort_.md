<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function SORT, STABLE-SORT

### Syntax
`sort sequence predicate &key key => sorted-sequence`  
`stable-sort sequence predicate &key key => sorted-sequence`  


### Arguments and Values
- **sequence** : a proper sequence.   
- **predicate** : a designator for a function of two arguments that returns a generalized boolean.   
- **key** : a designator for a function of one argument, or nil.   
- **sorted-sequence** : a sequence.   


### Description
sort and stable-sort destructively sort sequences according to the order determined by the predicate function.  
If sequence is a vector, the result is a vector that has the same actual array element type as sequence. If sequence is a list, the result is a list.  
sort determines the relationship between two elements by giving keys extracted from the elements to the predicate. The first argument to the predicate function is the part of one element of sequence extracted by the key function (if supplied); the second argument is the part of another element of sequence extracted by the key function (if supplied). Predicate should return true if and only if the first argument is strictly less than the second (in some appropriate sense). If the first argument is greater than or equal to the second (in the appropriate sense), then the predicate should return false.  
The argument to the key function is the sequence element. The return value of the key function becomes an argument to predicate. If key is not supplied or nil, the sequence element itself is used. There is no guarantee on the number of times the key will be called.  
If the key and predicate always return, then the sorting operation will always terminate, producing a sequence containing the same elements as sequence (that is, the result is a permutation of sequence). This is guaranteed even if the predicate does not really consistently represent a total order (in which case the elements will be scrambled in some unpredictable way, but no element will be lost). If the key consistently returns meaningful keys, and the predicate does reflect some total ordering criterion on those keys, then the elements of the sorted-sequence will be properly sorted according to that ordering.  
The sorting operation performed by sort is not guaranteed stable. Elements considered equal by the predicate might or might not stay in their original order. The predicate is assumed to consider two elements x and y to be equal if (funcall predicate x y) and (funcall predicate y x) are both false. stable-sort guarantees stability.  
The sorting operation can be destructive in all cases. In the case of a vector argument, this is accomplished by permuting the elements in place. In the case of a list, the list is destructively reordered in the same manner as for nreverse.



### Examples
```lisp 
(setq tester (copy-seq "lkjashd")) =>  "lkjashd"
 (sort tester #'char-lessp) =>  "adhjkls"
 (setq tester (list '(1 2 3) '(4 5 6) '(7 8 9))) =>  ((1 2 3) (4 5 6) (7 8 9))
 (sort tester #'> :key #'car)  =>  ((7 8 9) (4 5 6) (1 2 3)) 
 (setq tester (list 1 2 3 4 5 6 7 8 9 0)) =>  (1 2 3 4 5 6 7 8 9 0)
 (stable-sort tester #'(lambda (x y) (and (oddp x) (evenp y))))
=>  (1 3 5 7 9 2 4 6 8 0)
 (sort (setq committee-data
             (vector (list (list "JonL" "White") "Iteration")
                     (list (list "Dick" "Waters") "Iteration")
                     (list (list "Dick" "Gabriel") "Objects")
                     (list (list "Kent" "Pitman") "Conditions")
                     (list (list "Gregor" "Kiczales") "Objects")
                     (list (list "David" "Moon") "Objects")
                     (list (list "Kathy" "Chapman") "Editorial")
                     (list (list "Larry" "Masinter") "Cleanup")
                     (list (list "Sandra" "Loosemore") "Compiler")))
       #'string-lessp :key #'cadar)
=>  #((("Kathy" "Chapman") "Editorial")
     (("Dick" "Gabriel") "Objects")
     (("Gregor" "Kiczales") "Objects")
     (("Sandra" "Loosemore") "Compiler")
     (("Larry" "Masinter") "Cleanup")
     (("David" "Moon") "Objects")
     (("Kent" "Pitman") "Conditions")
     (("Dick" "Waters") "Iteration")
     (("JonL" "White") "Iteration"))
 ;; Note that individual alphabetical order within `committees'
 ;; is preserved.
 (setq committee-data 
       (stable-sort committee-data #'string-lessp :key #'cadr))
=>  #((("Larry" "Masinter") "Cleanup")
     (("Sandra" "Loosemore") "Compiler")
     (("Kent" "Pitman") "Conditions")
     (("Kathy" "Chapman") "Editorial")
     (("Dick" "Waters") "Iteration")
     (("JonL" "White") "Iteration")
     (("Dick" "Gabriel") "Objects")
     (("Gregor" "Kiczales") "Objects")
     (("David" "Moon") "Objects"))Side Effects: None.
```
