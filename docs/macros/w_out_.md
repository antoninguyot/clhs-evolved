<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro WITH-OUTPUT-TO-STRING

### Syntax
`with-output-to-string (var &optional string-form &key element-type) declaration* form* => result*`  


### Arguments and Values
- **var** : a variable name.   
- **string-form** : a form or nil; if non-nil, evaluated to produce string.   
- **string** : a string that has a fill pointer.   
- **element-type** : a type specifier; evaluated.  The default is character.   
- **declaration** : a declare expression; not evaluated.   
- **forms** : an implicit progn.   
- **results** : If a string-form is not supplied or nil, a string; otherwise, the values returned by the forms.   


### Description
with-output-to-string creates a  character output stream, performs a series of operations that may send results to this stream, and then closes the stream.  
 The element-type names the type of the elements of the stream; a stream is constructed of the most specialized type that can accommodate elements of the given type.  
The body is executed as an implicit progn with var bound to an output string stream. All output to that string stream is saved in a string.  
 If string is supplied, element-type is ignored, and the output is incrementally appended to string as if by use of vector-push-extend.  
The output stream is automatically closed on exit from with-output-from-string, no matter whether the exit is normal or abnormal.  The output string stream to which the variable var is bound has dynamic extent; its extent ends when the form is exited.  
If no string is provided, then with-output-from-string  produces a stream that accepts characters and returns a string of the indicated element-type.  If string is provided, with-output-to-string returns the results of evaluating the last form.  
 The consequences are undefined if an attempt is made to assign the variable var.



### Examples
```lisp 
(setq fstr (make-array '(0) :element-type 'base-char
                             :fill-pointer 0 :adjustable t)) =>  ""
 (with-output-to-string (s fstr)
    (format s "here's some output")
    (input-stream-p s)) =>  false
 fstr =>  "here's some output"Side Effects:
The string is modified.
```
