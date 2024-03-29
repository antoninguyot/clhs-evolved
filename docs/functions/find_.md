<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function FIND, FIND-IF, FIND-IF-NOT

### Syntax
`find item sequence &key from-end test test-not start end key => element`  
`find-if predicate sequence &key from-end start end key => element`  
`find-if-not predicate sequence &key from-end start end key => element`  


### Arguments and Values
- **item** : an object.   
- **sequence** : a proper sequence.   
- **predicate** : a designator for a function of one argument that returns a generalized boolean.   
- **from-end** : a generalized boolean. The default is false.   
- **test** : a designator for a function of two arguments that returns a generalized boolean.   
- **test-not** : a designator for a function of two arguments that returns a generalized boolean.   
- **start, end** : bounding index designators of sequence. The defaults for start and end are 0 and nil, respectively.   
- **key** : a designator for a function of one argument, or nil.   
- **element** : an element of the sequence, or nil.   


### Description
find, find-if, and find-if-not each search for an element of the sequence bounded by start and end that satisfies the predicate predicate or that satisfies the test test or test-not, as appropriate.  
If from-end is true, then the result is the rightmost element that satisfies the test.  
If the sequence contains an element that satisfies the test, then the leftmost or rightmost sequence element, depending on from-end, is returned; otherwise nil is returned.



### Examples
```lisp 
(find #\d "here are some letters that can be looked at" :test #'char>)
=>  #\Space 
 (find-if #'oddp '(1 2 3 4 5) :end 3 :from-end t) =>  3
 (find-if-not #'complexp                                    
             '#(3.5 2 #C(1.0 0.0) #C(0.0 1.0))
             :start 2) =>  NILSide Effects: None.
```
