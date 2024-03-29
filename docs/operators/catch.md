<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Special Operator CATCH

### Syntax
`catch tag form* => result*`  


### Arguments and Values
- **tag** : a catch tag; evaluated.   
- **forms** : an implicit progn.   
- **results** : if the forms exit normally, the values returned by the forms; if a throw occurs to the tag, the values that are thrown.   


### Description
catch is used as the destination of a non-local control transfer by throw. Tags are used to find the catch to which a throw is transferring control. (catch 'foo form) catches a (throw 'foo form) but not a (throw 'bar form).  
The order of execution of catch follows:  
If during the execution of one of the forms, a throw is executed whose tag is eq to the catch tag, then the values specified by the throw are returned as the result of the dynamically most recently established catch form with that tag.  
The mechanism for catch and throw works even if throw is not within the lexical scope of catch. throw must occur within the dynamic extent of the evaluation of the body of a catch with a corresponding tag.



### Examples
```lisp 
(catch 'dummy-tag 1 2 (throw 'dummy-tag 3) 4) =>  3
 (catch 'dummy-tag 1 2 3 4) =>  4
 (defun throw-back (tag) (throw tag t)) =>  THROW-BACK
 (catch 'dummy-tag (throw-back 'dummy-tag) 2) =>  T

 ;; Contrast behavior of this example with corresponding example of BLOCK.
 (catch 'c
   (flet ((c1 () (throw 'c 1)))
     (catch 'c (c1) (print 'unreachable))
     2)) =>  2
```
