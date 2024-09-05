### 完全背包
- 每件物品都有无限个（也就是可以放入背包多次），完全背包和01背包问题唯一不同的地方就是，每种物品有无限件。
- 之前的一维实现，用倒序遍历，避免重复pick up，现在直接改成正序就好了

```python
def test_CompletePack(weight, value, bagWeight):
    dp = [0] * (bagWeight + 1)
    for i in range(len(weight)):  # 遍历物品
        for j in range(weight[i], bagWeight + 1):  # 遍历背包容量
            dp[j] = max(dp[j], dp[j - weight[i]] + value[i])
    return dp[bagWeight]
```

### 518. 零钱兑换 II 
- 给定不同面额的硬币和一个总金额。写出函数来计算可以凑成总金额的硬币组合数。假设每一种面额的硬币有无限个。
- 就是上面的那个

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0]*(amount + 1)
        dp[0] = 1
        # 遍历物品
        for i in range(len(coins)):
            # 遍历背包
            for j in range(coins[i], amount + 1):
                dp[j] += dp[j - coins[i]]
        return dp[amount]
```

### 377. 组合总和 Ⅳ
- 给定一个由正整数组成且不存在重复数字的数组，找出和为给定目标正整数的组合的个数。
- 顺序不同的序列被视作不同的组合。
- 可以重复取

```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        dp = [0] * (target + 1)
        dp[0] = 1
        for i in range(1, target + 1):  # 遍历背包
            for j in range(len(nums)):  # 遍历物品
                if i - nums[j] >= 0:
                    dp[i] += dp[i - nums[j]]
        return dp[target]
```


### 70. 爬楼梯 （进阶）
- 一步一个台阶，两个台阶，三个台阶，.......，直到 m个台阶。问有多少种不同的方法可以爬到楼顶
- 1阶，2阶，.... m阶就是物品，楼顶就是背包。每一阶可以重复使用，例如跳了1阶，还可以继续跳1阶。
- 此时大家应该发现这就是一个完全背包问题
- dp[i]：爬到有i个台阶的楼顶，有dp[i]种方法

```python
def climbing_stairs(n,m):
    dp = [0]*(n+1) # 背包总容量
    dp[0] = 1 
    # 排列题，注意循环顺序，背包在外物品在内
    for j in range(1,n+1):
        for i in range(1,m+1):
            if j>=i:
                dp[j] += dp[j-i] # 这里i就是重量而非index
    return dp[n]
```


