<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function SET-DISPATCH-MACRO-CHARACTER, GET-DISPATCH-MACRO-CHARACTER

### Syntax
`get-dispatch-macro-character disp-char sub-char &optional readtable => function`  
`set-dispatch-macro-character disp-char sub-char new-function &optional readtable => t`  


### Arguments and Values
- **disp-char** : a character.   
- **sub-char** : a character.   
- **readtable** : a readtable designator.  The default is the current readtable.   
- **function** : a function designator or nil.   
- **new-function** : a function designator.   


### Description
set-dispatch-macro-character causes new-function to be called when disp-char followed by sub-char is read. If sub-char is a lowercase letter, it is converted to its uppercase equivalent. It is an error if sub-char is one of the ten decimal digits.  
set-dispatch-macro-character installs a new-function to be called when a particular dispatching macro character pair is read. New-function is installed as the dispatch function to be called when readtable is in use and when disp-char is followed by sub-char.  
For more information about how the new-function is invoked, see Section 2.1.4.4 (Macro Characters).  
get-dispatch-macro-character retrieves the dispatch function associated with disp-char and sub-char in readtable.  
get-dispatch-macro-character returns the macro-character function for sub-char under disp-char, or nil if there is no function associated with sub-char. If sub-char is a decimal digit, get-dispatch-macro-character returns nil.



### Examples
```lisp 
(get-dispatch-macro-character #\# #\{) =>  NIL
 (set-dispatch-macro-character #\# #\{        ;dispatch on #{
    #'(lambda(s c n)
        (let ((list (read s nil (values) t)))  ;list is object after #n{
          (when (consp list)                   ;return nth element of list
            (unless (and n (< 0 n (length list))) (setq n 0))
            (setq list (nth n list)))
         list))) =>  T
 #{(1 2 3 4) =>  1
 #3{(0 1 2 3) =>  3
 #{123 =>  123
(defun |#$-reader| (stream subchar arg)
   (declare (ignore subchar arg))
   (list 'dollars (read stream t nil t))) =>  |#$-reader|
 (set-dispatch-macro-character #\# #\$ #'|#$-reader|) =>  TSee Also:
Section 2.1.4.4 (Macro Characters)Side Effects:
The readtable is modified.
```
