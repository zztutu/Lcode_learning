### 530.二叉搜索树的最小绝对差 
> 遇到在二叉搜索树上求什么最值，求差值之类的，都要思考一下二叉搜索树可是有序的，要利用好这一特点。
> 遇到在二叉搜索树上求什么最值啊，差值之类的，就把它想成在一个有序数组上求最值，求差值，这样就简单多了。

```python
class Solution:
    def __init__(self):
        self.vec = []

    def traversal(self, root):
        if root is None:
            return
        self.traversal(root.left)
        self.vec.append(root.val)  # 将二叉搜索树转换为有序数组
        self.traversal(root.right)

    def getMinimumDifference(self, root):
        self.vec = []
        self.traversal(root)
        if len(self.vec) < 2:
            return 0
        result = float('inf')
        for i in range(1, len(self.vec)):
            # 统计有序数组的最小差值
            result = min(result, self.vec[i] - self.vec[i - 1])
        return result
```

### 501.二叉搜索树中的众数
- 最简单的方法，遍历，to Vector，字典
- 二叉搜索树，有顺序，一次性loop：使用双指针

```python
class Solution:
    def __init__(self):
        self.maxCount = 0  # 最大频率
        self.count = 0  # 统计频率
        self.pre = None
        self.result = []

    def searchBST(self, cur):
        if cur is None:
            return

        self.searchBST(cur.left)  # 左
        # 中
        if self.pre is None:  # 第一个节点
            self.count = 1
        elif self.pre.val == cur.val:  # 与前一个节点数值相同
            self.count += 1
        else:  # 与前一个节点数值不同
            self.count = 1
        self.pre = cur  # 更新上一个节点

        if self.count == self.maxCount:  # 如果与最大值频率相同，放进result中
            self.result.append(cur.val)

        if self.count > self.maxCount:  # 如果计数大于最大值频率
            self.maxCount = self.count  # 更新最大频率
            self.result = [cur.val]  # 很关键的一步，不要忘记清空result，之前result里的元素都失效了

        self.searchBST(cur.right)  # 右
        return

    def findMode(self, root):
        self.count = 0
        self.maxCount = 0
        self.pre = None  # 记录前一个节点
        self.result = []

        self.searchBST(root)
        return self.result
```


### 236. 二叉树的最近公共祖先
- 最容易的理解就是，找到两个note，之后做判断
  
```python
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        if root == q or root == p or root is None:
            return root

        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)

        if left is not None and right is not None:
            return root

        if left is None and right is not None:
            return right
        elif left is not None and right is None:
            return left
        else: 
            return None
```