<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function COUNT, COUNT-IF, COUNT-IF-NOT

### Syntax
`count item sequence &key from-end start end key test test-not => n`  
`count-if predicate sequence &key from-end start end key => n`  
`count-if-not predicate sequence &key from-end start end key => n`  


### Arguments and Values
- **item** : an object.   
- **sequence** : a proper sequence.   
- **predicate** : a designator for a function of one argument that returns a generalized boolean.   
- **from-end** : a generalized boolean. The default is false.   
- **test** : a designator for a function of two arguments that returns a generalized boolean.   
- **test-not** : a designator for a function of two arguments that returns a generalized boolean.   
- **start, end** : bounding index designators of sequence. The defaults for start and end are 0 and nil, respectively.   
- **key** : a designator for a function of one argument, or nil.   
- **n** : a non-negative integer less than or equal to the length of sequence.   


### Description
count, count-if, and count-if-not count and return the number of elements in the sequence bounded by start and end that satisfy the test.  
The from-end has no direct effect on the result. However, if from-end is true, the elements of sequence will be supplied as arguments to the test, test-not, and key in reverse order, which may change the side-effects, if any, of those functions.



### Examples
```lisp 
(count #\a "how many A's are there in here?") =>  2
 (count-if-not #'oddp '((1) (2) (3) (4)) :key #'car) =>  2
 (count-if #'upper-case-p "The Crying of Lot 49" :start 4) =>  2Side Effects: None.
```
