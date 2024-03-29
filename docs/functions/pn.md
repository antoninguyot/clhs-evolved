<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PATHNAME

### Syntax
`pathname pathspec => pathname`  


### Arguments and Values
- **pathspec** : a pathname designator.   
- **pathname** : a pathname.   


### Description
Returns the pathname denoted by pathspec.  
 If the pathspec designator is a stream, the stream can be either open or closed; in both cases, the pathname returned corresponds to the filename used to open the file. pathname returns the same pathname for a file stream after it is closed as it did when it was open.  
 If the pathspec designator is a file stream created by opening a logical pathname, a logical pathname is returned.



### Examples
```lisp 
;; There is a great degree of variability permitted here.  The next
 ;; several examples are intended to illustrate just a few of the many
 ;; possibilities.  Whether the name is canonicalized to a particular
 ;; case (either upper or lower) depends on both the file system and the
 ;; implementation since two different implementations using the same
 ;; file system might differ on many issues.  How information is stored
 ;; internally (and possibly presented in #S notation) might vary,
 ;; possibly requiring `accessors' such as PATHNAME-NAME to perform case
 ;; conversion upon access.  The format of a namestring is dependent both
 ;; on the file system and the implementation since, for example, one
 ;; implementation might include the host name in a namestring, and
 ;; another might not.  #S notation would generally only be used in a
 ;; situation where no appropriate namestring could be constructed for use
 ;; with #P.
 (setq p1 (pathname "test"))
=>  #P"CHOCOLATE:TEST" ; with case canonicalization (e.g., VMS)
OR=>  #P"VANILLA:test"   ; without case canonicalization (e.g., Unix)
OR=>  #P"test"
OR=>  #S(PATHNAME :HOST "STRAWBERRY" :NAME "TEST")
OR=>  #S(PATHNAME :HOST "BELGIAN-CHOCOLATE" :NAME "test")
 (setq p2 (pathname "test"))
=>  #P"CHOCOLATE:TEST"
OR=>  #P"VANILLA:test"
OR=>  #P"test"
OR=>  #S(PATHNAME :HOST "STRAWBERRY" :NAME "TEST")
OR=>  #S(PATHNAME :HOST "BELGIAN-CHOCOLATE" :NAME "test")
 (pathnamep p1) =>  true
 (eq p1 (pathname p1)) =>  true
 (eq p1 p2)
=>  true
OR=>  false
 (with-open-file (stream "test" :direction :output)
   (pathname stream))
=>  #P"ORANGE-CHOCOLATE:>Gus>test.lisp.newest"
```
