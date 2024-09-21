### 99. 岛屿数量 深搜
- 这个题目，cv2有函数，可以直接求连通区域，连通区域的构成，参数4/8
- 思路：遇到一个没有遍历过的节点，计数+1

```python
direction = [[0, 1], [1, 0], [0, -1], [-1, 0]]  # 四个方向：上、右、下、左


def dfs(grid, visited, x, y):
    """
    对一块陆地进行深度优先遍历并标记
    """
    for i, j in direction:
        next_x = x + i
        next_y = y + j
        # 下标越界，跳过
        if next_x < 0 or next_x >= len(grid) or next_y < 0 or next_y >= len(grid[0]):
            continue
        # 未访问的陆地，标记并调用深度优先搜索
        if not visited[next_x][next_y] and grid[next_x][next_y] == 1:
            visited[next_x][next_y] = True
            dfs(grid, visited, next_x, next_y)


if __name__ == '__main__':  
    # 版本一
    n, m = map(int, input().split())
    
    # 邻接矩阵
    grid = []
    for i in range(n):
        grid.append(list(map(int, input().split())))
    
    # 访问表
    visited = [[False] * m for _ in range(n)]
    
    res = 0
    for i in range(n):
        for j in range(m):
            # 判断：如果当前节点是陆地，res+1并标记访问该节点，使用深度搜索标记相邻陆地。
            if grid[i][j] == 1 and not visited[i][j]:
                res += 1
                visited[i][j] = True
                dfs(grid, visited, i, j)
    
    print(res)
```

### 99. 岛屿数量 广搜
- 和之前的二叉树广搜很像了

```python
from collections import deque
directions = [[0, 1], [1, 0], [0, -1], [-1, 0]]
def bfs(grid, visited, x, y):
    que = deque([])
    que.append([x,y])
    while que:
        cur_x, cur_y = que.popleft()
        for i, j in directions:
            next_x = cur_x + i
            next_y = cur_y + j
            if next_y < 0 or next_x < 0 or next_x >= len(grid) or next_y >= len(grid[0]):
                continue
            if not visited[next_x][next_y] and grid[next_x][next_y] == 1: 
                visited[next_x][next_y] = True
                que.append([next_x, next_y])


def main():
    n, m = map(int, input().split())
    grid = []
    for i in range(n):
        grid.append(list(map(int, input().split())))
    visited = [[False] * m for _ in range(n)]
    res = 0
    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1 and not visited[i][j]:
                res += 1
                bfs(grid, visited, i, j)
    print(res)

if __name__ == "__main__":
    main()
```

### 100. 岛屿的最大面积
- 最大面积，像素之和咯

```python
# 四个方向
position = [[0, 1], [1, 0], [0, -1], [-1, 0]]
count = 0


def dfs(grid, visited, x, y):
    """
    深度优先搜索，对一整块陆地进行标记
    """
    global count  # 定义全局变量，便于传递count值
    for i, j in position:
        cur_x = x + i
        cur_y = y + j
        # 下标越界，跳过
        if cur_x < 0 or cur_x >= len(grid) or cur_y < 0 or cur_y >= len(grid[0]):
            continue
        if not visited[cur_x][cur_y] and grid[cur_x][cur_y] == 1:
            visited[cur_x][cur_y] = True
            count += 1
            dfs(grid, visited, cur_x, cur_y)


n, m = map(int, input().split())
# 邻接矩阵
grid = []
for i in range(n):
    grid.append(list(map(int, input().split())))
# 访问表
visited = [[False] * m for _ in range(n)]

result = 0  # 记录最终结果
for i in range(n):
    for j in range(m):
        if grid[i][j] == 1 and not visited[i][j]:
            count = 1
            visited[i][j] = True
            dfs(grid, visited, i, j)
            result = max(count, result)

print(result)

```