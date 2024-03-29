<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Special Operator FLET, LABELS, MACROLET

### Syntax
`flet ((function-name lambda-list [[local-declaration* | local-documentation]] local-form*)*) declaration* form* => result*`  
`labels ((function-name lambda-list [[local-declaration* | local-documentation]] local-form*)*) declaration* form* => result*`  
`macrolet ((name lambda-list [[local-declaration* | local-documentation]] local-form*)*) declaration* form* => result*`  


### Arguments and Values
- **function-name** : a function name.   
- **name** : a symbol.   
- **lambda-list** : a lambda list; for flet and labels, it is an ordinary lambda list; for macrolet, it is a macro lambda list.   
- **local-declaration** : a declare expression; not evaluated.   
- **declaration** : a declare expression; not evaluated.   
- **local-documentation** : a string; not evaluated.   
- **local-forms, forms** : an implicit progn.   
- **results** : the values of the forms.   


### Description
flet, labels, and macrolet define local functions and macros, and execute forms using the local definitions. Forms are executed in order of occurrence.  
   The body forms (but not the lambda list)  of each function created by flet and labels and each macro created by macrolet are enclosed in an implicit block whose name is the function block name of the function-name or name, as appropriate.  
 The scope of the declarations between the list of local function/macro definitions and the body forms in flet and labels does not include the bodies of the locally defined functions, except that for labels, any inline, notinline, or ftype declarations that refer to the locally defined functions do apply to the local function bodies. That is, their scope is the same as the function name that they affect.   The scope of these declarations does not include the bodies of the macro expander functions defined by macrolet.  
The scope of the name binding encompasses only the body. Within the body of flet, function-names matching those defined by flet refer to the locally defined functions rather than to the global function definitions of the same name.   Also, within the scope of flet, global setf expander definitions of the function-name defined by flet do not apply. Note that this applies to (defsetf f ...), not (defmethod (setf f) ...).  
The names of functions defined by flet are in the lexical environment; they retain their local definitions only within the body of flet. The function definition bindings are visible only in the body of flet, not the definitions themselves. Within the function definitions, local function names that match those being defined refer to functions or macros defined outside the flet. flet can locally shadow a global function name, and the new definition can refer to the global definition.  
Any local-documentation is attached to the corresponding local function (if one is actually created) as a documentation string.  
  Within the body of macrolet, global setf expander definitions of the names defined by the macrolet do not apply; rather, setf expands the macro form and recursively process the resulting form.  
The macro-expansion functions defined by macrolet are defined in the  lexical environment in which the macrolet form appears. Declarations and macrolet and symbol-macrolet definitions affect the local macro definitions in a macrolet, but the consequences are undefined if the local macro definitions reference any local variable or function bindings that are visible in that lexical environment.  
Any local-documentation is attached to the corresponding local macro function as a documentation string.



### Examples
```lisp 
(defun foo (x flag)
   (macrolet ((fudge (z)
                 ;The parameters x and flag are not accessible
                 ; at this point; a reference to flag would be to
                 ; the global variable of that name.
                 ` (if flag (* ,z ,z) ,z)))
    ;The parameters x and flag are accessible here.
     (+ x
        (fudge x)
        (fudge (+ x 1)))))
 == 
 (defun foo (x flag)
   (+ x
      (if flag (* x x) x)
      (if flag (* (+ x 1) (+ x 1)) (+ x 1))))
 (flet ((flet1 (n) (+ n n)))
    (flet ((flet1 (n) (+ 2 (flet1 n))))
      (flet1 2))) =>  6

 (defun dummy-function () 'top-level) =>  DUMMY-FUNCTION 
 (funcall #'dummy-function) =>  TOP-LEVEL 
 (flet ((dummy-function () 'shadow)) 
      (funcall #'dummy-function)) =>  SHADOW 
 (eq (funcall #'dummy-function) (funcall 'dummy-function))
=>  true 
 (flet ((dummy-function () 'shadow))
   (eq (funcall #'dummy-function)
       (funcall 'dummy-function)))
=>  false 

 (defun recursive-times (k n)
   (labels ((temp (n) 
              (if (zerop n) 0 (+ k (temp (1- n))))))
     (temp n))) =>  RECURSIVE-TIMES
 (recursive-times 2 3) =>  6

 (defmacro mlets (x &environment env) 
    (let ((form `(babbit ,x)))
      (macroexpand form env))) =>  MLETS
 (macrolet ((babbit (z) `(+ ,z ,z))) (mlets 5)) =>  10
 (flet ((safesqrt (x) (sqrt (abs x))))
  ;; The safesqrt function is used in two places.
   (safesqrt (apply #'+ (map 'list #'safesqrt '(1 2 3 4 5 6)))))
=>  3.291173
 (defun integer-power (n k)     
   (declare (integer n))         
   (declare (type (integer 0 *) k))
   (labels ((expt0 (x k a)
              (declare (integer x a) (type (integer 0 *) k))
              (cond ((zerop k) a)
                    ((evenp k) (expt1 (* x x) (floor k 2) a))
                    (t (expt0 (* x x) (floor k 2) (* x a)))))
            (expt1 (x k a)
              (declare (integer x a) (type (integer 0 *) k))
              (cond ((evenp k) (expt1 (* x x) (floor k 2) a))
                    (t (expt0 (* x x) (floor k 2) (* x a))))))
    (expt0 n k 1))) =>  INTEGER-POWER
 (defun example (y l)
   (flet ((attach (x)
            (setq l (append l (list x)))))
     (declare (inline attach))
     (dolist (x y)
       (unless (null (cdr x))
         (attach x)))
     l))

 (example '((a apple apricot) (b banana) (c cherry) (d) (e))
          '((1) (2) (3) (4 2) (5) (6 3 2)))
=>  ((1) (2) (3) (4 2) (5) (6 3 2) (A APPLE APRICOT) (B BANANA) (C CHERRY))
```
