<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Standard Generic Function NO-NEXT-METHOD

### Syntax
`no-next-method generic-function method &rest args => result*Method Signatures:`  
`no-next-method (generic-function standard-generic-function) (method standard-method) &rest args`  


### Arguments and Values
- **generic-function** :  generic function to which method belongs.   
- **method** :  method that contained the call to call-next-method for which there is no next method.   
- **args** :  arguments to call-next-method.   
- **result** : an object.   


### Description
The generic function no-next-method is called by call-next-method when there is no next method.  
The generic function no-next-method is not intended to be called by programmers. Programmers may write methods for it.Examples: None.



### Examples
No example  
