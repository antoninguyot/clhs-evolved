<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Accessor GET

### Syntax
`get symbol indicator &optional default => value`  
`(setf (get symbol indicator &optional default) new-value)`  


### Arguments and Values
- **symbol** : a symbol.   
- **indicator** : an object.   
- **default** : an object. The default is nil.   
- **value** : if the indicated property exists, the object that is its value; otherwise, the specified default.   
- **new-value** : an object.   


### Description
get finds a property on the property list[2] of symbol whose property indicator is identical to indicator, and returns its corresponding property value.  If there are multiple properties[1] with that property indicator, get uses the first such property.  If there is no property with that property indicator, default is returned.  
setf of get may be used to associate a new object with an existing indicator already on the symbol's property list, or to create a new assocation if none exists.  If there are multiple properties[1] with that property indicator, setf of get associates the new-value with the first such property.   When a get form is used as a setf place, any default which is supplied is evaluated according to normal left-to-right evaluation rules, but its value is ignored.



### Examples
```lisp 
(defun make-person (first-name last-name)
   (let ((person (gensym "PERSON")))
     (setf (get person 'first-name) first-name)
     (setf (get person 'last-name) last-name)
     person)) =>  MAKE-PERSON
 (defvar *john* (make-person "John" "Dow")) =>  *JOHN*
 *john* =>  #:PERSON4603
 (defvar *sally* (make-person "Sally" "Jones")) =>  *SALLY*
 (get *john* 'first-name) =>  "John"
 (get *sally* 'last-name) =>  "Jones"
 (defun marry (man woman married-name)
   (setf (get man 'wife) woman)
   (setf (get woman 'husband) man)
   (setf (get man 'last-name) married-name)
   (setf (get woman 'last-name) married-name)
   married-name) =>  MARRY
 (marry *john* *sally* "Dow-Jones") =>  "Dow-Jones"
 (get *john* 'last-name) =>  "Dow-Jones"
 (get (get *john* 'wife) 'first-name) =>  "Sally"
 (symbol-plist *john*)
=>  (WIFE #:PERSON4604 LAST-NAME "Dow-Jones" FIRST-NAME "John")
 (defmacro age (person &optional (default ''thirty-something)) 
   `(get ,person 'age ,default)) =>  AGE
 (age *john*) =>  THIRTY-SOMETHING
 (age *john* 20) =>  20
 (setf (age *john*) 25) =>  25
 (age *john*) =>  25
 (age *john* 20) =>  25Side Effects: None.
```
