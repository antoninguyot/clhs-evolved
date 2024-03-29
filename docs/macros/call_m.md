<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Local Macro CALL-METHOD, MAKE-METHOD

### Syntax
`call-method method &optional next-method-list => result*`  
`make-method form => method-object`  


### Arguments and Values
- **method** : a method object, or a list (see below); not evaluated.   
- **method-object** : a method object.   
- **next-method-list** : a list of method objects; not evaluated.   
- **results** : the values returned by the method invocation.   


### Description
The macro call-method is used in method combination. It hides the implementation-dependent details of how methods are called. The macro call-method has lexical scope and can only be used within an effective method form.  
 Whether or not call-method is fbound in the global environment is implementation-dependent; however, the restrictions on redefinition and shadowing of call-method are the same as for symbols in the COMMON-LISP package which are fbound in the global environment. The consequences of attempting to use call-method outside of an effective method form are undefined.  
 The macro call-method invokes the specified method, supplying it with arguments and with definitions for call-next-method and for next-method-p. If the invocation of call-method is lexically inside of a make-method, the arguments are those that were supplied to that method. Otherwise the arguments are those that were supplied to the generic function. The definitions of call-next-method and next-method-p rely on the specified next-method-list.  
If method is a list, the first element of the list must be the symbol make-method and the second element must be a form. Such a list specifies a method object whose method function has a body that is the given form.  
Next-method-list can contain method objects or lists, the first element of which must be the symbol make-method and the second element of which must be a form.  
 Those are the only two places where make-method can be used. The form used with make-method is evaluated in the null lexical environment augmented with a local macro definition for call-method and with bindings named by symbols not accessible from the COMMON-LISP-USER package.  
The call-next-method function available to method will call the first method in next-method-list. The call-next-method function available in that method, in turn, will call the second method in next-method-list, and so on, until the list of next methods is exhausted.  
 If next-method-list is not supplied, the call-next-method function available to method signals an error of type control-error and the next-method-p function available to method returns nil.



### Examples
```lisp 

```
