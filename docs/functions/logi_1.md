<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function LOGICAL-PATHNAME

### Syntax
`logical-pathname pathspec => logical-pathname`  


### Arguments and Values
- **pathspec** : a logical pathname, a logical pathname namestring, or a stream.   
- **logical-pathname** : a logical pathname.   


### Description
logical-pathname converts pathspec to a logical pathname and returns the new logical pathname. If pathspec is a logical pathname namestring, it should contain a host component and its following colon. If pathspec is a stream, it should be one for which pathname returns a logical pathname.  
 If pathspec is a stream, the stream can be either open or closed. logical-pathname returns the same logical pathname after a file is closed as it did when the file was open.   It is an error if pathspec is a stream that is created with make-two-way-stream, make-echo-stream, make-broadcast-stream, make-concatenated-stream, make-string-input-stream, or make-string-output-stream.Examples: None.



### Examples
No example  
