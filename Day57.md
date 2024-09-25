### 53.寻宝
- 非常有名的问题，先只看prim的算法
- minDist这个数组更新的问题，之前str匹配的一个算法，也用到了类似的思路
  - 接下来选哪个点：当遍历到n的时候，我们要看n和n之前所有的节点，和剩余节点的距离，然后取最小的来加入
  - 最小距离如何求：要考虑n和n之前所有的点，和新点的距离，而不是只是n和其他点的距离，比较求最小，合理
  - minDist在不停更新，每一个有必要的index

```python
# 接收输入
v, e = list(map(int, input().strip().split()))
# 按照常规的邻接矩阵存储图信息，不可达的初始化为10001
graph = [[10001] * (v+1) for _ in range(v+1)]
for _ in range(e):
    x, y, w = list(map(int, input().strip().split()))
    graph[x][y] = w
    graph[y][x] = w

# 定义加入生成树的标记数组和未加入生成树的最近距离
visited = [False] * (v + 1)
minDist = [10001] * (v + 1)

# 循环 n - 1 次，建立 n - 1 条边
# 从节点视角来看：每次选中一个节点加入树，更新剩余的节点到树的最短距离，
# 这一步其实蕴含了确定下一条选取的边，计入总路程 ans 的计算
for _ in range(1, v + 1):
    min_val = 10002
    cur = -1
    for j in range(1, v + 1):
        if visited[j] == False and minDist[j] < min_val:
            cur = j
            min_val = minDist[j]
    visited[cur] = True
    for j in range(1, v + 1):
        if visited[j] == False and minDist[j] > graph[cur][j]:
            minDist[j] = graph[cur][j]

ans = 0
for i in range(2, v + 1):
    ans += minDist[i]
print(ans)
```