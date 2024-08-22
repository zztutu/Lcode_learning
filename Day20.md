### 235. 二叉搜索树的最近公共祖先
- 条件：node在两个点之间
- 顺序：第一个满足顺序的node，公共祖先
- order matters！
```python
class Solution:
    def traversal(self, cur, p, q):
        if cur is None:
            return cur
                                                        # 中
        if cur.val > p.val and cur.val > q.val:           # 左
            left = self.traversal(cur.left, p, q)
            if left is not None:
                return left

        if cur.val < p.val and cur.val < q.val:           # 右
            right = self.traversal(cur.right, p, q)
            if right is not None:
                return right

        return cur

    def lowestCommonAncestor(self, root, p, q):
```

### 701.二叉搜索树中的插入操作  
> 只要按照二叉搜索树的规则去遍历，遇到空节点就插入节点就可以了。
```python
class Solution:
    def __init__(self):
        self.parent = None

    def traversal(self, cur, val):
        if cur is None:
            node = TreeNode(val)
            if val > self.parent.val:
                self.parent.right = node
            else:
                self.parent.left = node
            return

        self.parent = cur
        if cur.val > val:
            self.traversal(cur.left, val)
        if cur.val < val:
            self.traversal(cur.right, val)

    def insertIntoBST(self, root, val):
        self.parent = TreeNode(0)
        if root is None:
            return TreeNode(val)
        self.traversal(root, val)
        return root
```

### 450.删除二叉搜索树中的节点
- 有以下五种情况：
> 第一种情况：没找到删除的节点，遍历到空节点直接返回了
> 第二种情况：左右孩子都为空（叶子节点），直接删除节点， 返回NULL为根节点
> 第三种情况：删除节点的左孩子为空，右孩子不为空，删除节点，右孩子补位，返回右孩子为根节点
> 第四种情况：删除节点的右孩子为空，左孩子不为空，删除节点，左孩子补位，返回左孩子为根节点
> 第五种情况：左右孩子节点都不为空，则将删除节点的左子树头结点（左孩子）放到删除节点的右子树的最左面节点的左孩子上，返回删除节点右孩子为新的根节点。
- 情况的讨论，是否想全了

```python
class Solution:
    def deleteNode(self, root, key):
        if root is None:  # 如果根节点为空，直接返回
            return root
        if root.val == key:  # 找到要删除的节点
            if root.right is None:  # 如果右子树为空，直接返回左子树作为新的根节点
                return root.left
            cur = root.right
            while cur.left:  # 找到右子树中的最左节点
                cur = cur.left
            root.val, cur.val = cur.val, root.val  # 将要删除的节点值与最左节点值交换
        root.left = self.deleteNode(root.left, key)  # 在左子树中递归删除目标节点
        root.right = self.deleteNode(root.right, key)  # 在右子树中递归删除目标节点
        return root
```

