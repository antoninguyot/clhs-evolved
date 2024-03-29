<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function STREAM-ELEMENT-TYPE

### Syntax
`stream-element-type stream => typespec`  


### Arguments and Values
- **stream** : a stream.   
- **typespec** : a type specifier.   


### Description
stream-element-type returns a type specifier that indicates the types of objects that may be read from or written to stream.  
Streams created by open have an element type restricted to integer or a subtype of type character.



### Examples
```lisp 
;; Note that the stream must accomodate at least the specified type,
;; but might accomodate other types.  Further note that even if it does
;; accomodate exactly the specified type, the type might be specified in
;; any of several ways.
 (with-open-file (s "test" :element-type '(integer 0 1)
                           :if-exists :error
                           :direction :output)
   (stream-element-type s))
=>  INTEGER
OR=>  (UNSIGNED-BYTE 16)
OR=>  (UNSIGNED-BYTE 8)
OR=>  BIT
OR=>  (UNSIGNED-BYTE 1)
OR=>  (INTEGER 0 1)
OR=>  (INTEGER 0 (2))Side Effects: None.
```
