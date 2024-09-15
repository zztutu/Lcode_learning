### 1143.最长公共子序列
- 可删除，但是不可调整顺序

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        # 创建一个二维数组 dp，用于存储最长公共子序列的长度
        dp = [[0] * (len(text2) + 1) for _ in range(len(text1) + 1)]

        # 遍历 text1 和 text2，填充 dp 数组
        for i in range(1, len(text1) + 1):
            for j in range(1, len(text2) + 1):
                if text1[i - 1] == text2[j - 1]:
                    # 如果 text1[i-1] 和 text2[j-1] 相等，则当前位置的最长公共子序列长度为左上角位置的值加一
                    dp[i][j] = dp[i - 1][j - 1] + 1
                else:
                    # 如果 text1[i-1] 和 text2[j-1] 不相等，则当前位置的最长公共子序列长度为上方或左方的较大值
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

        # 返回最长公共子序列的长度
        return dp[len(text1)][len(text2)]
```

### 1035.不相交的线
- 本题说是求绘制的最大连线数，其实就是求两个字符串的最长公共子序列的长度
- 顺序matter，和上面的一样嘛

```python
class Solution:
    def maxUncrossedLines(self, A: List[int], B: List[int]) -> int:
        dp = [[0] * (len(B)+1) for _ in range(len(A)+1)]
        for i in range(1, len(A)+1):
            for j in range(1, len(B)+1):
                if A[i-1] == B[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        return dp[-1][-1]
```


### 53. 最大子序和
- 之前贪心的算法，理解起来更简单一些
- dp[i]：包括下标i（以nums[i]为结尾）的最大连续子序列和为dp[i]
  - dp[i - 1] + nums[i]，即：nums[i]加入当前连续子序列和
  - nums[i]，即：从头开始计算当前连续子序列和
  - 分情况讨论的递推公式，之前也遇到过类似问题
- dp[i] = max(dp[i - 1] + nums[i], nums[i])

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = [0] * len(nums)
        dp[0] = nums[0]
        result = dp[0]
        for i in range(1, len(nums)):
            dp[i] = max(dp[i-1] + nums[i], nums[i]) #状态转移公式
            result = max(result, dp[i]) #result 保存dp[i]的最大值
        return result
```


### 392.判断子序列
- 和第一个题是一样的
- dp[i][j] 表示以下标i-1为结尾的字符串s，和以下标j-1为结尾的字符串t，相同子序列的长度为dp[i][j]
  - if (s[i - 1] == t[j - 1])：- t中找到了一个字符在s中也出现了
  - if (s[i - 1] != t[j - 1])：相当于t要删除元素，继续匹配

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        dp = [[0] * (len(t)+1) for _ in range(len(s)+1)]
        for i in range(1, len(s)+1):
            for j in range(1, len(t)+1):
                if s[i-1] == t[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = dp[i][j-1]
        if dp[-1][-1] == len(s):
            return True
        return False
```