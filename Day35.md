### 01背包问题 二维
- 01背包，因为元素我们只能用一次
- 将哪些物品装入背包里物品价值总和最大
- dp[i][j] 表示从下标为[0-i]的物品里任意取，放进容量为j的背包，价值总和最大是多少
  - max
  - 放物品1 的情况 = dp[0][1] + 物品1 的价值，也可以是不放的情况
  - dp[1][4] = max(dp[0][4], dp[0][1] + 物品1 的价值)
  - 状态转移：dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);
- 初始化：二维问题，两个维度初始化
- 遍历：两种方式，两个维度遍历方式

```python
n, bagweight = map(int, input().split())
weight = list(map(int, input().split()))
value = list(map(int, input().split()))

dp = [[0] * (bagweight + 1) for _ in range(n)]
for j in range(weight[0], bagweight + 1):
    dp[0][j] = value[0]

for i in range(1, n):
    for j in range(bagweight + 1):
        if j < weight[i]:
            dp[i][j] = dp[i - 1][j]
        else:
            dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i])

print(dp[n - 1][bagweight])
```


### 01背包问题 一维 
- 滚动数组：其实就是动态更新，这个和RL中的policy，value function求解非常相似
- dp[j]为 容量为j的背包所背的最大价值
  - dp[j]可以通过dp[j - weight[i]]推导出来，dp[j - weight[i]]表示容量为j - weight[i]的背包所背的最大价值。
  - dp[j - weight[i]] + value[i] 表示 容量为 [j - 物品i重量] 的背包 加上 物品i的价值。（也就是容量为j的背包，放入物品i了之后的价值即：dp[j]）
  - 此时dp[j]有两个选择，一个是取自己dp[j] 相当于 二维dp数组中的dp[i-1][j]，即不放物品i，一个是取dp[j - weight[i]] + value[i]，即放物品i，指定是取最大的，毕竟是求最大价值，
- 状态转移：dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
- 倒序遍历，就可以保证物品只放入一次
  - 没太想明白，直觉上感觉是因为重量和value重复使用一个position照成的

```python
n, bagweight = map(int, input().split())

weight = list(map(int, input().split()))
value = list(map(int, input().split()))

dp = [[0] * (bagweight + 1) for _ in range(n)]

for j in range(weight[0], bagweight + 1):
    dp[0][j] = value[0]

for i in range(1, n):
    for j in range(bagweight + 1):
        if j < weight[i]:
            dp[i][j] = dp[i - 1][j]
        else:
            dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i])

print(dp[n - 1][bagweight])
```

### 416. 分割等和子集
- 背包容量就是sum/2，item价值就是element值
- 求解最大价值是否和xxx相等这么个问题

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        if sum(nums) % 2 != 0:
            return False
        target = sum(nums) // 2
        dp = [0] * (target + 1)
        for num in nums:
            for j in range(target, num-1, -1):
                dp[j] = max(dp[j], dp[j-num] + num)
        return dp[-1] == target
```