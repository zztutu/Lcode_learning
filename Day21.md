### 669. 修剪二叉搜索树 
- 对于不符合的node，如何操作：
> 发现节点0并不符合区间要求，那么将节点0的右孩子 节点2 直接赋给 节点3的左孩子就可以了
- 如何删除节点
- 返回值的定义
  
```python
class Solution:
    def trimBST(self, root: TreeNode, low: int, high: int) -> TreeNode:
        if root is None:
            return None
        if root.val < low:
            # 寻找符合区间 [low, high] 的节点
            return self.trimBST(root.right, low, high)
        if root.val > high:
            # 寻找符合区间 [low, high] 的节点
            return self.trimBST(root.left, low, high)
        root.left = self.trimBST(root.left, low, high)  # root.left 接入符合条件的左孩子
        root.right = self.trimBST(root.right, low, high)  # root.right 接入符合条件的右孩子
        return root
```


### 108.将有序数组转换为二叉搜索树
- 本质就是寻找分割点，分割点作为当前节点，然后递归左区间和右区间。
```python
class Solution:
    def traversal(self, nums: List[int], left: int, right: int) -> TreeNode:
        if left > right:
            return None
        
        mid = left + (right - left) // 2
        root = TreeNode(nums[mid])
        root.left = self.traversal(nums, left, mid - 1)
        root.right = self.traversal(nums, mid + 1, right)
        return root
    
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        root = self.traversal(nums, 0, len(nums) - 1)
        return root
```


### 538.把二叉搜索树转换为累加树  
> 其实这就是一棵树，大家可能看起来有点别扭，换一个角度来看，这就是一个有序数组[2, 5, 13]，求从后到前的累加数组，也就是[20, 18, 13]，是不是感觉这就简单了。
> 遍历这个二叉树，也就迎刃而解了，从树中可以看出累加的顺序是右中左，所以我们需要反中序遍历这个二叉树，然后顺序累加就可以了

```python
class Solution:
    def convertBST(self, root: TreeNode) -> TreeNode:
        self.pre = 0  # 记录前一个节点的数值
        self.traversal(root)
        return root
    def traversal(self, cur):
        if cur is None:
            return        
        self.traversal(cur.right)
        cur.val += self.pre
        self.pre = cur.val
        self.traversal(cur.left)
```