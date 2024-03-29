<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function COMPILE-FILE

### Syntax
`compile-file input-file &key output-file verbose print external-format => output-truename, warnings-p, failure-p`  


### Arguments and Values
- **input-file** : a pathname designator. (Default fillers for unspecified components are taken from *default-pathname-defaults*.)   
- **output-file** : a pathname designator. The default is implementation-defined.   
- **verbose** : a generalized boolean. The default is the value of *compile-verbose*.   
- **print** : a generalized boolean. The default is the value of *compile-print*.   
- **external-format** : an external file format designator. The default is :default.   
- **output-truename** : a pathname (the truename of the output file), or nil.   
- **warnings-p** : a generalized boolean.   
- **failure-p** : a generalized boolean.   


### Description
compile-file transforms the contents of the file specified by input-file into implementation-dependent binary data which are placed in the file specified by output-file.  
The file to which input-file refers should be a source file. output-file can be used to specify an output pathname;  the actual pathname of the compiled file to which compiled code will be output is computed as if by calling compile-file-pathname.  
 If input-file or output-file is a logical pathname, it is translated into a physical pathname as if by calling translate-logical-pathname.  
  If verbose is true, compile-file prints a message in the form of a comment (i.e., with a leading semicolon) to standard output indicating what file is being compiled and other useful information. If verbose is false, compile-file does not print this information.  
If print is true, information about top level forms in the file being compiled is printed to standard output. Exactly what is printed is implementation-dependent, but nevertheless some information is printed. If print is nil, no information is printed.  
 The external-format specifies the external file format to be used when opening the file; see the function open. compile-file and load must cooperate in such a way that the resulting compiled file can be loaded without specifying an external file format anew; see the function load.  
  compile-file binds *readtable* and *package* to the values they held before processing the file.  
 *compile-file-truename* is bound by compile-file to hold the truename of the pathname of the file being compiled.  
 *compile-file-pathname* is bound by compile-file to hold a pathname denoted by the first argument to compile-file, merged against the defaults; that is, (pathname (merge-pathnames input-file)).  
The compiled functions contained in the compiled file become available for use when the compiled file is loaded into Lisp.  Any function definition that is processed by the compiler, including #'(lambda ...) forms and local function definitions made by flet, labels and defun forms, result in an object of type compiled-function.  
 The primary value returned by compile-file, output-truename, is the truename of the output file, or nil if the file could not be created.  
The secondary value, warnings-p, is false if no conditions of type error or warning were detected by the compiler, and true otherwise.  
The tertiary value, failure-p, is false if no conditions of type error or warning (other than style-warning) were detected by the compiler, and true otherwise.  
For general information about how files are processed by the file compiler, see Section 3.2.3 (File Compilation).  
  Programs to be compiled by the file compiler must only contain externalizable objects; for details on such objects, see Section 3.2.4 (Literal Objects in Compiled Files). For information on how to extend the set of externalizable objects, see the function make-load-form and Section 3.2.4.4 (Additional Constraints on Externalizable Objects).Examples: None.



### Examples
No example  
