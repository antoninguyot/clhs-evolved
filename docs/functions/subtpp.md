<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function SUBTYPEP

### Syntax
`subtypep type-1 type-2 &optional environment => subtype-p, valid-p`  


### Arguments and Values
- **type-1** : a type specifier.   
- **type-2** : a type specifier.   
- **environment** : an environment object. The default is nil, denoting the null lexical environment and the current global environment.   
- **subtype-p** : a generalized boolean.   
- **valid-p** : a generalized boolean.   


### Description
If type-1 is a recognizable subtype of type-2, the first value is true. Otherwise, the first value is false, indicating that either type-1 is not a subtype of type-2, or else type-1 is a subtype of type-2 but is not a recognizable subtype.  
A second value is also returned indicating the `certainty' of the first value. If this value is true, then the first value is an accurate indication of the subtype relationship. (The second value is always true when the first value is true.)  
The next figure summarizes the possible combinations of values that might result.  
Value 1  Value 2  Meaning                                                 
true     true     type-1 is definitely a subtype of type-2.               
false    true     type-1 is definitely not a subtype of type-2.           
false    false    subtypep could not determine the relationship,          
                  so type-1 might or might not be a subtype of type-2.Figure 4-9.  Result possibilities for subtypep  
subtypep is permitted to return the values false and false only when at least one argument involves one of these type specifiers: and, eql, the list form of function, member, not, or, satisfies, or values. (A type specifier `involves' such a symbol if, after being type expanded, it contains that symbol in a position that would call for its meaning as a type specifier to be used.) One consequence of this is that if neither type-1 nor type-2 involves any of these type specifiers, then subtypep is obliged to determine the relationship accurately. In particular, subtypep returns the values true and true if the arguments are equal and do not involve any of these type specifiers.  
subtypep never returns a second value of nil when both type-1 and type-2 involve only the names in Figure 4-2, or names of types defined by defstruct, define-condition, or defclass, or derived types that expand into only those names. While type specifiers listed in Figure 4-2 and names of defclass and defstruct can in some cases be implemented as derived types, subtypep regards them as primitive.  
The relationships between types reflected by subtypep are those specific to the particular implementation. For example, if an implementation supports only a single type of floating-point numbers, in that implementation (subtypep 'float 'long-float) returns the values true and true (since the two types are identical).  
 For all T1 and T2 other than *, (array T1) and (array T2) are two different type specifiers that always refer to the same sets of things if and only if they refer to arrays of exactly the same specialized representation, i.e., if (upgraded-array-element-type 'T1) and (upgraded-array-element-type 'T2) return two different type specifiers that always refer to the same sets of objects. This is another way of saying that `(array type-specifier) and `(array ,(upgraded-array-element-type 'type-specifier)) refer to the same set of specialized array representations. For all T1 and T2 other than *, the intersection of (array T1) and (array T2) is the empty set if and only if they refer to arrays of different, distinct specialized representations.  
Therefore,  
 (subtypep '(array T1) '(array T2)) =>  true  
 (upgraded-array-element-type 'T1)  and  
 (upgraded-array-element-type 'T2)  
return two different type specifiers that always refer to the same sets of objects.  
For all type-specifiers T1 and T2 other than *,  
 (subtypep '(complex T1) '(complex T2)) =>  true, true  
if:  
The form  
 (subtypep '(complex single-float) '(complex float))  
 (subtypep '(array single-float) '(array float))  
returns true only in implementations that do not have a specialized array representation for single floats distinct from that for other floats.



### Examples
```lisp 
(subtypep 'compiled-function 'function) =>  true, true
 (subtypep 'null 'list) =>  true, true
 (subtypep 'null 'symbol) =>  true, true
 (subtypep 'integer 'string) =>  false, true
 (subtypep '(satisfies dummy) nil) =>  false, implementation-dependent
 (subtypep '(integer 1 3) '(integer 1 4)) =>  true, true
 (subtypep '(integer (0) (0)) 'nil) =>  true, true
 (subtypep 'nil '(integer (0) (0))) =>  true, true
 (subtypep '(integer (0) (0)) '(member)) =>  true, true ;or false, false
 (subtypep '(member) 'nil) =>  true, true ;or false, false
 (subtypep 'nil '(member)) =>  true, true ;or false, false
 Let <aet-x> and <aet-y> be two distinct type specifiers that do not always refer to the same sets of objects in a given implementation, but for which make-array, will return an object of the same array type.
Thus, in each case,
  (subtypep (array-element-type (make-array 0 :element-type '<aet-x>))
            (array-element-type (make-array 0 :element-type '<aet-y>)))
=>  true, true
 
  (subtypep (array-element-type (make-array 0 :element-type '<aet-y>))
            (array-element-type (make-array 0 :element-type '<aet-x>)))
=>  true, true
If (array <aet-x>) and (array <aet-y>) are different names for exactly the same set of objects, these names should always refer to the same sets of objects. That implies that the following set of tests are also true:
 (subtypep '(array <aet-x>) '(array <aet-y>)) =>  true, true
 (subtypep '(array <aet-y>) '(array <aet-x>)) =>  true, trueSide Effects: None.
```
