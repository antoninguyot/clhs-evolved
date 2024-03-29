<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro WITH-STANDARD-IO-SYNTAX

### Syntax
`with-standard-io-syntax form* => result*`  


### Arguments and Values
- **forms** : an implicit progn.   
- **results** : the values returned by the forms.   


### Description
Within the dynamic extent of the body of forms, all reader/printer control variables, including any implementation-defined ones not specified by this standard, are bound to values that produce standard read/print behavior. The values for the variables specified by this standard are listed in the next figure.  
Variable                     Value                                 
*package*                    The CL-USER package                   
*print-array*                t                                     
*print-base*                 10                                    
*print-case*                 :upcase                               
*print-circle*               nil                                   
*print-escape*               t                                     
*print-gensym*               t                                     
*print-length*               nil                                   
*print-level*                nil                                   
*print-lines*                nil                                   
*print-miser-width*          nil                                   
*print-pprint-dispatch*      The standard pprint dispatch table    
*print-pretty*               nil                                   
*print-radix*                nil                                   
*print-readably*             t                                     
*print-right-margin*         nil                                   
*read-base*                  10                                    
*read-default-float-format*  single-float                          
*read-eval*                  t                                     
*read-suppress*              nil                                   
*readtable*                  The standard readtableFigure 23-1.  Values of standard control variables



### Examples
```lisp 
(with-open-file (file pathname :direction :output)
   (with-standard-io-syntax
     (print data file)))

;;; ... Later, in another Lisp:

 (with-open-file (file pathname :direction :input)
   (with-standard-io-syntax
     (setq data (read file))))
```
