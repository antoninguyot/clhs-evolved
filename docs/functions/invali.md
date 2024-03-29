<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function INVALID-METHOD-ERROR

### Syntax
`invalid-method-error method format-control &rest args => implementation-dependent`  


### Arguments and Values
- **method** : a method.   
- **format-control** : a format control.   
- **args** : format arguments for the format-control.   


### Description
The function invalid-method-error is used to signal an error of type error when there is an applicable method whose qualifiers are not valid for the method combination type. The error message is constructed by using the format-control suitable for format and any args to it. Because an implementation may need to add additional contextual information to the error message, invalid-method-error should be called only within the dynamic extent of a method combination function.  
The function invalid-method-error is called automatically when a method fails to satisfy every qualifier pattern and predicate in a define-method-combination form. A method combination function that imposes additional restrictions should call invalid-method-error explicitly if it encounters a method it cannot accept.  
Whether invalid-method-error returns to its caller or exits via throw is implementation-dependent.Examples: None.Side Effects:  
The debugger might be entered.



### Examples
No example  
