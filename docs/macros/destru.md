<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro DESTRUCTURING-BIND

### Syntax
`destructuring-bind lambda-list expression declaration* form* => result*`  


### Arguments and Values
- **lambda-list** : a destructuring lambda list.   
- **expression** : a form.   
- **declaration** : a declare expression; not evaluated.   
- **forms** : an implicit progn.   
- **results** : the values returned by the forms.   


### Description
destructuring-bind binds the variables specified in lambda-list to the corresponding values in the tree structure resulting from the evaluation of expression; then destructuring-bind evaluates forms.  
The lambda-list supports destructuring as described in Section 3.4.5 (Destructuring Lambda Lists).



### Examples
```lisp 
(defun iota (n) (loop for i from 1 to n collect i))       ;helper
 (destructuring-bind ((a &optional (b 'bee)) one two three)
     `((alpha) ,@(iota 3))
   (list a b three two one)) =>  (ALPHA BEE 3 2 1)
```
