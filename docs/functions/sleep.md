<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function SLEEP

### Syntax
`sleep seconds => nil`  


### Arguments and Values
- **seconds** : a non-negative real.   


### Description
Causes execution to cease and become dormant for approximately the seconds of real time indicated by seconds, whereupon execution is resumed.



### Examples
```lisp 
(sleep 1) =>  NIL 

;; Actually, since SLEEP is permitted to use approximate timing, 
;; this might not always yield true, but it will often enough that
;; we felt it to be a productive example of the intent.
 (let ((then (get-universal-time))
       (now  (progn (sleep 10) (get-universal-time))))
   (>= (- now then) 10))
=>  trueSide Effects:
Causes processing to pause.
```
