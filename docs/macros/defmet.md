<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro DEFMETHOD

### Syntax
`defmethod function-name {method-qualifier}* specialized-lambda-list [[declaration* | documentation]] form* => new-methodfunction-name::= {symbol | (setf symbol)}method-qualifier::= non-list`  
`specialized-lambda-list::= ({var | (var parameter-specializer-name)}*`  
`[&optional {var | (var [initform [supplied-p-parameter] ])}*]`  
`[&rest var]`  
`[&key{var | ({var | (keywordvar)} [initform [supplied-p-parameter] ])}*`  
`[&allow-other-keys] ]`  
`[&aux {var | (var [initform] )}*] )`  
`parameter-specializer-name::= symbol | (eql eql-specializer-form)`  


### Arguments and Values
- **declaration** : a declare expression; not evaluated.   
- **documentation** : a string; not evaluated.   
- **var** : a variable name.   
- **eql-specializer-form** : a form.   
- **Form** : a form.   
- **Initform** : a form.   
- **Supplied-p-parameter** : variable name.   
- **new-method** : the new method object.   


### Description
The macro defmethod defines a method on a generic function.  
If (fboundp function-name) is nil, a generic function is created with default values for the argument precedence order (each argument is more specific than the arguments to its right in the argument list), for the generic function class (the class standard-generic-function), for the method class (the class standard-method), and for the method combination type (the standard method combination type). The lambda list of the generic function is congruent with the lambda list of the method being defined; if the defmethod form mentions keyword arguments, the lambda list of the generic function will mention  ..... key (but no keyword arguments). If function-name names an ordinary function, a macro, or a special operator, an error is signaled.  
If a generic function is currently named by function-name, the lambda list of the method must be congruent with the lambda list of the generic function. If this condition does not hold, an error is signaled. For a definition of congruence in this context, see Section 7.6.4 (Congruent Lambda-lists for all Methods of a Generic Function).  
Each method-qualifier argument is an object that is used by method combination to identify the given method. The method combination type might further restrict what a method qualifier can be. The standard method combination type allows for unqualified methods and methods whose sole qualifier is one of the keywords :before, :after, or :around.  
The specialized-lambda-list argument is like an ordinary lambda list except that the names of required parameters can be replaced by specialized parameters. A specialized parameter is a list of the form (var parameter-specializer-name). Only required parameters can be specialized. If parameter-specializer-name is a symbol it names a class; if it is a list, it is of the form (eql eql-specializer-form). The parameter specializer name (eql eql-specializer-form) indicates that the corresponding argument must be eql to the object that is the value of eql-specializer-form for the method to be applicable. The eql-specializer-form is evaluated at the time that the expansion of the defmethod macro is evaluated. If no parameter specializer name is specified for a given required parameter, the parameter specializer defaults to the class t. For further discussion, see Section 7.6.2 (Introduction to Methods).  
The form arguments specify the method body. The body of the method is enclosed in an implicit block. If function-name is a symbol, this block bears the same name as the generic function. If function-name is a list of the form (setf symbol), the name of the block is symbol.  
The class of the method object that is created is that given by the method class option of the generic function on which the method is defined.  
If the generic function already has a method that agrees with the method being defined on parameter specializers and qualifiers, defmethod replaces the existing method with the one now being defined. For a definition of agreement in this context. see Section 7.6.3 (Agreement on Parameter Specializers and Qualifiers).  
The parameter specializers are derived from the parameter specializer names as described in Section 7.6.2 (Introduction to Methods).  
The expansion of the defmethod macro ``refers to'' each specialized parameter (see the description of ignore within the description of declare). This includes parameters that have an explicit parameter specializer name of t. This means that a compiler warning does not occur if the body of the method does not refer to a specialized parameter, while a warning might occur if the body of the method does not refer to an unspecialized parameter. For this reason, a parameter that specializes on t is not quite synonymous with an unspecialized parameter in this context.  
 Declarations at the head of the method body that apply to the method's lambda variables are treated as bound declarations whose scope is the same as the corresponding bindings.  
Declarations at the head of the method body that apply to the functional bindings of call-next-method or next-method-p apply to references to those functions within the method body forms. Any outer bindings of the function names call-next-method and next-method-p, and declarations associated with such bindings are shadowed[2] within the method body forms.  
The scope of free declarations at the head of the method body is the entire method body, which includes any implicit local function definitions but excludes initialization forms for the lambda variables.  
 defmethod is not required to perform any compile-time side effects. In particular, the methods are not installed for invocation during compilation. An implementation may choose to store information about the generic function for the purposes of compile-time error-checking (such as checking the number of arguments on calls, or noting that a definition for the function name has been seen).  
 Documentation is attached as a documentation string to the method object.Examples: None.



### Examples
No example  
