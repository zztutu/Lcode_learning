### 322. 零钱兑换
- 编写一个函数来计算可以凑成总金额所需的最少的硬币个数
  - 有多少种组合
  - 每个组合的物品个数，求最小
- dp[j] = min(dp[j - coins[i]] + 1, dp[j]);
  - 凑足总额为j所需钱币的最少个数为dp[j]
  - 注意最少
- 如果 dp[i - coin] 仍然是 float('inf'), 说明我们目前还无法通过任何组合得到容量为 i - coin 的背包, 因此也就不应该尝试更新 dp[i] 的值。
- if条件的问题，感觉和之前倒序的问题类似

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount + 1)  # 创建动态规划数组，初始值为正无穷大
        dp[0] = 0  # 初始化背包容量为0时的最小硬币数量为0

        for coin in coins:  # 遍历硬币列表，相当于遍历物品
            for i in range(coin, amount + 1):  # 遍历背包容量
                if dp[i - coin] != float('inf'):  # 如果dp[i - coin]不是初始值，则进行状态转移
                    dp[i] = min(dp[i - coin] + 1, dp[i])  # 更新最小硬币数量

        if dp[amount] == float('inf'):  # 如果最终背包容量的最小硬币数量仍为正无穷大，表示无解
            return -1
        return dp[amount]  # 返回背包容量为amount时的最小硬币数量
```


### 279.完全平方数 
- 和上面比较类似的了
- 有个问题是if为什么不需要
  - 对于任何 i,状态 dp[i] 一定是可以从某个子问题 dp[i - j*j] 转移过来的,不存在无解的情况。
  - 不是特别的明白

```python
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [float('inf')] * (n + 1)
        dp[0] = 0

        for i in range(1, n + 1):  # 遍历背包
            for j in range(1, int(i ** 0.5) + 1):  # 遍历物品
                # 更新凑成数字 i 所需的最少完全平方数数量
                dp[i] = min(dp[i], dp[i - j * j] + 1)
        return dp[n]
```



### 139.单词拆分
- 判断s是否可以被空格拆分为一个或多个在字典中出现的单词。
- 这个题比较容易想到匹配的算法，背包，还是蛮难想到的
- 一个思路是，大的问题，可以化成小的s解决，这个思路，可以想到背包
  - dp[i] : 字符串长度为i的话，dp[i]为true，表示可以拆分为一个或多个在字典中出现的单词。
- 递推公式
  - 如果确定dp[j] 是true，且 [j, i] 这个区间的子串出现在字典里，那么dp[i]一定是true。（j < i ）。
- dp[0]表示如果字符串为空的话，说明出现在字典里，为true。

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        wordSet = set(wordDict)
        n = len(s)
        dp = [False] * (n + 1)  # dp[i] 表示字符串的前 i 个字符是否可以被拆分成单词
        dp[0] = True  # 初始状态，空字符串可以被拆分成单词

        for i in range(1, n + 1): # 遍历背包
            for j in range(i): # 遍历单词
                if dp[j] and s[j:i] in wordSet:
                    dp[i] = True  # 如果 s[0:j] 可以被拆分成单词，并且 s[j:i] 在单词集合中存在，则 s[0:i] 可以被拆分成单词
                    break

        return dp[n]
```