<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function BIT-AND, BIT-ANDC1, BIT-ANDC2, BIT-EQV, BIT-IOR, BIT-NAND, BIT-NOR, BIT-NOT, BIT-ORC1, BIT-ORC2, BIT-XOR

### Syntax
`bit-and bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-andc1 bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-andc2 bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-eqv bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-ior bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-nand bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-nor bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-orc1 bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-orc2 bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-xor bit-array1 bit-array2 &optional opt-arg => resulting-bit-array`  
`bit-not bit-array &optional opt-arg => resulting-bit-array`  


### Arguments and Values


### Description
These functions perform bit-wise logical operations on bit-array1 and bit-array2 and return an array of matching rank and dimensions, such that any given bit of the result is produced by operating on corresponding bits from each of the arguments.  
In the case of bit-not, an array of rank and dimensions matching bit-array is returned that contains a copy of bit-array with all the bits inverted.  
If opt-arg is of type (array bit) the contents of the result are destructively placed into opt-arg. If opt-arg is the symbol t, bit-array or bit-array1 is replaced with the result; if opt-arg is nil or omitted, a new array is created to contain the result.  
The next figure indicates the logical operation performed by each of the functions.  
                                                                                                         
Function                                                 Operation                                       
----------  
                                                                                                         
                                                           
bit-and                                                  and                                             
bit-eqv                                                  equivalence (exclusive nor)                     
bit-not                                                  complement                                      
bit-ior                                                  inclusive or                                    
bit-xor                                                  exclusive or                                    
bit-nand                                                 complement of bit-array1 and bit-array2         
bit-nor                                                  complement of bit-array1 or bit-array2          
bit-andc1                                                and complement of bit-array1 with bit-array2    
bit-andc2                                                and bit-array1 with complement of bit-array2    
bit-orc1                                                 or complement of bit-array1 with bit-array2     
bit-orc2                                                 or bit-array1 with complement of bit-array2     
                                                                                                         
Figure 15-4.  Bit-wise Logical Operations on Bit Arrays



### Examples
```lisp 
(bit-and (setq ba #*11101010) #*01101011) =>  #*01101010
 (bit-and #*1100 #*1010) =>  #*1000      
 (bit-andc1 #*1100 #*1010) =>  #*0010
 (setq rba (bit-andc2 ba #*00110011 t)) =>  #*11001000
 (eq rba ba) =>  true
 (bit-not (setq ba #*11101010)) =>  #*00010101
 (setq rba (bit-not ba 
                     (setq tba (make-array 8 
                                           :element-type 'bit))))
=>  #*00010101
 (equal rba tba) =>  true
 (bit-xor #*1100 #*1010) =>  #*0110
```
