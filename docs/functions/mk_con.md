<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MAKE-CONCATENATED-STREAM

### Syntax
`make-concatenated-stream &rest input-streams => concatenated-stream`  


### Arguments and Values
- **input-stream** : an input stream.   
- **concatenated-stream** : a concatenated stream.   


### Description
Returns a concatenated stream that has the indicated input-streams initially associated with it.



### Examples
```lisp 
(read (make-concatenated-stream
         (make-string-input-stream "1")
         (make-string-input-stream "2"))) =>  12Side Effects: None.
```
