<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MACHINE-VERSION

### Syntax
`machine-version <no arguments> => description`  


### Arguments and Values
- **description** : a string or nil.   


### Description
Returns a string that identifies the version of the computer hardware on which Common Lisp is running, or nil if no such value can be computed.



### Examples
```lisp 
(machine-version) =>  "KL-10, microcode 9"Side Effects: None.
```
