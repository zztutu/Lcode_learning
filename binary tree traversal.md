# Binary Traversal
## Basic 
Q: iteration styles:
1. binary-tree-preorder-traversal
2. binary-tree-postorder-traversal
3. binary-tree-inorder-traversal

Q: differences  
A: where the root node is!  
1. inorder: left root right
2. preorder: root left right
3. postorder: left right root

## Recursion methods
Q: how to understand the recursion of "return [root.val]+left+right"  
A:  
1. example: [1] + [2] +[3] or [1] + [2, 3]  
2. the recursion can runover the function and return --  current layer is done 
3. or it can break at the condition and return to continue last layer -- left node 

B: [root.val] is importatn also, if not root: return **[]**

## Stack realizations:
T: we have to push root.left/right and then pop



## Sources
[videos](https://www.youtube.com/watch?v=p3YUlEZr2vM&list=PLFj4kIJmwGu1U3uBAy4BXzQtXUihM2Hq0)