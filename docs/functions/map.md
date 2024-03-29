<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MAP

### Syntax
`map result-type function &rest sequences+ => result`  


### Arguments and Values
- **result-type** :  a sequence type specifier, or nil.   
- **function** : a function designator. function must take as many arguments as there are sequences.   
- **sequence** : a proper sequence.   
- **result** : if result-type is a type specifier other than nil, then a sequence of the type it denotes; otherwise (if the result-type is nil), nil.   


### Description
Applies function to successive sets of arguments in which one argument is obtained from each sequence. The function is called first on all the elements with index 0, then on all those with index 1, and so on. The result-type specifies the type of the resulting sequence.  
map returns nil if result-type is nil. Otherwise, map returns a sequence such that element j is the result of applying function to element j of each of the sequences. The result sequence is as long as the shortest of the sequences. The consequences are undefined if the result of applying function to the successive elements of the sequences cannot be contained in a sequence of the type given by result-type.  
 If the result-type is a subtype of list, the result will be a list.  
If the result-type is a subtype of vector, then if the implementation can determine the element type specified for the result-type, the element type of the resulting array is the result of upgrading that element type; or, if the implementation can determine that the element type is unspecified (or *), the element type of the resulting array is t; otherwise, an error is signaled.



### Examples
```lisp 
(map 'string #'(lambda (x y)
                  (char "01234567890ABCDEF" (mod (+ x y) 16)))
       '(1 2 3 4)
       '(10 9 8 7)) =>  "AAAA"
 (setq seq '("lower" "UPPER" "" "123")) =>  ("lower" "UPPER" "" "123")
 (map nil #'nstring-upcase seq) =>  NIL
 seq =>  ("LOWER" "UPPER" "" "123")
 (map 'list #'- '(1 2 3 4)) =>  (-1 -2 -3 -4)
 (map 'string
      #'(lambda (x) (if (oddp x) #\1 #\0))
      '(1 2 3 4)) =>  "1010"
 (map '(vector * 4) #'cons "abc" "de") should signal an error
```
