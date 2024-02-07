### Breadth-First-Search (level traversal)
```python
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root: 
            return None

        queue = collections.deque([root])    
        while queue:
            for i in range(len(queue)):
                node = queue.popleft()
                node.left, node.right = node.right, node.left
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
        return root  
```
### Depth First Search (recursive)

```python
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            return None
        root.left, root.right = root.right, root.left
        self.invertTree(root.left)
        self.invertTree(root.right)
        return root
```