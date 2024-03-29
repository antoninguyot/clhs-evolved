<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function Y-OR-N-P, YES-OR-NO-P

### Syntax
`y-or-n-p &optional control &rest arguments => generalized-boolean`  
`yes-or-no-p &optional control &rest arguments => generalized-boolean`  


### Arguments and Values
- **control** : a format control.   
- **arguments** : format arguments for control.   
- **generalized-boolean** : a generalized boolean.   


### Description
These functions ask a question and parse a response from the user. They return true if the answer is affirmative, or false if the answer is negative.  
y-or-n-p is for asking the user a question whose answer is either ``yes'' or ``no.'' It is intended that the reply require the user to answer a yes-or-no question with a single character. yes-or-no-p is also for asking the user a question whose answer is either ``Yes'' or ``No.'' It is intended that the reply require the user to take more action than just a single keystroke, such as typing the full word yes or no followed by a newline.  
y-or-n-p types out a message (if supplied), reads an answer in some implementation-dependent manner (intended to be short and simple, such as reading a single character such as Y or N). yes-or-no-p types out a message (if supplied), attracts the user's attention (for example, by ringing the terminal's bell), and reads an answer in some implementation-dependent manner (intended to be multiple characters, such as YES or NO).  
If format-control is supplied and not nil, then a fresh-line operation is performed; then a message is printed as if format-control and arguments were given to format. In any case, yes-or-no-p and y-or-n-p will provide a prompt such as ``(Y or N)'' or ``(Yes or No)'' if appropriate.  
All input and output are performed using query I/O.



### Examples
```lisp 
(y-or-n-p "(t or nil) given by")
>>  (t or nil) given by (Y or N) Y
=>  true
 (yes-or-no-p "a ~S message" 'frightening) 
>>  a FRIGHTENING message (Yes or No) no
=>  false
 (y-or-n-p "Produce listing file?") 
>>  Produce listing file?
>>  Please respond with Y or N. n
=>  falseSide Effects:
Output to and input from query I/O will occur.
```
