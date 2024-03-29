<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Standard Generic Function MAKE-INSTANCES-OBSOLETE

### Syntax
`make-instances-obsolete class => classMethod Signatures:`  
`make-instances-obsolete (class standard-class)`  
`make-instances-obsolete (class symbol)`  


### Arguments and Values
- **class** : a class designator.   


### Description
The function make-instances-obsolete has the effect of initiating the process of updating the instances of the class. During updating, the generic function update-instance-for-redefined-class will be invoked.  
The generic function make-instances-obsolete is invoked automatically by the system when defclass has been used to redefine an existing standard class and the set of local slots accessible in an instance is changed or the order of slots in storage is changed. It can also be explicitly invoked by the user.  
If the second of the above methods is selected, that method invokes make-instances-obsolete on (find-class class).



### Examples
```lisp 

```
