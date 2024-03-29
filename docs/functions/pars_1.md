<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function PARSE-NAMESTRING

### Syntax
`parse-namestring thing &optional host default-pathname &key start end junk-allowed => pathname, position`  


### Arguments and Values
- **thing** : a string, a pathname, or a stream associated with a file.   
- **host** : a valid pathname host, a logical host, or nil.   
- **default-pathname** : a pathname designator. The default is the value of *default-pathname-defaults*.   
- **start, end** : bounding index designators of thing. The defaults for start and end are 0 and nil, respectively.   
- **junk-allowed** : a generalized boolean. The default is false.   
- **pathname** : a pathname, or nil.   
- **position** : a bounding index designator for thing.   


### Description
Converts thing into a pathname.  
The host supplies a host name with respect to which the parsing occurs.  
 If thing is a stream associated with a file, processing proceeds as if the pathname used to open that file had been supplied instead.  
If thing is a pathname, the host and the host component of thing are compared. If they match, two values are immediately returned: thing and start; otherwise (if they do not match), an error is signaled.  
Otherwise (if thing is a string), parse-namestring parses the name of a file within the substring of thing bounded by start and end.  
  If thing is a string then the substring of thing bounded by start and end is parsed into a pathname as follows:  
In the first of these cases, the host portion of the logical pathname namestring and its following colon are optional.  
If the host portion of the namestring and host are both present and do not match, an error is signaled.  
If junk-allowed is true, then the primary value is the pathname parsed or, if no syntactically correct pathname was seen, nil. If junk-allowed is false, then the entire substring is scanned, and the primary value is the pathname parsed.  
In either case, the secondary value is the index into thing of the delimiter that terminated the parse, or the index beyond the substring if the parse terminated at the end of the substring (as will always be the case if junk-allowed is false).  
Parsing a null string always succeeds, producing a pathname with all components (except the host) equal to nil.  
If thing contains an explicit host name and no explicit device name, then it is implementation-defined whether parse-namestring will supply the standard default device for that host as the device component of the resulting pathname.



### Examples
```lisp 
(setq q (parse-namestring "test"))  
=>  #S(PATHNAME :HOST NIL :DEVICE NIL :DIRECTORY NIL :NAME "test" 
       :TYPE NIL :VERSION NIL)
 (pathnamep q) =>  true
 (parse-namestring "test") 
=>  #S(PATHNAME :HOST NIL :DEVICE NIL :DIRECTORY NIL :NAME "test"
       :TYPE NIL :VERSION NIL), 4
 (setq s (open xxx)) =>  #<Input File Stream...>
 (parse-namestring s) 
=>  #S(PATHNAME :HOST NIL :DEVICE NIL :DIRECTORY NIL :NAME xxx 
       :TYPE NIL :VERSION NIL), 0
 (parse-namestring "test" nil nil :start 2 :end 4 )
 =>  #S(PATHNAME ...), 15
 (parse-namestring "foo.lisp")
=>  #P"foo.lisp"
```
