### 107. 寻找存在的路径
- 判断是否有一条从节点 source 出发到节点 destination 的路径存在
- 路径压缩：

#### 我们来看一个具体的例子，有以下结构：
```
u -> v -> w -> x (根节点)
```

现在，我们执行 `find(u)`：

1. 初始调用 `find(u)`：
   - 因为 `u != father[u]`，进入 `find(father[u])`，即 `find(v)`。
   
2. 继续调用 `find(v)`：
   - 因为 `v != father[v]`，进入 `find(father[v])`，即 `find(w)`。
   
3. 继续调用 `find(w)`：
   - 因为 `w != father[w]`，进入 `find(father[w])`，即 `find(x)`。
   
4. 调用 `find(x)`：
   - 因为 `x == father[x]`，所以返回 `x`，表示找到了根节点。

到这里，递归调用结束，开始逐层返回，并在返回的过程中压缩路径。

- 返回到 `w`，现在 `father[w] = x`（即 `w` 的父节点直接被更新为根节点 `x`）。
- 返回到 `v`，现在 `father[v] = x`（`v` 的父节点也直接指向根节点 `x`）。
- 返回到 `u`，现在 `father[u] = x`（`u` 也直接指向根节点 `x`）。

#### 路径压缩后的效果
压缩路径后，原本是 `u -> v -> w -> x` 的路径，现在变成了：

```
u -> x
v -> x
w -> x
x -> x (根节点)
```

这样，下次再查询 `find(u)` 时，只需要一次递归就能直接得到根节点 `x`，不需要再次经过 `v` 和 `w`。

#### 总结
虽然 `find(father[u])` 是递归调用，但是**路径压缩**在递归返回的过程中起作用，最终使得经过的每个节点都直接指向根节点，从而加快以后对这些节点的查询。

```python
class UnionFind:
    def __init__(self, size):
        self.parent = list(range(size + 1))  # 初始化并查集

    def find(self, u):
        if self.parent[u] != u:
            self.parent[u] = self.find(self.parent[u])  # 路径压缩
        return self.parent[u]

    def union(self, u, v):
        root_u = self.find(u)
        root_v = self.find(v)
        if root_u != root_v:
            self.parent[root_v] = root_u

    def is_same(self, u, v):
        return self.find(u) == self.find(v)


def main():
    import sys
    input = sys.stdin.read
    data = input().split()
    
    index = 0
    n = int(data[index])
    index += 1
    m = int(data[index])
    index += 1
    
    uf = UnionFind(n)
    
    for _ in range(m):
        s = int(data[index])
        index += 1
        t = int(data[index])
        index += 1
        uf.union(s, t)
    
    source = int(data[index])
    index += 1
    destination = int(data[index])
    
    if uf.is_same(source, destination):
        print(1)
    else:
        print(0)

if __name__ == "__main__":
    main()
```