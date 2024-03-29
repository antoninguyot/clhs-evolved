<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PHASE

### Syntax
`phase number => phase`  


### Arguments and Values
- **number** : a number.   
- **phase** : a number.   


### Description
phase returns the phase of number (the angle part of its polar representation) in radians, in the range  -<PI> (exclusive) if minus zero is not supported, or -<PI> (inclusive) if minus zero is supported,  to <PI> (inclusive). The phase of a positive  real  number is zero; that of a negative  real  number is <PI>. The phase of zero is defined to be zero.  
If number is a complex float, the result is a float of the same type as the components of number. If number is a float, the result is a float of the same type. If number is a rational or a complex rational, the result is a single float.  
The branch cut for phase lies along the negative real axis, continuous with quadrant II. The range consists of that portion of the real axis between -<PI> (exclusive) and <PI> (inclusive).  
 The mathematical definition of phase is as follows:  
(phase x) = (atan (imagpart x) (realpart x))



### Examples
```lisp 
(phase 1) =>  0.0s0
 (phase 0) =>  0.0s0
 (phase (cis 30)) =>  -1.4159266
 (phase #c(0 1)) =>  1.5707964Side Effects: None.
```
