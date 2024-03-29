<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function APROPOS, APROPOS-LIST

### Syntax
`apropos string &optional package => <no values>`  
`apropos-list string &optional package => symbols`  


### Arguments and Values
- **string** : a string designator.   
- **package** : a package designator or nil. The default is nil.   
- **symbols** : a list of symbols.   


### Description
These functions search for interned symbols whose names contain the substring string.  
For apropos, as each such symbol is found, its name is printed on standard output. In addition, if such a symbol is defined as a function or dynamic variable, information about those definitions might also be printed.  
For apropos-list, no output occurs as the search proceeds; instead a list of the matching symbols is returned when the search is complete.  
If package is non-nil, only the symbols accessible in that package are searched; otherwise all symbols accessible in any package are searched.  
Because a symbol might be available by way of more than one inheritance path, apropos might print information about the same symbol more than once, or apropos-list might return a list containing duplicate symbols.  
Whether or not the search is case-sensitive is implementation-defined.Examples: None.



### Examples
No example  
