<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function CONCATENATED-STREAM-STREAMS

### Syntax
`concatenated-stream-streams concatenated-stream => streams`  


### Arguments and Values
- **concatenated-stream** :  a concatenated stream.   
- **streams** : a list of input streams.   


### Description
Returns a list of input streams that constitute the ordered set of streams the concatenated-stream still has to read from, starting with the current one it is reading from. The list may be empty if no more streams remain to be read.  
The consequences are undefined if the list structure of the streams is ever modified.Examples: None.Side Effects: None.



### Examples
No example  
