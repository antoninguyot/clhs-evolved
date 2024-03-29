<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PPRINT-INDENT

### Syntax
`pprint-indent relative-to n &optional stream => nil`  


### Arguments and Values
- **relative-to** : either :block or :current.   
- **n** : a real.   
- **stream** : an output stream designator. The default is standard output.   


### Description
pprint-indent specifies the indentation to use in a logical block on stream.  If stream is a pretty printing stream and the value of *print-pretty* is true, pprint-indent sets the indentation in the innermost dynamically enclosing logical block; otherwise, pprint-indent has no effect.  
N specifies the indentation in ems. If relative-to is :block, the indentation is set to the horizontal position of the first character in the dynamically current logical block plus n ems. If relative-to is :current, the indentation is set to the current output position plus n ems. (For robustness in the face of variable-width fonts, it is advisable to use :current with an n of zero whenever possible.)  
N can be negative; however, the total indentation cannot be moved left of the beginning of the line or left of the end of the rightmost per-line prefix---an attempt to move beyond one of these limits is treated the same as an attempt to move to that limit. Changes in indentation caused by pprint-indent do not take effect until after the next line break. In addition, in miser mode all calls to pprint-indent are ignored, forcing the lines corresponding to the logical block to line up under the first character in the block.Examples: None.Side Effects: None.



### Examples
No example  
