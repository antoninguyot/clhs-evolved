<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Symbol DECLARE

### Syntax
`declare declaration-specifier*Arguments:`  
`declaration-specifier---a declaration specifier; not evaluated.`  


### Arguments and Values


### Description
A declare expression, sometimes called a declaration, can occur only at the beginning of the bodies of certain forms; that is, it may be preceded only by other declare expressions, or by a documentation string if the context permits.  
A declare expression can occur in a lambda expression or in any of the forms listed in the next figure.  
defgeneric                 do-external-symbols   prog                        
define-compiler-macro      do-symbols            prog*                       
define-method-combination  dolist                restart-case                
define-setf-expander       dotimes               symbol-macrolet             
defmacro                   flet                  with-accessors              
defmethod                  handler-case          with-hash-table-iterator    
defsetf                    labels                with-input-from-string      
deftype                    let                   with-open-file              
defun                      let*                  with-open-stream            
destructuring-bind         locally               with-output-to-string       
do                         macrolet              with-package-iterator       
do*                        multiple-value-bind   with-slots                  
do-all-symbols             pprint-logical-blockFigure 3-23.  Standardized Forms In Which Declarations Can Occur  
A declare expression can only occur where specified by the syntax of these forms. The consequences of attempting to evaluate a declare expression are undefined. In situations where such expressions can appear, explicit checks are made for their presence and they are never actually evaluated; it is for this reason that they are called ``declare expressions'' rather than ``declare forms.''  
 Macro forms cannot expand into declarations; declare expressions must appear as actual subexpressions of the form to which they refer.  
The next figure shows a list of declaration identifiers that can be used with declare.  
dynamic-extent  ignore     optimize    
ftype           inline     special     
ignorable       notinline  typeFigure 3-24.  Local Declaration Specifiers  
An implementation is free to support other (implementation-defined) declaration identifiers as well.



### Examples
```lisp 
(defun nonsense (k x z)
   (foo z x)                     ;First call to foo
   (let ((j (foo k x))           ;Second call to foo
         (x (* k k)))
     (declare (inline foo) (special x z))
     (foo x j z)))               ;Third call to foo
In this example, the inline declaration applies only to the third call to foo, but not to the first or second ones. The special declaration of x causes let to make a dynamic binding for x, and causes the reference to x in the body of let to be a dynamic reference. The reference to x in the second call to foo is a local reference to the second parameter of nonsense. The reference to x in the first call to foo is a local reference, not a special one. The special declaration of z causes the reference to z in the third call to foo to be a dynamic reference; it does not refer to the parameter to nonsense named z, because that parameter binding has not been declared to be special. (The special declaration of z does not appear in the body of defun, but in an inner form, and therefore does not affect the binding of the parameter.)
```
