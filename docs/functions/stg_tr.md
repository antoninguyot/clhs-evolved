<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function STRING-TRIM, STRING-LEFT-TRIM, STRING-RIGHT-TRIM

### Syntax
`string-trim character-bag string => trimmed-string`  
`string-left-trim character-bag string => trimmed-string`  
`string-right-trim character-bag string => trimmed-string`  


### Arguments and Values
- **character-bag** : a sequence containing characters.   
- **string** : a string designator.   
- **trimmed-string** : a string.   


### Description
string-trim returns a substring of string, with all characters in character-bag stripped off the beginning and end. string-left-trim is similar but strips characters off only the beginning; string-right-trim strips off only the end.  
If no characters need to be trimmed from the string, then either string itself or a copy of it may be returned, at the discretion of the implementation.  
All of these functions observe the fill pointer.



### Examples
```lisp 
(string-trim "abc" "abcaakaaakabcaaa") =>  "kaaak"
 (string-trim '(#\Space #\Tab #\Newline) " garbanzo beans
        ") =>  "garbanzo beans"
 (string-trim " (*)" " ( *three (silly) words* ) ")
=>  "three (silly) words"

 (string-left-trim "abc" "labcabcabc") =>  "labcabcabc"
 (string-left-trim " (*)" " ( *three (silly) words* ) ")
=>  "three (silly) words* ) "

 (string-right-trim " (*)" " ( *three (silly) words* ) ") 
=>  " ( *three (silly) words"Side Effects: None.
```
