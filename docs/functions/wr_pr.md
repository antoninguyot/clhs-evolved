<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function WRITE, PRIN1, PRINT, PPRINT, PRINC

### Syntax
`write object &key array base case circle escape gensym length level lines miser-width pprint-dispatch pretty radix readably right-margin stream => object`  
`prin1 object &optional output-stream => object`  
`princ object &optional output-stream => object`  
`print object &optional output-stream => object`  
`pprint object &optional output-stream => <no values>`  


### Arguments and Values
- **object** : an object.   
- **output-stream** : an output stream designator. The default is standard output.   
- **array** : a generalized boolean.   
- **base** : a radix.   
- **case** : a symbol of type (member :upcase :downcase :capitalize).   
- **circle** : a generalized boolean.   
- **escape** : a generalized boolean.   
- **gensym** : a generalized boolean.   
- **length** : a non-negative integer, or nil.   
- **level** : a non-negative integer, or nil.   
- **lines** : a non-negative integer, or nil.   
- **miser-width** : a non-negative integer, or nil.   
- **pprint-dispatch** : a pprint dispatch table.   
- **pretty** : a generalized boolean.   
- **radix** : a generalized boolean.   
- **readably** : a generalized boolean.   
- **right-margin** : a non-negative integer, or nil.   
- **stream** : an output stream designator. The default is standard output.   


### Description
write, prin1, princ, print, and pprint write the printed representation of object to output-stream.  
write is the general entry point to the Lisp printer. For each explicitly supplied keyword parameter named in the next figure, the corresponding printer control variable is dynamically bound to its value while printing goes on; for each keyword parameter in the next figure that is not explicitly supplied, the value of the corresponding printer control variable is the same as it was at the time write was invoked. Once the appropriate bindings are established, the object is output by the Lisp printer.  
Parameter        Corresponding Dynamic Variable    
array            *print-array*                     
base             *print-base*                      
case             *print-case*                      
circle           *print-circle*                    
escape           *print-escape*                    
gensym           *print-gensym*                    
length           *print-length*                    
level            *print-level*                     
lines            *print-lines*                     
miser-width      *print-miser-width*               
pprint-dispatch  *print-pprint-dispatch*           
pretty           *print-pretty*                    
radix            *print-radix*                     
readably         *print-readably*                  
right-margin     *print-right-margin*Figure 22-7.  Argument correspondences for the WRITE function.  
 prin1, princ, print, and pprint implicitly bind certain print parameters to particular values. The remaining parameter values are taken from *print-array*, *print-base*, *print-case*, *print-circle*, *print-escape*, *print-gensym*, *print-length*, *print-level*, *print-lines*, *print-miser-width*, *print-pprint-dispatch*, *print-pretty*, *print-radix*, and *print-right-margin*.  
prin1 produces output suitable for input to read. It binds *print-escape* to true.  
princ is just like prin1 except that the output has no escape characters. It binds *print-escape* to false  and *print-readably* to false.  The general rule is that output from princ is intended to look good to people, while output from prin1 is intended to be acceptable to read.  
print is just like prin1 except that the printed representation of object is preceded by a newline and followed by a space.  
pprint is just like print except that the trailing space is omitted and object is printed with the *print-pretty* flag non-nil to produce pretty output.  
Output-stream specifies the stream to which output is to be sent.



### Examples
No example  
