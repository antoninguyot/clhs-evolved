<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function CHAR-UPCASE, CHAR-DOWNCASE

### Syntax
`char-upcase character => corresponding-character`  
`char-downcase character => corresponding-character`  


### Arguments and Values
- **character, corresponding-character** : a character.   


### Description
If character is a lowercase character, char-upcase returns the corresponding uppercase character. Otherwise, char-upcase just returns the given character.  
If character is an uppercase character, char-downcase returns the corresponding lowercase character. Otherwise, char-downcase just returns the given character.  
 The result only ever differs from character in its code attribute; all implementation-defined attributes are preserved.



### Examples
```lisp 
(char-upcase #\a) =>  #\A
 (char-upcase #\A) =>  #\A
 (char-downcase #\a) =>  #\a
 (char-downcase #\A) =>  #\a
 (char-upcase #\9) =>  #\9
 (char-downcase #\9) =>  #\9
 (char-upcase #\@) =>  #\@
 (char-downcase #\@) =>  #\@
 ;; Note that this next example might run for a very long time in 
 ;; some implementations if CHAR-CODE-LIMIT happens to be very large
 ;; for that implementation.
 (dotimes (code char-code-limit)
   (let ((char (code-char code)))
     (when char
       (unless (cond ((upper-case-p char) (char= (char-upcase (char-downcase char)) char))
                     ((lower-case-p char) (char= (char-downcase (char-upcase char)) char))
                     (t (and (char= (char-upcase (char-downcase char)) char)
                             (char= (char-downcase (char-upcase char)) char))))
         (return char)))))
=>  NIL
```
