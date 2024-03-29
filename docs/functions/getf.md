<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Accessor GETF

### Syntax
`getf plist indicator &optional default => value`  
`(setf (getf place indicator &optional default) new-value)`  


### Arguments and Values
- **plist** : a property list.   
- **place** : a place, the value of which is a property list.   
- **indicator** : an object.   
- **default** : an object. The default is nil.   
- **value** : an object.   
- **new-value** : an object.   


### Description
getf finds a property on the plist whose property indicator is identical to indicator, and returns its corresponding property value.  If there are multiple properties[1] with that property indicator, getf uses the first such property.  If there is no property with that property indicator, default is returned.  
setf of getf may be used to associate a new object with an existing indicator in the property list held by place, or to create a new assocation if none exists.  If there are multiple properties[1] with that property indicator, setf of getf associates the new-value with the first such property.   When a getf form is used as a setf place, any default which is supplied is evaluated according to normal left-to-right evaluation rules, but its value is ignored.  
 setf of getf is permitted to either write the value of place itself, or modify of any part, car or cdr, of the list structure held by place.



### Examples
```lisp 
(setq x '()) =>  NIL
 (getf x 'prop1) =>  NIL
 (getf x 'prop1 7) =>  7
 (getf x 'prop1) =>  NIL
 (setf (getf x 'prop1) 'val1) =>  VAL1
 (eq (getf x 'prop1) 'val1) =>  true
 (getf x 'prop1) =>  VAL1
 (getf x 'prop1 7) =>  VAL1
 x =>  (PROP1 VAL1)

;; Examples of implementation variation permitted.
 (setq foo (list 'a 'b 'c 'd 'e 'f)) =>  (A B C D E F)
 (setq bar (cddr foo)) =>  (C D E F)
 (remf foo 'c) =>  true
 foo =>  (A B E F)
 bar
=>  (C D E F)
OR=>  (C)
OR=>  (NIL)
OR=>  (C NIL)
OR=>  (C D)Side Effects: None.
```
