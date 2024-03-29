<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function FILL

### Syntax
`fill sequence item &key start end => sequence`  


### Arguments and Values
- **sequence** : a proper sequence.   
- **item** : a sequence.   
- **start, end** : bounding index designators of sequence. The defaults for start and end are 0 and nil, respectively.   


### Description
Replaces the elements of sequence bounded by start and end with item.



### Examples
```lisp 
(fill (list 0 1 2 3 4 5) '(444)) =>  ((444) (444) (444) (444) (444) (444))
 (fill (copy-seq "01234") #\e :start 3) =>  "012ee"
 (setq x (vector 'a 'b 'c 'd 'e)) =>  #(A B C D E)
 (fill x 'z :start 1 :end 3) =>  #(A Z Z D E)
 x =>  #(A Z Z D E)
 (fill x 'p) =>  #(P P P P P)
 x =>  #(P P P P P)Side Effects:
Sequence is destructively modified.
```
