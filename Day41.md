### 121. 买卖股票的最佳时机
- 只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。
- dp[i][0]表示在第i天结束时持有股票所得到的最大收益，
- 而dp[i][1]表示在第i天结束时不持有股票所得到的最大收益。
- 动规中结合分类讨论的方式，之前的题目也有涉及
- max(dp[i-1][1], prices[i] + dp[i-1][0])

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        length = len(prices)
        if len == 0:
            return 0
        dp = [[0] * 2 for _ in range(length)]
        dp[0][0] = -prices[0]
        dp[0][1] = 0
        for i in range(1, length):
            dp[i][0] = max(dp[i-1][0], -prices[i])
            dp[i][1] = max(dp[i-1][1], prices[i] + dp[i-1][0])
        return dp[-1][1] #肯定最后卖出收益最大咯
```

### 122.买卖股票的最佳时机II
- 你可以尽可能地完成更多的交易（多次买卖一支股票）。和上面的区别，n次交易
- 收益可以由两个状态推出来
- 动规结合分类讨论

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        length = len(prices)
        dp = [[0] * 2 for _ in range(length)]
        dp[0][0] = -prices[0]
        dp[0][1] = 0
        for i in range(1, length):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1] - prices[i]) #注意这里是和上面唯一不同的地方
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] + prices[i])
        return dp[-1][1]
```


### 123.买卖股票的最佳时机III
- 你最多可以完成 两笔 交易。
- 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
- 分类讨论极致了
- 1，3 是持有; 2，4是不持有

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) == 0:
            return 0
        dp = [[0] * 5 for _ in range(len(prices))]
        dp[0][1] = -prices[0]
        dp[0][3] = -prices[0]
        for i in range(1, len(prices)):
            dp[i][0] = dp[i-1][0]
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] - prices[i])
            dp[i][2] = max(dp[i-1][2], dp[i-1][1] + prices[i])
            dp[i][3] = max(dp[i-1][3], dp[i-1][2] - prices[i])
            dp[i][4] = max(dp[i-1][4], dp[i-1][3] + prices[i])
        return dp[-1][4]
```