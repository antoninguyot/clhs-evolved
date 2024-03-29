<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro WITH-OPEN-STREAM

### Syntax
`with-open-stream (var stream) declaration* form* => result*`  


### Arguments and Values
- **var** : a variable name.   
- **stream** : a form; evaluated to produce a stream.   
- **declaration** : a declare expression; not evaluated.   
- **forms** : an implicit progn.   
- **results** : the values returned by the forms.   


### Description
with-open-stream performs a series of operations on stream, returns a value, and then closes the stream.  
Var is bound to the value of stream, and then forms are executed as an implicit progn. stream is automatically closed on exit from with-open-stream, no matter whether the exit is normal or abnormal.  The stream has dynamic extent; its extent ends when the form is exited.  
 The consequences are undefined if an attempt is made to assign the the variable var with the forms.



### Examples
```lisp 
(with-open-stream (s (make-string-input-stream "1 2 3 4"))
    (+ (read s) (read s) (read s))) =>  6Side Effects:
The stream is closed (upon exit).
```
