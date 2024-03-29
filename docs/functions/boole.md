<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function BOOLE

### Syntax
`boole op integer-1 integer-2 => result-integer`  


### Arguments and Values
- **Op** : a bit-wise logical operation specifier.   
- **integer-1** : an integer.   
- **integer-2** : an integer.   
- **result-integer** : an integer.   


### Description
boole performs bit-wise logical operations on integer-1 and integer-2, which are treated as if they were binary and in two's complement representation.  
The operation to be performed and the return value are determined by op.  
boole returns the values specified for any op in the next figure.  
Op           Result                                        
boole-1      integer-1                                     
boole-2      integer-2                                     
boole-andc1  and complement of integer-1 with integer-2    
boole-andc2  and integer-1 with complement of integer-2    
boole-and    and                                           
boole-c1     complement of integer-1                       
boole-c2     complement of integer-2                       
boole-clr    always 0 (all zero bits)                      
boole-eqv    equivalence (exclusive nor)                   
boole-ior    inclusive or                                  
boole-nand   not-and                                       
boole-nor    not-or                                        
boole-orc1   or complement of integer-1 with integer-2     
boole-orc2   or integer-1 with complement of integer-2     
boole-set    always -1 (all one bits)                      
boole-xor    exclusive orFigure 12-17.  Bit-Wise Logical Operations



### Examples
```lisp 
(boole boole-ior 1 16) =>  17
 (boole boole-and -2 5) =>  4
 (boole boole-eqv 17 15) =>  -31

;;; These examples illustrate the result of applying BOOLE and each
;;; of the possible values of OP to each possible combination of bits.
 (progn
   (format t "~&Results of (BOOLE <op> #b0011 #b0101) ...~
           ~%---Op-------Decimal-----Binary----Bits---~%")
   (dolist (symbol '(boole-1     boole-2    boole-and  boole-andc1
                     boole-andc2 boole-c1   boole-c2   boole-clr
                     boole-eqv   boole-ior  boole-nand boole-nor
                     boole-orc1  boole-orc2 boole-set  boole-xor))
     (let ((result (boole (symbol-value symbol) #b0011 #b0101)))
       (format t "~& ~A~13T~3,' D~23T~:*~5,' B~31T ...~4,'0B~%" 
               symbol result (logand result #b1111)))))
>>  Results of (BOOLE <op> #b0011 #b0101) ...
>>  ---Op-------Decimal-----Binary----Bits---
>>   BOOLE-1       3          11    ...0011
>>   BOOLE-2       5         101    ...0101
>>   BOOLE-AND     1           1    ...0001
>>   BOOLE-ANDC1   4         100    ...0100
>>   BOOLE-ANDC2   2          10    ...0010
>>   BOOLE-C1     -4        -100    ...1100
>>   BOOLE-C2     -6        -110    ...1010
>>   BOOLE-CLR     0           0    ...0000
>>   BOOLE-EQV    -7        -111    ...1001
>>   BOOLE-IOR     7         111    ...0111
>>   BOOLE-NAND   -2         -10    ...1110
>>   BOOLE-NOR    -8       -1000    ...1000
>>   BOOLE-ORC1   -3         -11    ...1101
>>   BOOLE-ORC2   -5        -101    ...1011
>>   BOOLE-SET    -1          -1    ...1111
>>   BOOLE-XOR     6         110    ...0110
=>  NIL
```
