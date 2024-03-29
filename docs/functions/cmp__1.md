<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function COMPILE-FILE-PATHNAME

### Syntax
`compile-file-pathname input-file &key output-file &allow-other-keys => pathname`  


### Arguments and Values
- **input-file** : a pathname designator. (Default fillers for unspecified components are taken from *default-pathname-defaults*.)   
- **output-file** : a pathname designator. The default is implementation-defined.   
- **pathname** : a pathname.   


### Description
Returns the pathname that compile-file would write into, if given the same arguments.  
 The defaults for the output-file are taken from the pathname that results from merging the input-file with the value of *default-pathname-defaults*, except that the type component should default to the appropriate implementation-defined default type for compiled files.  
If input-file is a logical pathname and output-file is unsupplied, the result is a logical pathname.  If input-file is a logical pathname, it is translated into a physical pathname as if by calling translate-logical-pathname.   If input-file is a stream, the stream can be either open or closed. compile-file-pathname returns the same pathname after a file is closed as it did when the file was open.   It is an error if input-file is a stream that is created with make-two-way-stream, make-echo-stream, make-broadcast-stream, make-concatenated-stream, make-string-input-stream, make-string-output-stream.  
If an implementation supports additional keyword arguments to compile-file, compile-file-pathname must accept the same arguments.



### Examples
```lisp 
See logical-pathname-translations.
```
