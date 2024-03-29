<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function RANDOM

### Syntax
`random limit &optional random-state => random-number`  


### Arguments and Values
- **limit** : a positive integer, or a positive float.   
- **random-state** : a random state. The default is the current random state.   
- **random-number** : a non-negative number less than limit and of the same type as limit.   


### Description
Returns a pseudo-random number that is a non-negative number less than limit and of the same type as limit.  
The random-state, which is modified by this function, encodes the internal state maintained by the random number generator.  
An approximately uniform choice distribution is used. If limit is an integer, each of the possible results occurs with (approximate) probability 1/limit.



### Examples
```lisp 
(<= 0 (random 1000) 1000) =>  true
 (let ((state1 (make-random-state))
       (state2 (make-random-state)))
   (= (random 1000 state1) (random 1000 state2))) =>  trueSide Effects:
The random-state is modified.
```
