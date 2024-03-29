<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Special Operator THROW

### Syntax
`throw tag result-form =>|`  


### Arguments and Values
- **tag** : a catch tag; evaluated.   
- **result-form** : a form; evaluated as described below.   


### Description
throw causes a non-local control transfer to a catch whose tag is eq to tag.  
Tag is evaluated first to produce an object called the throw tag; then result-form is evaluated, and its results are saved. If the result-form produces multiple values, then all the values are saved. The most recent outstanding catch whose tag is eq to the throw tag is exited; the saved results are returned as the value or values of catch.  
The transfer of control initiated by throw is performed as described in Section 5.2 (Transfer of Control to an Exit Point).



### Examples
```lisp 
(catch 'result
    (setq i 0 j 0)
    (loop (incf j 3) (incf i)
          (if (= i 3) (throw 'result (values i j))))) =>  3, 9
 (catch nil 
   (unwind-protect (throw nil 1)
     (throw nil 2))) =>  2
The consequences of the following are undefined because the catch of b is passed over by the first throw, hence portable programs must assume that its dynamic extent is terminated. The binding of the catch tag is not yet disestablished and therefore it is the target of the second throw.
 (catch 'a
   (catch 'b
     (unwind-protect (throw 'a 1)
       (throw 'b 2))))
The following prints ``The inner catch returns :SECOND-THROW'' and then returns :outer-catch.
 (catch 'foo
         (format t "The inner catch returns ~s.~%"
                 (catch 'foo
                     (unwind-protect (throw 'foo :first-throw)
                         (throw 'foo :second-throw))))
         :outer-catch)
>>  The inner catch returns :SECOND-THROW
=>  :OUTER-CATCH
```
