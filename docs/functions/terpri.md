<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function TERPRI, FRESH-LINE

### Syntax
`terpri &optional output-stream => nil`  
`fresh-line &optional output-stream => generalized-boolean`  


### Arguments and Values
- **output-stream** :  an output stream designator. The default is standard output.   
- **generalized-boolean** : a generalized boolean.   


### Description
terpri outputs a newline to output-stream.  
fresh-line is similar to terpri but outputs a newline only if the output-stream is not already at the start of a line. If for some reason this cannot be determined, then a newline is output anyway. fresh-line returns true if it outputs a newline; otherwise it returns false.



### Examples
```lisp 
(with-output-to-string (s)
    (write-string "some text" s)
    (terpri s)
    (terpri s)
    (write-string "more text" s))
=>  "some text

more text"
 (with-output-to-string (s)
    (write-string "some text" s)
    (fresh-line s)
    (fresh-line s)
    (write-string "more text" s))
=>  "some text
more text"Side Effects:
The output-stream is modified.
```
