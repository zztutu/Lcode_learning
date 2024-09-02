### 62.不同路径 
- 机器人每次只能向下或者向右移动一步
- dp[i][j] ：表示从（0 ，0）出发，到(i, j) 有dp[i][j]条不同的路径。
- 二维的迭代
- update table

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # 创建一个二维列表用于存储唯一路径数
        dp = [[0] * n for _ in range(m)]
        
        # 设置第一行和第一列的基本情况
        for i in range(m):
            dp[i][0] = 1
        for j in range(n):
            dp[0][j] = 1
        
        # 计算每个单元格的唯一路径数
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        
        # 返回右下角单元格的唯一路径数
        return dp[m - 1][n - 1]
```

###  63. 不同路径 II 
- 现在考虑网格中有障碍物
- 其实也就是，all possibilities中，select，一部分的结果，在哪里，如何，进行condition？
  - 因为有了障碍，(i, j)如果就是障碍的话应该就保持初始状态（初始状态为0）
- dp[i][j] ：表示从（0 ，0）出发，到(i, j) 有dp[i][j]条不同的路径。
- 二维的这种问题，本质和RL中的policy function，是一样的，update all table along iterations

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid):
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])
        if obstacleGrid[m - 1][n - 1] == 1 or obstacleGrid[0][0] == 1:
            return 0
        dp = [[0] * n for _ in range(m)]
        for i in range(m):
            if obstacleGrid[i][0] == 0:  # 遇到障碍物时，直接退出循环，后面默认都是0
                dp[i][0] = 1
            else:
                break
        for j in range(n):
            if obstacleGrid[0][j] == 0:
                dp[0][j] = 1
            else:
                break
        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j] == 1:
                    continue
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return dp[m - 1][n - 1]
```
