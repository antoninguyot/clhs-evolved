<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MACHINE-INSTANCE

### Syntax
`machine-instance <no arguments> => description`  


### Arguments and Values
- **description** : a string or nil.   


### Description
Returns a string that identifies the particular instance of the computer hardware on which Common Lisp is running, or nil if no such string can be computed.



### Examples
```lisp 
(machine-instance)
=>  "ACME.COM"
OR=>  "S/N 123231"
OR=>  "18.26.0.179"
OR=>  "AA-00-04-00-A7-A4"Side Effects: None.
```
