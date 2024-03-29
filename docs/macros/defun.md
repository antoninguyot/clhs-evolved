<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro DEFUN

### Syntax
`defun function-name lambda-list [[declaration* | documentation]] form* => function-name`  


### Arguments and Values
- **function-name** : a function name.   
- **lambda-list** : an ordinary lambda list.   
- **declaration** : a declare expression; not evaluated.   
- **documentation** : a string; not evaluated.   
- **forms** : an implicit progn.   
- **block-name** : the function block name of the function-name.   


### Description
Defines a new function named function-name in the global environment. The body of the function defined by defun consists of forms; they are executed as an implicit progn when the function is called. defun can be used to define a new function, to install a corrected version of an incorrect definition, to redefine an already-defined function, or to redefine a macro as a function.  
defun implicitly puts a block named block-name around the body forms  (but not the forms in the lambda-list)  of the function defined.  
 Documentation is attached as a documentation string to name (as kind function) and to the function object.  
Evaluating defun causes function-name to be a global name for the function specified by the lambda expression  
 (lambda lambda-list  
   [[declaration* | documentation]]  
   (block block-name form*))  
processed in the lexical environment in which defun was executed.  
(None of the arguments are evaluated at macro expansion time.)  
 defun is not required to perform any compile-time side effects. In particular, defun does not make the function definition available at compile time. An implementation may choose to store information about the function for the purposes of compile-time error-checking (such as checking the number of arguments on calls), or to enable the function to be expanded inline.



### Examples
```lisp 
(defun recur (x)
  (when (> x 0)
    (recur (1- x)))) =>  RECUR 
 (defun ex (a b &optional c (d 66) &rest keys &key test (start 0))
    (list a b c d keys test start)) =>  EX 
 (ex 1 2) =>  (1 2 NIL 66 NIL NIL 0)
 (ex 1 2 3 4 :test 'equal :start 50) 
=>  (1 2 3 4 (:TEST EQUAL :START 50) EQUAL 50)
 (ex :test 1 :start 2) =>  (:TEST 1 :START 2 NIL NIL 0)

 ;; This function assumes its callers have checked the types of the
 ;; arguments, and authorizes the compiler to build in that assumption.
 (defun discriminant (a b c)
   (declare (number a b c))
   "Compute the discriminant for a quadratic equation."
   (- (* b b) (* 4 a c))) =>  DISCRIMINANT
 (discriminant 1 2/3 -2) =>  76/9

 ;; This function assumes its callers have not checked the types of the
 ;; arguments, and performs explicit type checks before making any assumptions. 
 (defun careful-discriminant (a b c)
   "Compute the discriminant for a quadratic equation."
   (check-type a number)
   (check-type b number)
   (check-type c number)
   (locally (declare (number a b c))
     (- (* b b) (* 4 a c)))) =>  CAREFUL-DISCRIMINANT
 (careful-discriminant 1 2/3 -2) =>  76/9
```
