### dijkstra（堆优化版）精讲
- 有权重的图的表达
    - 相邻矩阵，most straight forward way 
    - 相邻表，链表中加入权重，<节点，权重>
- 堆的优化
    - 和边有关，和节点无关的方法
- 利用了小顶堆自动排序的function，直接pop

```python
import heapq

class Edge:
    def __init__(self, to, val):
        self.to = to
        self.val = val

def dijkstra(n, m, edges, start, end):
    grid = [[] for _ in range(n + 1)]

    for p1, p2, val in edges:
        grid[p1].append(Edge(p2, val))

    minDist = [float('inf')] * (n + 1)
    visited = [False] * (n + 1)

    pq = []
    heapq.heappush(pq, (0, start))
    minDist[start] = 0

    while pq:
        cur_dist, cur_node = heapq.heappop(pq)

        if visited[cur_node]:
            continue

        visited[cur_node] = True

        for edge in grid[cur_node]:
            if not visited[edge.to] and cur_dist + edge.val < minDist[edge.to]:
                minDist[edge.to] = cur_dist + edge.val
                heapq.heappush(pq, (minDist[edge.to], edge.to))

    return -1 if minDist[end] == float('inf') else minDist[end]

# 输入
n, m = map(int, input().split())
edges = [tuple(map(int, input().split())) for _ in range(m)]
start = 1  # 起点
end = n    # 终点

# 运行算法并输出结果
result = dijkstra(n, m, edges, start, end)
print(result)
```


### Bellman_ford 算法精讲
- 和之前的问题很像，唯一区别是边的权值，允许有负数存在
- 松弛（relax edge）：
    - 通过 A 到 B 这条边可以获得更短的到达B节点的路径，即如果 minDist[B] > minDist[A] + value，那么我们就更新 minDist[B] = minDist[A] + value ，这个过程就叫做 “松弛” 
    - minDist[B] = min(minDist[A] + value, minDist[B])
- 之前的minDist更新策略：对所有的边，进行relax
    - 有点局部最优解的意思
    - 对所有边松弛一次，相当于计算 起点到达 **与起点一条边相连的节点** 的最短距离。
    - 那么再回归刚刚的问题，需要对所有边松弛几次才能得到 起点（节点1） 到终点（节点6）的最短距离呢？
        - 节点数量为n，那么起点到终点，最多是 n-1 条边相连。

```python
def main():
    n, m = map(int, input().strip().split())
    edges = []
    for _ in range(m):
        src, dest, weight = map(int, input().strip().split())
        edges.append([src, dest, weight])
    
    minDist = [float("inf")] * (n + 1)
    minDist[1] = 0  # 起点处距离为0
    
    for i in range(1, n):
        updated = False
        for src, dest, weight in edges:
            if minDist[src] != float("inf") and minDist[src] + weight < minDist[dest]:
                minDist[dest] = minDist[src] + weight
                updated = True
        if not updated:  # 若边不再更新，即停止回圈
            break
    
    if minDist[-1] == float("inf"):  # 返还终点权重
        return "unconnected"
    return minDist[-1]
    
if __name__ == "__main__":
    print(main())
```

