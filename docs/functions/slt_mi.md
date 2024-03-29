<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Standard Generic Function SLOT-MISSING

### Syntax
`slot-missing class object slot-name operation &optional new-value => result*Method Signatures:`  
`slot-missing (class t) object slot-name operation &optional new-value`  


### Arguments and Values
- **class** : the class of object.   
- **object** : an object.   
- **slot-name** : a symbol (the name of a would-be slot).   
- **operation** : one of the symbols setf, slot-boundp, slot-makunbound, or slot-value.   
- **new-value** : an object.   
- **result** : an object.   


### Description
The generic function slot-missing is invoked when an attempt is made to access a slot in an object whose metaclass is standard-class and the slot of the name slot-name is not a name of a slot in that class. The default method signals an error.  
The generic function slot-missing is not intended to be called by programmers. Programmers may write methods for it.  
The generic function slot-missing may be called during evaluation of slot-value, (setf slot-value), slot-boundp, and slot-makunbound. For each of these operations the corresponding symbol for the operation argument is slot-value, setf, slot-boundp, and slot-makunbound respectively.  
The optional new-value argument to slot-missing is used when the operation is attempting to set the value of the slot.  
 If slot-missing returns, its values will be treated as follows:Examples: None.



### Examples
No example  
