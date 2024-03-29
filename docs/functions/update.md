<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Standard Generic Function UPDATE-INSTANCE-FOR-DIFFERENT-CLASS

### Syntax
`update-instance-for-different-class previous current &rest initargs &key &allow-other-keys => implementation-dependentMethod Signatures:`  
`update-instance-for-different-class (previous standard-object) (current standard-object) &rest initargs`  


### Arguments and Values
- **previous** : a copy of the original instance.   
- **current** : the original instance (altered).   
- **initargs** : an initialization argument list.   


### Description
The generic function update-instance-for-different-class is not intended to be called by programmers. Programmers may write methods for it. The function update-instance-for-different-class is called only by the function change-class.  
The system-supplied primary method on update-instance-for-different-class checks the validity of initargs and signals an error if an initarg is supplied that is not declared as valid. This method then initializes slots with values according to the initargs, and initializes the newly added slots with values according to their :initform forms. It does this by calling the generic function shared-initialize with the following arguments: the instance (current), a list of names of the newly added slots, and the initargs it received. Newly added slots are those local slots for which no slot of the same name exists in the previous class.  
Methods for update-instance-for-different-class can be defined to specify actions to be taken when an instance is updated. If only after methods for update-instance-for-different-class are defined, they will be run after the system-supplied primary method for initialization and therefore will not interfere with the default behavior of update-instance-for-different-class.  
Methods on update-instance-for-different-class can be defined to initialize slots differently from change-class. The default behavior of change-class is described in Section 7.2 (Changing the Class of an Instance).  
The arguments to update-instance-for-different-class are computed by change-class. When change-class is invoked on an instance, a copy of that instance is made; change-class then destructively alters the original instance. The first argument to update-instance-for-different-class, previous, is that copy; it holds the old slot values temporarily. This argument has dynamic extent within change-class; if it is referenced in any way once update-instance-for-different-class returns, the results are undefined. The second argument to update-instance-for-different-class, current, is the altered original instance. The intended use of previous is to extract old slot values by using slot-value or with-slots or by invoking a reader generic function, or to run other methods that were applicable to instances of the original class.



### Examples
```lisp 
See the example for the function change-class.
```
