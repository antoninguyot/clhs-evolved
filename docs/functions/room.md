<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function ROOM

### Syntax
`room &optional x => implementation-dependent`  


### Arguments and Values
- **x** : one of t, nil, or :default.   


### Description
room prints, to standard output, information about the state of internal storage and its management. This might include descriptions of the amount of memory in use and the degree of memory compaction, possibly broken down by internal data type if that is appropriate. The nature and format of the printed information is implementation-dependent. The intent is to provide information that a programmer might use to tune a program for a particular implementation.  
(room nil) prints out a minimal amount of information. (room t) prints out a maximal amount of information.  (room) or (room :default) prints out an intermediate amount of information that is likely to be useful.Examples: None.Side Effects:  
Output to standard output.



### Examples
No example  
