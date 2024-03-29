<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro WITH-ACCESSORS

### Syntax
`with-accessors (slot-entry*) instance-form declaration* form* => result*`  
`slot-entry::= (variable-name accessor-name)`  


### Arguments and Values
- **variable-name** : a variable name; not evaluated.   
- **accessor-name** : a function name; not evaluated.   
- **instance-form** : a form; evaluated.   
- **declaration** : a declare expression; not evaluated.   
- **forms** : an implicit progn.   
- **results** : the values returned by the forms.   


### Description
Creates a lexical environment in which the slots specified by slot-entry are lexically available through their accessors as if they were variables. The macro with-accessors invokes the appropriate accessors to access the slots specified by slot-entry. Both setf and setq can be used to set the value of the slot.



### Examples
```lisp 
(defclass thing ()
           ((x :initarg :x :accessor thing-x)
            (y :initarg :y :accessor thing-y)))
=>  #<STANDARD-CLASS THING 250020173>
 (defmethod (setf thing-x) :before (new-x (thing thing))
   (format t "~&Changing X from ~D to ~D in ~S.~%"
           (thing-x thing) new-x thing))
 (setq thing1 (make-instance 'thing :x 1 :y 2)) =>  #<THING 43135676>
 (setq thing2 (make-instance 'thing :x 7 :y 8)) =>  #<THING 43147374>
 (with-accessors ((x1 thing-x) (y1 thing-y))
                 thing1
   (with-accessors ((x2 thing-x) (y2 thing-y))
                   thing2
     (list (list x1 (thing-x thing1) y1 (thing-y thing1)
                 x2 (thing-x thing2) y2 (thing-y thing2))
           (setq x1 (+ y1 x2))
           (list x1 (thing-x thing1) y1 (thing-y thing1)
                 x2 (thing-x thing2) y2 (thing-y thing2))
           (setf (thing-x thing2) (list x1))
           (list x1 (thing-x thing1) y1 (thing-y thing1)
                 x2 (thing-x thing2) y2 (thing-y thing2)))))
>>  Changing X from 1 to 9 in #<THING 43135676>.
>>  Changing X from 7 to (9) in #<THING 43147374>.
=>  ((1 1 2 2 7 7 8 8)
     9
     (9 9 2 2 7 7 8 8) 
     (9)
     (9 9 2 2 (9) (9) 8 8))
```
