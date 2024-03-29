<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Standard Generic Function INITIALIZE-INSTANCE

### Syntax
`initialize-instance instance &rest initargs &key &allow-other-keys => instanceMethod Signatures:`  
`initialize-instance (instance standard-object) &rest initargs`  


### Arguments and Values
- **instance** : an object.   
- **initargs** : a defaulted initialization argument list.   


### Description
Called by make-instance to initialize a newly created instance. The generic function is called with the new instance and the defaulted initialization argument list.  
The system-supplied primary method on initialize-instance initializes the slots of the instance with values according to the initargs and the :initform forms of the slots. It does this by calling the generic function shared-initialize with the following arguments: the instance, t (this indicates that all slots for which no initialization arguments are provided should be initialized according to their :initform forms), and the initargs.  
Programmers can define methods for initialize-instance to specify actions to be taken when an instance is initialized. If only after methods are defined, they will be run after the system-supplied primary method for initialization and therefore will not interfere with the default behavior of initialize-instance.Examples: None.



### Examples
No example  
