<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function UNREAD-CHAR

### Syntax
`unread-char character &optional input-stream => nil`  


### Arguments and Values
- **character** : a character; must be the last character that was read from input-stream.   
- **input-stream** : an input stream designator. The default is standard input.   


### Description
unread-char places character back onto the front of input-stream so that it will again be the next character in input-stream.  
 When input-stream is an echo stream, no attempt is made to undo any echoing of the character that might already have been done on input-stream. However, characters placed on input-stream by unread-char are marked in such a way as to inhibit later re-echo by read-char.  
It is an error to invoke unread-char twice consecutively on the same stream without an intervening call to read-char (or some other input operation which implicitly reads characters) on that stream.  
 Invoking peek-char or read-char commits all previous characters. The consequences of invoking unread-char on any character preceding that which is returned by peek-char (including those passed over by peek-char that has a non-nil peek-type) are unspecified. In particular, the consequences of invoking unread-char after peek-char are unspecified.



### Examples
```lisp 
(with-input-from-string (is "0123")
    (dotimes (i 6)
      (let ((c (read-char is)))
        (if (evenp i) (format t "~&~S ~S~%" i c) (unread-char c is)))))
>>  0 #\0
>>  2 #\1
>>  4 #\2
=>  NIL
```
