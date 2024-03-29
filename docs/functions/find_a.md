<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function FIND-ALL-SYMBOLS

### Syntax
`find-all-symbols string => symbols`  


### Arguments and Values
- **string** : a string designator.   
- **symbols** : a list of symbols.   


### Description
find-all-symbols searches  every registered package  for symbols that have a name that is the same (under string=) as string. A list of all such symbols is returned. Whether or how the list is ordered is implementation-dependent.



### Examples
```lisp 
(find-all-symbols 'car)
=>  (CAR)
OR=>  (CAR VEHICLES:CAR)
OR=>  (VEHICLES:CAR CAR)
 (intern "CAR" (make-package 'temp :use nil)) =>  TEMP::CAR, NIL
 (find-all-symbols 'car)
=>  (TEMP::CAR CAR)
OR=>  (CAR TEMP::CAR)
OR=>  (TEMP::CAR CAR VEHICLES:CAR)
OR=>  (CAR TEMP::CAR VEHICLES:CAR)Side Effects: None.
```
