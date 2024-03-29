<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro WITH-INPUT-FROM-STRING

### Syntax
`with-input-from-string (var string &key index start end) declaration* form* => result*`  


### Arguments and Values


### Description
Creates an  input string stream,  provides an opportunity to perform operations on the stream (returning zero or more values), and then closes the string stream.  
String is evaluated first, and var is bound to a character input string stream that supplies characters from the subsequence of the resulting string bounded by start and end. The body is executed as an implicit progn.  
The input string stream is automatically closed on exit from with-input-from-string, no matter whether the exit is normal or abnormal.  The input string stream to which the variable var is bound has dynamic extent; its extent ends when the form is exited.  
The index is a pointer within the string to be advanced. If with-input-from-string is exited normally, then index will have as its value the index into the string indicating the first character not read which is (length string) if all characters were used. The place specified by index is not updated as reading progresses, but only at the end of the operation.  
start and index may both specify the same variable, which is a pointer within the string to be advanced, perhaps repeatedly by some containing loop.  
 The consequences are undefined if an attempt is made to assign the variable var.



### Examples
```lisp 
(with-input-from-string (s "XXX1 2 3 4xxx"
                             :index ind
                             :start 3 :end 10)
    (+ (read s) (read s) (read s))) =>  6
 ind =>  9
 (with-input-from-string (s "Animal Crackers" :index j :start 6)
   (read s)) =>  CRACKERSSide Effects:
The value of the place named by index, if any, is modified.
```
