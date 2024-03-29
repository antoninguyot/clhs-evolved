<!-- Generated on 05/10/2020 by https://github.com/anto2oo/clhs-evolved -->

# Function TREE-EQUAL

### Syntax
`tree-equal tree-1 tree-2 &key test test-not => generalized-boolean`  


### Arguments and Values
- **tree-1** : a tree.   
- **tree-2** : a tree.   
- **test** : a designator for a function of two arguments that returns a generalized boolean.   
- **test-not** : a designator for a function of two arguments that returns a generalized boolean.   
- **generalized-boolean** : a generalized boolean.   


### Description
tree-equal tests whether two trees are of the same shape and have the same leaves. tree-equal returns true if tree-1 and tree-2 are both atoms and satisfy the test, or if they are both conses and the car of tree-1 is tree-equal to the car of tree-2 and the cdr of tree-1 is tree-equal to the cdr of tree-2. Otherwise, tree-equal returns false.  
tree-equal recursively compares conses but not any other objects that have components.  
The first argument to the :test or :test-not function is tree-1 or a car or cdr of tree-1; the second argument is tree-2 or a car or cdr of tree-2.



### Examples
```lisp 
(setq tree1 '(1 (1 2))
       tree2 '(1 (1 2))) =>  (1 (1 2))
 (tree-equal tree1 tree2) =>  true
 (eql tree1 tree2) =>  false
 (setq tree1 '('a ('b 'c))
       tree2 '('a ('b 'c))) =>  ('a ('b 'c)) 
=>  ((QUOTE A) ((QUOTE B) (QUOTE C)))
 (tree-equal tree1 tree2 :test 'eq) =>  trueSide Effects: None.
```
