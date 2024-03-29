<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function REPLACE

### Syntax
`replace sequence-1 sequence-2 &key start1 end1 start2 end2 => sequence-1`  


### Arguments and Values
- **sequence-1** : a sequence.   
- **sequence-2** : a sequence.   
- **start1, end1** : bounding index designators of sequence-1. The defaults for start1 and end1 are 0 and nil, respectively.   
- **start2, end2** : bounding index designators of sequence-2. The defaults for start2 and end2 are 0 and nil, respectively.   


### Description
Destructively modifies sequence-1 by replacing the elements of subsequence-1 bounded by start1 and end1 with the elements of subsequence-2 bounded by start2 and end2.  
Sequence-1 is destructively modified by copying successive elements into it from sequence-2. Elements of the subsequence of sequence-2 bounded by start2 and end2 are copied into the subsequence of sequence-1 bounded by start1 and end1. If these subsequences are not of the same length, then the shorter length determines how many elements are copied; the extra elements near the end of the longer subsequence are not involved in the operation. The number of elements copied can be expressed as:  
 (min (- end1 start1) (- end2 start2))  
If sequence-1 and sequence-2 are the same object and the region being modified overlaps the region being copied from, then it is as if the entire source region were copied to another place and only then copied back into the target region. However, if sequence-1 and sequence-2 are not the same, but the region being modified overlaps the region being copied from (perhaps because of shared list structure or displaced arrays), then after the replace operation the subsequence of sequence-1 being modified will have unpredictable contents. It is an error if the elements of sequence-2 are not of a type that can be stored into sequence-1.



### Examples
```lisp 
(replace "abcdefghij" "0123456789" :start1 4 :end1 7 :start2 4) 
=>  "abcd456hij"
 (setq lst "012345678") =>  "012345678"
 (replace lst lst :start1 2 :start2 0) =>  "010123456"
 lst =>  "010123456"Side Effects:
The sequence-1 is modified.
```
