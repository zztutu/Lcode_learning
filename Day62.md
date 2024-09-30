### Floyd 算法精讲
- 动态规划，求局部最优，求递推公式
- 节点之间的最短距离，可以通过细分节点来求
- grid[i][j][k] = m，表示 节点i 到 节点j 以[1...k] 集合为中间节点的最短距离为m。
    - 因为细分节点，会有很多种组合，求最短距离
- 递推公式: grid[i][j][k] = min(grid[i][k][k - 1] + grid[k][j][k - 1]， grid[i][j][k - 1])
    - 节点i 到 节点j 的最短路径经过节点k
        - grid[i][j][k] = grid[i][k][k - 1] + grid[k][j][k - 1]
    - 节点i 到 节点j 的最短路径不经过节点k
        - grid[i][j][k] = grid[i][j][k - 1]

```python
if __name__ == '__main__':
    max_int = 10005  # 设置最大路径，因为边最大距离为10^4

    n, m = map(int, input().split())

    grid = [[[max_int] * (n+1) for _ in range(n+1)] for _ in range(n+1)]  # 初始化三维dp数组

    for _ in range(m):
        p1, p2, w = map(int, input().split())
        grid[p1][p2][0] = w
        grid[p2][p1][0] = w

    # 开始floyd
    for k in range(1, n+1):
        for i in range(1, n+1):
            for j in range(1, n+1):
                grid[i][j][k] = min(grid[i][j][k-1], grid[i][k][k-1] + grid[k][j][k-1])

    # 输出结果
    z = int(input())
    for _ in range(z):
        start, end = map(int, input().split())
        if grid[start][end][n] == max_int:
            print(-1)
        else:
            print(grid[start][end][n])
```

### A * 算法精讲 （A star算法）
-  BFS 是没有目的性的 一圈一圈去搜索， 而 A * 是有方向性的去搜索。
- 

```python
import heapq
 
n = int(input())
 
moves = [(1, 2), (2, 1), (-1, 2), (2, -1), (1, -2), (-2, 1), (-1, -2), (-2, -1)]
 
def distance(a, b):
    return ((a[0] - b[0]) ** 2 + (a[1] - b[1]) ** 2) ** 0.5
 
def bfs(start, end):
    q = [(distance(start, end), start)]
    step = {start: 0}
     
    while q:
        d, cur = heapq.heappop(q)
        if cur == end:
            return step[cur]
        for move in moves:
            new = (move[0] + cur[0], move[1] + cur[1])
            if 1 <= new[0] <= 1000 and 1 <= new[1] <= 1000:
                step_new = step[cur] + 1
                if step_new < step.get(new, float('inf')):
                    step[new] = step_new
                    heapq.heappush(q, (distance(new, end) + step_new, new))
    return False
                     
for _ in range(n):
    a1, a2, b1, b2 = map(int, input().split())
    print(bfs((a1, a2), (b1, b2)))
```

