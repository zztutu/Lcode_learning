### 77.组合
- 回溯法解决的问题都可以抽象为树形结构（N叉树），用树形结构来理解回溯就容易多了
- 回溯法的搜索过程就是一个树型结构的遍历过程
- 剪枝优化，具体问题可以提前stop循环
- core: path.pop() 
```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        result = []  # 存放结果集
        self.backtracking(n, k, 1, [], result)
        return result
    def backtracking(self, n, k, startIndex, path, result):
        if len(path) == k:
            result.append(path[:])
            return
        for i in range(startIndex, n - (k - len(path)) + 2):  # 优化的地方
            path.append(i)  # 处理节点
            self.backtracking(n, k, i + 1, path, result)
            path.pop()  # 回溯，撤销处理的节点

```

### 216.组合总和III
- 每个数字 最多使用一次
```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        result = []
        self.backtracking(n, k, 0, 1, [], result)
        return result
    
    def backtracking(self, targetSum, k, currentSum, startIndex, path, result):
        if currentSum > targetSum:
            return
        if len(path) == k:
            if currentSum == targetSum:
                result.append(path[:])
                return
        for i in range(startIndex, 9-(k-len(path))+2):
            currentSum +=i
            path.append(i)
            self.backtracking(targetSum, k, currentSum, i+1, path, result)
            currentSum -=i
            path.pop()
```

### 17.电话号码的字母组合
- string的回溯
```python
def backtracking(self, digits, index):
        if index == len(digits):
            self.result.append(self.s)
            return
        digit = int(digits[index])    # 将索引处的数字转换为整数
        letters = self.letterMap[digit]    # 获取对应的字符集
        for i in range(len(letters)):
            self.s += letters[i]    # 处理字符
            self.backtracking(digits, index + 1)    # 递归调用，注意索引加1，处理下一个数字
            self.s = self.s[:-1]    # 回溯，删除最后添加的字符
```