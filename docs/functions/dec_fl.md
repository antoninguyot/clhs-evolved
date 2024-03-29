<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function DECODE-FLOAT, SCALE-FLOAT, FLOAT-RADIX, FLOAT-SIGN, FLOAT-DIGITS, FLOAT-PRECISION, INTEGER-DECODE-FLOAT

### Syntax
`decode-float float => significand, exponent, sign`  
`scale-float float integer => scaled-float`  
`float-radix float => float-radix`  
`float-sign float-1 &optional float-2 => signed-float`  
`float-digits float => digits1`  
`float-precision float => digits2`  
`integer-decode-float float => significand, exponent, integer-sign`  


### Arguments and Values
- **digits1** : a non-negative integer.   
- **digits2** : a non-negative integer.   
- **exponent** : an integer.   
- **float** : a float.   
- **float-1** : a float.   
- **float-2** : a float.   
- **float-radix** : an integer.   
- **integer** : a non-negative integer.   
- **integer-sign** : the integer -1, or the integer 1.   
- **scaled-float** : a float.   
- **sign** : A float of the same type as float but numerically equal to 1.0 or -1.0.   
- **signed-float** : a float.   
- **significand** : a float.   


### Description
decode-float computes three values that characterize float. The first value is of the same type as float and represents the significand. The second value represents the exponent to which the radix (notated in this description by b) must be raised to obtain the value that, when multiplied with the first result, produces the absolute value of float. If float is zero, any integer value may be returned, provided that the identity shown for scale-float holds. The third value is of the same type as float and is 1.0 if float is greater than or equal to zero or -1.0 otherwise.  
decode-float divides float by an integral power of b so as to bring its value between 1/b (inclusive) and 1 (exclusive), and returns the quotient as the first value. If float is zero, however, the result equals the absolute value of float (that is, if there is a negative zero, its significand is considered to be a positive zero).  
scale-float returns (* float (expt (float b float) integer)), where b is the radix of the floating-point representation. float is not necessarily between 1/b and 1.  
float-radix returns the radix of float.  
float-sign returns a number z such that z and float-1 have the same sign and also such that z and float-2 have the same absolute value. If float-2 is not supplied, its value is (float 1 float-1). If an implementation has distinct representations for negative zero and positive zero, then (float-sign -0.0) =>  -1.0.  
float-digits returns the number of radix b digits used in the representation of float (including any implicit digits, such as a ``hidden bit'').  
float-precision returns the number of significant radix b digits present in float; if float is a float zero, then the result is an integer zero.  
For normalized floats, the results of float-digits and float-precision are the same, but the precision is less than the number of representation digits for a denormalized or zero number.  
integer-decode-float computes three values that characterize float - the significand scaled so as to be an integer, and the same last two values that are returned by decode-float. If float is zero, integer-decode-float returns zero as the first value. The second value bears the same relationship to the first value as for decode-float:  
 (multiple-value-bind (signif expon sign)  
                      (integer-decode-float f)  
   (scale-float (float signif f) expon)) ==  (abs f)



### Examples
```lisp 
;; Note that since the purpose of this functionality is to expose
 ;; details of the implementation, all of these examples are necessarily
 ;; very implementation-dependent.  Results may vary widely.
 ;; Values shown here are chosen consistently from one particular implementation.
 (decode-float .5) =>  0.5, 0, 1.0
 (decode-float 1.0) =>  0.5, 1, 1.0
 (scale-float 1.0 1) =>  2.0
 (scale-float 10.01 -2) =>  2.5025
 (scale-float 23.0 0) =>  23.0
 (float-radix 1.0) =>  2
 (float-sign 5.0) =>  1.0
 (float-sign -5.0) =>  -1.0
 (float-sign 0.0) =>  1.0
 (float-sign 1.0 0.0) =>  0.0
 (float-sign 1.0 -10.0) =>  10.0
 (float-sign -1.0 10.0) =>  -10.0
 (float-digits 1.0) =>  24
 (float-precision 1.0) =>  24
 (float-precision least-positive-single-float) =>  1
 (integer-decode-float 1.0) =>  8388608, -23, 1Side Effects: None.
```
