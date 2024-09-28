### Bellman_ford 队列优化算法（又名SPFA）
- 相比原始的bellman ford算法，优化在哪里
    - 只需要对 上一次松弛的时候更新过的节点作为出发节点所连接的边 进行松弛就够了
    - 找到变化的边呗
    - 基于队列优化的算法，要比bellman_ford 算法 减少很多无用的松弛情况，特别是对于边数众多的大图 优化效果明显。

```python
import collections

def main():
    n, m = map(int, input().strip().split())
    edges = [[] for _ in range(n + 1)]
    for _ in range(m):
        src, dest, weight = map(int, input().strip().split())
        edges[src].append([dest, weight])
    
    minDist = [float("inf")] * (n + 1)
    minDist[1] = 0
    que = collections.deque([1])
    visited = [False] * (n + 1)
    visited[1] = True
    
    while que:
        cur = que.popleft()
        visited[cur] = False
        for dest, weight in edges[cur]:
            if minDist[cur] != float("inf") and minDist[cur] + weight < minDist[dest]:
                minDist[dest] = minDist[cur] + weight
                if visited[dest] == False:
                    que.append(dest)
                    visited[dest] = True
    
    if minDist[-1] == float("inf"):
        return "unconnected"
    return minDist[-1]

if __name__ == "__main__":
    print(main())
```


### bellman_ford之判断负权回路
- 负权回路是指一系列道路的总权值为负，这样的回路使得通过反复经过回路中的道路，理论上可以无限地减少总成本或无限地增加总收益。
    - 还的检测
- impact：使用bellman_ford 算法对边进行松弛n次以上，因为 有负权回路 就是可以无限最短路径（一直绕圈，就可以一直得到无限小的最短距离）。每松弛一次，都会更新最短路径，所以结果会一直有变化。
- key：那么解决本题的 核心思路，就是在 kama94.城市间货物运输I 的基础上，再多松弛一次，看minDist数组 是否发生变化。

```python
import sys

def main():
    input = sys.stdin.read
    data = input().split()
    index = 0
    
    n = int(data[index])
    index += 1
    m = int(data[index])
    index += 1
    
    grid = []
    for i in range(m):
        p1 = int(data[index])
        index += 1
        p2 = int(data[index])
        index += 1
        val = int(data[index])
        index += 1
        # p1 指向 p2，权值为 val
        grid.append([p1, p2, val])

    start = 1  # 起点
    end = n    # 终点

    minDist = [float('inf')] * (n + 1)
    minDist[start] = 0
    flag = False

    for i in range(1, n + 1):  # 这里我们松弛n次，最后一次判断负权回路
        for side in grid:
            from_node = side[0]
            to = side[1]
            price = side[2]
            if i < n:
                if minDist[from_node] != float('inf') and minDist[to] > minDist[from_node] + price:
                    minDist[to] = minDist[from_node] + price
            else:  # 多加一次松弛判断负权回路
                if minDist[from_node] != float('inf') and minDist[to] > minDist[from_node] + price:
                    flag = True

    if flag:
        print("circle")
    elif minDist[end] == float('inf'):
        print("unconnected")
    else:
        print(minDist[end])

if __name__ == "__main__":
    main()

```


### bellman_ford之单源有限最短路
- 最多经过 k 个城市的条件下，而不是一定经过k个城市，也可以经过的城市数量比k小，但要最短的路径。
    - 有条件约束下的最值问题
- 对所有边松弛一次，相当于计算 起点到达 与起点一条边相连的节点 的最短距离，那么对所有边松弛 k + 1次，就是求 起点到达 与起点k + 1条边相连的节点的 最短距离。
    - 转化为更新次数有limited情况下，最短距离

```c++
#include <iostream>
#include <vector>
#include <list>
#include <climits>
using namespace std;

int main() {
    int src, dst,k ,p1, p2, val ,m , n;
    
    cin >> n >> m;

    vector<vector<int>> grid;

    for(int i = 0; i < m; i++){
        cin >> p1 >> p2 >> val;
        // p1 指向 p2，权值为 val
        grid.push_back({p1, p2, val});
    }

    cin >> src >> dst >> k;

    vector<int> minDist(n + 1 , INT_MAX);
    minDist[src] = 0;
    for (int i = 1; i <= k + 1; i++) { // 对所有边松弛 k + 1次
        for (vector<int> &side : grid) {
            int from = side[0];
            int to = side[1];
            int price = side[2];
            if (minDist[from] != INT_MAX && minDist[to] > minDist[from] + price) minDist[to] = minDist[from] + price;
        }
        // 打印 minDist 数组 
        for (int j = 1; j <= n; j++) cout << minDist[j] << " ";
        cout << endl;

    }

    if (minDist[dst] == INT_MAX) cout << "unreachable" << endl; // 不能到达终点
    else cout << minDist[dst] << endl; // 到达终点最短路径

}

```