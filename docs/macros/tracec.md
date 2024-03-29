<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Macro TRACE, UNTRACE

### Syntax
`trace function-name* => trace-result`  
`untrace function-name* => untrace-result`  


### Arguments and Values
- **function-name** : a function name.   
- **trace-result** : implementation-dependent, unless no function-names are supplied, in which case trace-result is a list of function names.   
- **untrace-result** : implementation-dependent.   


### Description
trace and untrace control the invocation of the trace facility.  
Invoking trace with one or more function-names causes the denoted functions to be ``traced.'' Whenever a traced function is invoked, information about the call, about the arguments passed, and about any eventually returned values is printed to trace output. If trace is used with no function-names, no tracing action is performed; instead, a list of the functions currently being traced is returned.  
Invoking untrace with one or more function names causes those functions to be ``untraced'' (i.e., no longer traced). If untrace is used with no function-names, all functions currently being traced are untraced.  
If a function to be traced has been open-coded (e.g., because it was declared inline), a call to that function might not produce trace output.



### Examples
```lisp 
(defun fact (n) (if (zerop n) 1 (* n (fact (- n 1)))))
=>  FACT
 (trace fact)
=>  (FACT)
;; Of course, the format of traced output is implementation-dependent.
 (fact 3)
>>  1 Enter FACT 3
>>  | 2 Enter FACT 2
>>  |   3 Enter FACT 1
>>  |   | 4 Enter FACT 0
>>  |   | 4 Exit FACT 1
>>  |   3 Exit FACT 1
>>  | 2 Exit FACT 2
>>  1 Exit FACT 6
=>  6Side Effects:
Might change the definitions of the functions named by function-names.
```
