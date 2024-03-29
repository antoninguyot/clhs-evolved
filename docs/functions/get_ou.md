<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function GET-OUTPUT-STREAM-STRING

### Syntax
`get-output-stream-string string-output-stream => string`  


### Arguments and Values
- **string-output-stream** : a stream.   
- **string** : a string.   


### Description
Returns a string containing, in order, all the characters that have been output to string-output-stream. This operation clears any characters on string-output-stream, so the string contains only those characters which have been output since the last call to get-output-stream-string or since the creation of the string-output-stream, whichever occurred most recently.



### Examples
```lisp 
(setq a-stream (make-string-output-stream)
        a-string "abcdefghijklm") =>  "abcdefghijklm"
 (write-string a-string a-stream) =>  "abcdefghijklm"
 (get-output-stream-string a-stream) =>  "abcdefghijklm"
 (get-output-stream-string a-stream) =>  ""Side Effects:
The string-output-stream is cleared.
```
