<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function FILE-LENGTH

### Syntax
`file-length stream => length`  


### Arguments and Values
- **stream** : a stream associated with a file.   
- **length** : a non-negative integer or nil.   


### Description
file-length returns the length of stream, or nil if the length cannot be determined.  
For a binary file, the length is measured in units of the element type of the stream.



### Examples
```lisp 
(with-open-file (s "decimal-digits.text" 
                    :direction :output :if-exists :error)
   (princ "0123456789" s)
   (truename s))
=>  #P"A:>Joe>decimal-digits.text.1"
 (with-open-file (s "decimal-digits.text")
   (file-length s))
=>  10Side Effects: None.
```
