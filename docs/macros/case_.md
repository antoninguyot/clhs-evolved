<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro CASE, CCASE, ECASE

### Syntax
`case keyform {normal-clause}* [otherwise-clause] => result*`  
`ccase keyplace {normal-clause}* => result*`  
`ecase keyform {normal-clause}* => result*`  
`normal-clause::= (keys form*)`  
`otherwise-clause::= ({otherwise | t} form*)`  
`clause::= normal-clause | otherwise-clause`  


### Arguments and Values
- **keyform** : a form; evaluated to produce a test-key.   
- **keyplace** : a form; evaluated initially to produce a test-key. Possibly also used later as a place if no keys match.   
- **test-key** : an object produced by evaluating keyform or keyplace.   
- **keys** : a designator for a list of objects. In the case of case, the symbols t and otherwise may not be used as the keys designator. To refer to these symbols by themselves as keys, the designators (t) and (otherwise), respectively, must be used instead.   
- **forms** : an implicit progn.   
- **results** : the values returned by the forms in the matching clause.   


### Description
These macros allow the conditional execution of a body of forms in a clause that is selected by matching the test-key on the basis of its identity.  
The keyform or keyplace is evaluated to produce the test-key.  
Each of the normal-clauses is then considered in turn. If the test-key is the same as any key for that clause, the forms in that clause are evaluated as an implicit progn, and the values it returns are returned as the value of the case, ccase, or ecase form.  
These macros differ only in their behavior when no normal-clause matches; specifically:  
If there is no otherwise-clause, case returns nil.  
If the store-value restart is invoked, its argument becomes the new test-key, and is stored in keyplace as if by (setf keyplace test-key). Then ccase starts over, considering each clause anew.  
 The subforms of keyplace might be evaluated again if none of the cases holds.  
Note that in contrast with ccase, the caller of ecase may rely on the fact that ecase does not return if a normal-clause does not match.



### Examples
```lisp 
(dolist (k '(1 2 3 :four #\v () t 'other))
    (format t "~S "
       (case k ((1 2) 'clause1)
               (3 'clause2)
               (nil 'no-keys-so-never-seen)
               ((nil) 'nilslot)
               ((:four #\v) 'clause4)
               ((t) 'tslot)
               (otherwise 'others)))) 
>>  CLAUSE1 CLAUSE1 CLAUSE2 CLAUSE4 CLAUSE4 NILSLOT TSLOT OTHERS 
=>  NIL
 (defun add-em (x) (apply #'+ (mapcar #'decode x)))
=>  ADD-EM
 (defun decode (x)
   (ccase x
     ((i uno) 1)
     ((ii dos) 2)
     ((iii tres) 3)
     ((iv cuatro) 4)))
=>  DECODE
 (add-em '(uno iii)) =>  4
 (add-em '(uno iiii))
>>  Error: The value of X, IIII, is not I, UNO, II, DOS, III,
>>         TRES, IV, or CUATRO.
>>   1: Supply a value to use instead.
>>   2: Return to Lisp Toplevel.
>>  Debug> :CONTINUE 1
>>  Value to evaluate and use for X: 'IV
=>  5Side Effects:
The debugger might be entered. If the store-value restart is invoked, the value of keyplace might be changed.
```
