<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function MERGE-PATHNAMES

### Syntax
`merge-pathnames pathname &optional default-pathname default-version => merged-pathname`  


### Arguments and Values
- **pathname** : a pathname designator.   
- **default-pathname** : a pathname designator.  The default is the value of *default-pathname-defaults*.   
- **default-version** : a valid pathname version.  The default is :newest.   
- **merged-pathname** : a pathname.   


### Description
Constructs a pathname from pathname by filling in any unsupplied components with the corresponding values from default-pathname and default-version.  
Defaulting of pathname components is done by filling in components taken from another pathname.  This is especially useful for cases such as a program that has an input file and an output file. Unspecified components of the output pathname will come from the input pathname, except that the type should not default to the type of the input pathname but rather to the appropriate default type for output from the program; for example, see the function compile-file-pathname.  
If no version is supplied, default-version is used. If default-version is nil, the version component will remain unchanged.  
If pathname explicitly specifies a host and not a device, and if the host component of default-pathname matches the host component of pathname, then the device is taken from the default-pathname; otherwise the device will be the default file device for that host. If pathname does not specify a host, device, directory, name, or type, each such component is copied from default-pathname. If pathname does not specify a name, then the version, if not provided, will come from default-pathname, just like the other components. If pathname does specify a name, then the version is not affected by default-pathname. If this process leaves the version missing, the default-version is used. If the host's file name syntax provides a way to input a version without a name or type, the user can let the name and type default but supply a version different from the one in default-pathname.  
 If pathname is a stream, pathname effectively becomes (pathname pathname). merge-pathnames can be used on either an open or a closed stream.  
If pathname is a pathname it represents the name used to open the file. This may be, but is not required to be, the actual name of the file.  
 merge-pathnames recognizes a logical pathname namestring when default-pathname is a logical pathname,  or when the namestring begins with the name of a defined logical host followed by a colon. In the first of these two cases,  the host portion of the logical pathname namestring and its following colon are optional.  
 merge-pathnames returns a logical pathname if and only if its first argument is a logical pathname,  or its first argument is a logical pathname namestring with an explicit host, or its first argument does not specify a host and the default-pathname is a logical pathname.  
 Pathname merging treats a relative directory specially. If (pathname-directory pathname) is a list whose car is :relative, and (pathname-directory default-pathname) is a list, then the merged directory is the value of  
 (append (pathname-directory default-pathname)  
         (cdr  ;remove :relative from the front  
           (pathname-directory pathname)))  
 merge-pathnames maps customary case in pathname into customary case in the output pathname.



### Examples
```lisp 
(merge-pathnames "CMUC::FORMAT"
                  "CMUC::PS:<LISPIO>.FASL")
=>  #P"CMUC::PS:<LISPIO>FORMAT.FASL.0"
```
