<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PATHNAME-HOST, PATHNAME-DEVICE, PATHNAME-DIRECTORY, PATHNAME-NAME, PATHNAME-TYPE, PATHNAME-VERSION

### Syntax
`pathname-host pathname &key case => host`  
`pathname-device pathname &key case => device`  
`pathname-directory pathname &key case => directory`  
`pathname-name pathname &key case => name`  
`pathname-type pathname &key case => type`  
`pathname-version pathname => version`  


### Arguments and Values
- **pathname** : a pathname designator.   
- **case** : one of :local or :common. The default is :local.   
- **host** : a valid pathname host.   
- **device** : a valid pathname device.   
- **directory** : a valid pathname directory.   
- **name** : a valid pathname name.   
- **type** : a valid pathname type.   
- **version** : a valid pathname version.   


### Description
These functions return the components of pathname.  
If the pathname designator is a pathname, it represents the name used to open the file. This may be, but is not required to be, the actual name of the file.  
 If case is supplied, it is treated as described in Section 19.2.2.1.2 (Case in Pathname Components).



### Examples
```lisp 
(setq q (make-pathname :host "KATHY"
                        :directory "CHAPMAN" 
                        :name "LOGIN" :type "COM"))
=>  #P"KATHY::[CHAPMAN]LOGIN.COM"
 (pathname-host q) =>  "KATHY"
 (pathname-name q) =>  "LOGIN"
 (pathname-type q) =>  "COM"

 ;; Because namestrings are used, the results shown in the remaining
 ;; examples are not necessarily the only possible results.  Mappings
 ;; from namestring representation to pathname representation are 
 ;; dependent both on the file system involved and on the implementation
 ;; (since there may be several implementations which can manipulate the
 ;; the same file system, and those implementations are not constrained
 ;; to agree on all details). Consult the documentation for each
 ;; implementation for specific information on how namestrings are treated
 ;; that implementation.

 ;; VMS
 (pathname-directory (parse-namestring "[FOO.*.BAR]BAZ.LSP"))
=>  (:ABSOLUTE "FOO" "BAR")
 (pathname-directory (parse-namestring "[FOO.*.BAR]BAZ.LSP") :case :common)
=>  (:ABSOLUTE "FOO" "BAR")

 ;; Unix
 (pathname-directory "foo.l") =>  NIL
 (pathname-device "foo.l") =>  :UNSPECIFIC
 (pathname-name "foo.l") =>  "foo"
 (pathname-name "foo.l" :case :local) =>  "foo"
 (pathname-name "foo.l" :case :common) =>  "FOO"
 (pathname-type "foo.l") =>  "l"
 (pathname-type "foo.l" :case :local) =>  "l"
 (pathname-type "foo.l" :case :common) =>  "L"
 (pathname-type "foo") =>  :UNSPECIFIC
 (pathname-type "foo" :case :common) =>  :UNSPECIFIC
 (pathname-type "foo.") =>  ""
 (pathname-type "foo." :case :common) =>  ""
 (pathname-directory (parse-namestring "/foo/bar/baz.lisp") :case :local)
=>  (:ABSOLUTE "foo" "bar")
 (pathname-directory (parse-namestring "/foo/bar/baz.lisp") :case :local)
=>  (:ABSOLUTE "FOO" "BAR")
 (pathname-directory (parse-namestring "../baz.lisp"))
=>  (:RELATIVE :UP)
 (PATHNAME-DIRECTORY (PARSE-NAMESTRING "/foo/BAR/../Mum/baz"))
=>  (:ABSOLUTE "foo" "BAR" :UP "Mum")
 (PATHNAME-DIRECTORY (PARSE-NAMESTRING "/foo/BAR/../Mum/baz") :case :common)
=>  (:ABSOLUTE "FOO" "bar" :UP "Mum")
 (PATHNAME-DIRECTORY (PARSE-NAMESTRING "/foo/*/bar/baz.l"))
=>  (:ABSOLUTE "foo" :WILD "bar")
 (PATHNAME-DIRECTORY (PARSE-NAMESTRING "/foo/*/bar/baz.l") :case :common)
=>  (:ABSOLUTE "FOO" :WILD "BAR")

 ;; Symbolics LMFS
 (pathname-directory (parse-namestring ">foo>**>bar>baz.lisp"))
=>  (:ABSOLUTE "foo" :WILD-INFERIORS "bar")
 (pathname-directory (parse-namestring ">foo>*>bar>baz.lisp"))
=>  (:ABSOLUTE "foo" :WILD "bar")
 (pathname-directory (parse-namestring ">foo>*>bar>baz.lisp") :case :common)
=>  (:ABSOLUTE "FOO" :WILD "BAR")
 (pathname-device (parse-namestring ">foo>baz.lisp")) =>  :UNSPECIFIC
```
