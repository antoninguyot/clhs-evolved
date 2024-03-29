<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function NAMESTRING, FILE-NAMESTRING, DIRECTORY-NAMESTRING, HOST-NAMESTRING, ENOUGH-NAMESTRING

### Syntax
`namestring pathname => namestring`  
`file-namestring pathname => namestring`  
`directory-namestring pathname => namestring`  
`host-namestring pathname => namestring`  
`enough-namestring pathname &optional defaults => namestring`  


### Arguments and Values
- **pathname** : a pathname designator.   
- **defaults** : a pathname designator.  The default is the value of *default-pathname-defaults*.   
- **namestring** : a string or nil.   


### Description
These functions convert pathname into a namestring. The name represented by pathname is returned as a namestring in an implementation-dependent canonical form.  
namestring returns the full form of pathname.  
file-namestring returns just the name, type, and version components of pathname.  
directory-namestring returns the directory name portion.  
host-namestring returns the host name.  
enough-namestring returns an abbreviated namestring that is just sufficient to identify the file named by pathname when considered relative to the defaults. It is required that  
 (merge-pathnames (enough-namestring pathname defaults) defaults)  
==  (merge-pathnames (parse-namestring pathname nil defaults) defaults)  
It is not necessarily possible to construct a valid namestring by concatenating some of the three shorter namestrings in some order.



### Examples
```lisp 
(namestring "getty")            
=>  "getty"
 (setq q (make-pathname :host "kathy" 
                         :directory 
                           (pathname-directory *default-pathname-defaults*)
                         :name "getty")) 
=>  #S(PATHNAME :HOST "kathy" :DEVICE NIL :DIRECTORY directory-name 
       :NAME "getty" :TYPE NIL :VERSION NIL)
 (file-namestring q) =>  "getty"
 (directory-namestring q) =>  directory-name
 (host-namestring q) =>  "kathy"
 ;;;Using Unix syntax and the wildcard conventions used by the
 ;;;particular version of Unix on which this example was created:
 (namestring
   (translate-pathname "/usr/dmr/hacks/frob.l"
                       "/usr/d*/hacks/*.l"
                       "/usr/d*/backup/hacks/backup-*.*"))
=>  "/usr/dmr/backup/hacks/backup-frob.l"
 (namestring
   (translate-pathname "/usr/dmr/hacks/frob.l"
                       "/usr/d*/hacks/fr*.l"
                       "/usr/d*/backup/hacks/backup-*.*"))
=>  "/usr/dmr/backup/hacks/backup-ob.l"
 
 ;;;This is similar to the above example but uses two different hosts,
 ;;;U: which is a Unix and V: which is a VMS.  Note the translation
 ;;;of file type and alphabetic case conventions.
 (namestring
   (translate-pathname "U:/usr/dmr/hacks/frob.l"
                       "U:/usr/d*/hacks/*.l"
                       "V:SYS$DISK:[D*.BACKUP.HACKS]BACKUP-*.*"))
=>  "V:SYS$DISK:[DMR.BACKUP.HACKS]BACKUP-FROB.LSP"
 (namestring
   (translate-pathname "U:/usr/dmr/hacks/frob.l"
                       "U:/usr/d*/hacks/fr*.l"
                       "V:SYS$DISK:[D*.BACKUP.HACKS]BACKUP-*.*"))
=>  "V:SYS$DISK:[DMR.BACKUP.HACKS]BACKUP-OB.LSP"
```
