### 39. 组合总和 
- 集合里元素可以用无数次
- 1 <= candidates[i] <= 200
- sort

```python
class Solution:

    def backtracking(self, candidates, target, total, startIndex, path, result):
        if total == target:
            result.append(path[:])
            return

        for i in range(startIndex, len(candidates)):
            if total + candidates[i] > target:
                continue
            total += candidates[i]
            path.append(candidates[i])
            self.backtracking(candidates, target, total, i, path, result)
            total -= candidates[i]
            path.pop()

    def combinationSum(self, candidates, target):
        result = []
        candidates.sort()  # 需要排序
        self.backtracking(candidates, target, 0, 0, [], result)
        return result
```

### 40.组合总和II 
- 本题开始涉及到一个问题了：去重。
- 参数，i+1
- 判断candidates是否相同

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        results = []
        self.combinationSumHelper(candidates, target, 0, [], results)
        return results

    def combinationSumHelper(self, candidates, target, index, path, results):
        if target == 0:
            results.append(path[:])
            return
        for i in range(index, len(candidates)):
            if i > index and candidates[i] == candidates[i - 1]:
                continue  
            if candidates[i] > target:
                break  
            path.append(candidates[i])
            self.combinationSumHelper(candidates, target - candidates[i], i + 1, path, results)
            path.pop()
```


### 131.分割回文串  
- 回文串 是正着读和反着读都一样的字符串。
- 其实切割问题类似组合问题。如何转化为树结构思路

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        result = []
        self.backtracking(s, 0, [], result)
        return result

    def backtracking(self, s, start_index, path, result ):
        # Base Case
        if start_index == len(s):
            result.append(path[:])
            return
        for i in range(start_index, len(s)):
            # 若反序和正序相同，意味着这是回文串
            if s[start_index: i + 1] == s[start_index: i + 1][::-1]:
                path.append(s[start_index:i+1])
                self.backtracking(s, i+1, path, result)   # 递归纵向遍历：从下一处进行切割，判断其余是否仍为回文串
                path.pop()             # 回溯
```
