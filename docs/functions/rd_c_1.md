<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function READ-CHAR-NO-HANG

### Syntax
`read-char-no-hang &optional input-stream eof-error-p eof-value recursive-p => char`  


### Arguments and Values
- **input-stream** :  an input stream designator. The default is standard input.   
- **eof-error-p** : a generalized boolean. The default is true.   
- **eof-value** : an object. The default is nil.   
- **recursive-p** : a generalized boolean. The default is false.   
- **char** : a character or nil or the eof-value.   


### Description
read-char-no-hang returns a character from input-stream if such a character is available. If no character is available, read-char-no-hang returns nil.  
 If recursive-p is true, this call is expected to be embedded in a higher-level call to read or a similar function used by the Lisp reader.  
If an end of file[2] occurs and eof-error-p is false, eof-value is returned.



### Examples
```lisp 
;; This code assumes an implementation in which a newline is not
;; required to terminate input from the console.
 (defun test-it ()
   (unread-char (read-char))
   (list (read-char-no-hang) 
         (read-char-no-hang) 
         (read-char-no-hang)))
=>  TEST-IT
;; Implementation A, where a Newline is not required to terminate
;; interactive input on the console.
 (test-it)
>>  a
=>  (#\a NIL NIL)
;; Implementation B, where a Newline is required to terminate
;; interactive input on the console, and where that Newline remains
;; on the input stream.
 (test-it)
>>  a<NEWLINE>
=>  (#\a #\Newline NIL)
```
