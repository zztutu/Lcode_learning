### 1049. 最后一块石头的重量 II 
- 最后，最多只会剩下一块石头。返回此石头最小的可能重量。
  - 尽量让石头分成重量相同的两堆，相撞之后剩下的石头最小
  - 其实就是以对半为标准，尽量装多的石头
- dp[j]表示容量（这里说容量更形象，其实就是重量）为j的背包，最多可以背最大重量为dp[j]。
  - 递推公式：dp[j] = max(dp[j], dp[j - stones[i]] + stones[i]);
  - 就是之前的问题，一样的
- 最后return total_sum - dp[target] - dp[target]
  - 有一点点奇怪的思路，不过想对了就简单了
  
```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        dp = [0] * 1501
        total_sum = sum(stones)
        target = total_sum // 2

        for stone in stones:  # 遍历物品
            for j in range(target, stone - 1, -1):  # 遍历背包
                dp[j] = max(dp[j], dp[j - stone] + stone)

        return total_sum - dp[target] - dp[target]
```
- 一维写法
```python
class Solution:
    def lastStoneWeightII(self, stones):
        total_sum = sum(stones)
        target = total_sum // 2
        dp = [0] * (target + 1)
        for stone in stones:
            for j in range(target, stone - 1, -1):
                dp[j] = max(dp[j], dp[j - stone] + stone)
        return total_sum - 2* dp[-1]
```

### 494. 目标和
- 这个理解起来，在于，如何从题目上，联想到n可以通过n-1来得到？
  - 其实可以理解成，取或者不取，等同于加减
  - 这样就变成value，而容量就是target number
- 有一个点是判断是否可以取到target number，需要 condition的进行
- dpi的含义是，i容量背包中，有多少种组合
- 相对的二维更容易理解一点

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        total_sum = sum(nums)  # 计算nums的总和
        if abs(target) > total_sum:
            return 0  # 此时没有方案
        if (target + total_sum) % 2 == 1:
            return 0  # 此时没有方案
        target_sum = (target + total_sum) // 2  # 目标和

        # 创建二维动态规划数组，行表示选取的元素数量，列表示累加和
        dp = [[0] * (target_sum + 1) for _ in range(len(nums) + 1)]

        # 初始化状态
        dp[0][0] = 1

        # 动态规划过程
        for i in range(1, len(nums) + 1):
            for j in range(target_sum + 1):
                dp[i][j] = dp[i - 1][j]  # 不选取当前元素
                if j >= nums[i - 1]:
                    dp[i][j] += dp[i - 1][j - nums[i - 1]]  # 选取当前元素

        return dp[len(nums)][target_sum]  # 返回达到目标和的方案数
```

### 474.一和零
- 为什么能联想到用背包：最多m个0，n个1，每个str，有固定的1和0
  - 显然，每个str，可以看成是有value的
  - 容量就是个数
  - dp[i][j]：最多有i个0和j个1的strs的最大子集的大小为dp[i][j]。
- 两个维度的背包问题

```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        dp = [[0] * (n + 1) for _ in range(m + 1)]  # 创建二维动态规划数组，初始化为0
        # 遍历物品
        for s in strs:
            ones = s.count('1')  # 统计字符串中1的个数
            zeros = s.count('0')  # 统计字符串中0的个数
            # 遍历背包容量且从后向前遍历
            for i in range(m, zeros - 1, -1):
                for j in range(n, ones - 1, -1):
                    dp[i][j] = max(dp[i][j], dp[i - zeros][j - ones] + 1)  # 状态转移方程
        return dp[m][n]
```