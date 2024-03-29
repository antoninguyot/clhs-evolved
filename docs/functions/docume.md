<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Standard Generic Function DOCUMENTATION, (SETF DOCUMENTATION)

### Syntax
`documentation x doc-type => documentation`  
`(setf documentation) new-value x doc-type => new-valueArgument Precedence Order:`  
`doc-type, objectMethod Signatures:`  
`Functions, Macros, and Special Forms:`  
`documentation (x function) (doc-type (eql 't))`  
`documentation (x function) (doc-type (eql 'function))`  
`documentation (x list) (doc-type (eql 'function))`  
`documentation (x list) (doc-type (eql 'compiler-macro))`  
`documentation (x symbol) (doc-type (eql 'function))`  
`documentation (x symbol) (doc-type (eql 'compiler-macro))`  
`documentation (x symbol) (doc-type (eql 'setf))`  
`(setf documentation) new-value (x function) (doc-type (eql 't))`  
`(setf documentation) new-value (x function) (doc-type (eql 'function))`  
`(setf documentation) new-value (x list) (doc-type (eql 'function))`  
`(setf documentation) new-value (x list) (doc-type (eql 'compiler-macro))`  
`(setf documentation) new-value (x symbol) (doc-type (eql 'function))`  
`(setf documentation) new-value (x symbol) (doc-type (eql 'compiler-macro))`  
`(setf documentation) new-value (x symbol) (doc-type (eql 'setf))`  
`Method Combinations:`  
`documentation (x method-combination) (doc-type (eql 't))`  
`documentation (x method-combination) (doc-type (eql 'method-combination))`  
`documentation (x symbol) (doc-type (eql 'method-combination))`  
`(setf documentation) new-value (x method-combination) (doc-type (eql 't))`  
`(setf documentation) new-value (x method-combination) (doc-type (eql 'method-combination))`  
`(setf documentation) new-value (x symbol) (doc-type (eql 'method-combination))`  
`Methods:`  
`documentation (x standard-method) (doc-type (eql 't))`  
`(setf documentation) new-value (x standard-method) (doc-type (eql 't))`  
`Packages:`  
`documentation (x package) (doc-type (eql 't))`  
`(setf documentation) new-value (x package) (doc-type (eql 't))`  
`Types, Classes, and Structure Names:`  
`documentation (x standard-class) (doc-type (eql 't))`  
`documentation (x standard-class) (doc-type (eql 'type))`  
`documentation (x structure-class) (doc-type (eql 't))`  
`documentation (x structure-class) (doc-type (eql 'type))`  
`documentation (x symbol) (doc-type (eql 'type))`  
`documentation (x symbol) (doc-type (eql 'structure))`  
`(setf documentation) new-value (x standard-class) (doc-type (eql 't))`  
`(setf documentation) new-value (x standard-class) (doc-type (eql 'type))`  
`(setf documentation) new-value (x structure-class) (doc-type (eql 't))`  
`(setf documentation) new-value (x structure-class) (doc-type (eql 'type))`  
`(setf documentation) new-value (x symbol) (doc-type (eql 'type))`  
`(setf documentation) new-value (x symbol) (doc-type (eql 'structure))`  
`Variables:`  
`documentation (x symbol) (doc-type (eql 'variable))`  
`(setf documentation) new-value (x symbol) (doc-type (eql 'variable))`  


### Arguments and Values
- **x** : an object.   
- **doc-type** : a symbol.   
- **documentation** : a string, or nil.   
- **new-value** : a string.   


### Description
The generic function documentation returns the documentation string associated with the given object if it is available; otherwise it returns nil.  
The generic function (setf documentation) updates the documentation string associated with x to new-value. If x is a list, it must be of the form (setf symbol).  
Documentation strings are made available for debugging purposes. Conforming programs are permitted to use documentation strings when they are present, but should not depend for their correct behavior on the presence of those documentation strings. An implementation is permitted to discard documentation strings at any time for implementation-defined reasons.  
The nature of the documentation string returned depends on the doc-type, as follows:  
If x is a function, returns the documentation string associated with x.  
If x is a method combination, returns the documentation string associated with x.  
If x is a structure class or standard class, returns the documentation string associated with the class x.  
A conforming implementation or a conforming program may extend the set of symbols that are acceptable as the doc-type.Examples: None.



### Examples
No example  
