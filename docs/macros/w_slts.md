<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro WITH-SLOTS

### Syntax
`with-slots (slot-entry*) instance-form declaration* form* => result*`  
`slot-entry::= slot-name | (variable-name slot-name)`  


### Arguments and Values
- **slot-name** : a slot name; not evaluated.   
- **variable-name** : a variable name; not evaluated.   
- **instance-form** : a form; evaluted to produce instance.   
- **instance** : an object.   
- **declaration** : a declare expression; not evaluated.   
- **forms** : an implicit progn.   
- **results** : the values returned by the forms.   


### Description
The macro with-slots establishes a lexical environment for referring to the slots in the instance named by the given slot-names as though they were variables. Within such a context the value of the slot can be specified by using its slot name, as if it were a lexically bound variable. Both setf and setq can be used to set the value of the slot.  
The macro with-slots translates an appearance of the slot name as a variable into a call to slot-value.



### Examples
```lisp 
(defclass thing ()
           ((x :initarg :x :accessor thing-x)
            (y :initarg :y :accessor thing-y)))
=>  #<STANDARD-CLASS THING 250020173>
 (defmethod (setf thing-x) :before (new-x (thing thing))
   (format t "~&Changing X from ~D to ~D in ~S.~%"
           (thing-x thing) new-x thing))
 (setq thing (make-instance 'thing :x 0 :y 1)) =>  #<THING 62310540>
 (with-slots (x y) thing (incf x) (incf y)) =>  2
 (values (thing-x thing) (thing-y thing)) =>  1, 2
 (setq thing1 (make-instance 'thing :x 1 :y 2)) =>  #<THING 43135676>
 (setq thing2 (make-instance 'thing :x 7 :y 8)) =>  #<THING 43147374>
 (with-slots ((x1 x) (y1 y))
             thing1
   (with-slots ((x2 x) (y2 y))
               thing2
     (list (list x1 (thing-x thing1) y1 (thing-y thing1)
                 x2 (thing-x thing2) y2 (thing-y thing2))
           (setq x1 (+ y1 x2))
           (list x1 (thing-x thing1) y1 (thing-y thing1)
                 x2 (thing-x thing2) y2 (thing-y thing2))
           (setf (thing-x thing2) (list x1))
           (list x1 (thing-x thing1) y1 (thing-y thing1)
                 x2 (thing-x thing2) y2 (thing-y thing2)))))
>>  Changing X from 7 to (9) in #<THING 43147374>.
=>  ((1 1 2 2 7 7 8 8)
     9
     (9 9 2 2 7 7 8 8) 
     (9)
     (9 9 2 2 (9) (9) 8 8))
```
