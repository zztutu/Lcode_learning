### 108.冗余连接
- 找出冗余边，删除后，使该图可以重新变成一棵树
- 环：如果边的两个节点已经出现在同一个集合里，说明着边的两个节点已经连在一起了，再加入这条边一定就出现环了。
  - 判断 节点A 和 节点B 在在同一个集合（同一个根），如果将 节点A 和 节点B 连在一起就一定会出现环。

```python
class UnionFind:
    def __init__(self, n):
        # Initialize father array for the Union-Find (Disjoint Set) structure
        self.father = list(range(n + 1))
    
    def find(self, u):
        # Find the root of node u with path compression
        if u != self.father[u]:
            self.father[u] = self.find(self.father[u])
        return self.father[u]
    
    def union(self, u, v):
        # Connect the roots of u and v
        root_u = self.find(u)
        root_v = self.find(v)
        if root_u != root_v:
            self.father[root_v] = root_u

    def is_same(self, u, v):
        # Check if u and v share the same root (i.e., are in the same set)
        return self.find(u) == self.find(v)


def findRedundantConnection(edges):
    n = len(edges)
    # Initialize Union-Find with size n (number of nodes)
    uf = UnionFind(n)
    
    # Process each edge
    for u, v in edges:
        # If u and v are already connected, it means this edge is redundant
        if uf.is_same(u, v):
            return [u, v]
        else:
            uf.union(u, v)

# Example usage
edges = [[1, 2], [1, 3], [2, 3]]  # Example input for problem 684
print(findRedundantConnection(edges))  # Output should be [2, 3]

```

### 109.冗余连接II  
- 有向图
- 分析节点的度：
  - 如果发现入度为2的节点，我们需要判断 删除哪一条边，删除后本图能成为有向树。如果是删哪个都可以，优先删顺序靠后的边。
  - 如果没有入度为2的点，说明 图中有环了（注意是有向环）删掉构成环的边就可以了

```python
class UnionFind:
    def __init__(self, n):
        # Initialize the father array
        self.father = list(range(n + 1))

    def find(self, u):
        # Path compression while finding the root of u
        if u != self.father[u]:
            self.father[u] = self.find(self.father[u])
        return self.father[u]

    def union(self, u, v):
        # Union by root
        root_u = self.find(u)
        root_v = self.find(v)
        if root_u != root_v:
            self.father[root_v] = root_u

    def same(self, u, v):
        # Check if u and v have the same root
        return self.find(u) == self.find(v)

def is_tree_after_remove_edge(edges, n, delete_edge):
    uf = UnionFind(n)
    for i in range(len(edges)):
        if i == delete_edge:
            continue
        u, v = edges[i]
        if uf.same(u, v):
            return False
        uf.union(u, v)
    return True

def get_remove_edge(edges, n):
    uf = UnionFind(n)
    for u, v in edges:
        if uf.same(u, v):
            return [u, v]  # Found the cycle, return the edge causing it
        else:
            uf.union(u, v)
    return []

def findRedundantDirectedConnection(edges):
    n = len(edges)
    in_degree = [0] * (n + 1)  # To store the indegree of each node
    vec = []  # To store the index of edges where a node has 2 parents

    # Step 1: Find the nodes with indegree 2
    for i, (u, v) in enumerate(edges):
        in_degree[v] += 1
        if in_degree[v] == 2:
            vec.append(i)

    # Step 2: If there's a node with two parents
    if vec:
        # Check removing the first or second edge leads to a valid tree
        if is_tree_after_remove_edge(edges, n, vec[0]):
            return edges[vec[0]]
        else:
            return edges[vec[1]]

    # Step 3: If no node has two parents, find the edge forming the cycle
    return get_remove_edge(edges, n)

# Example usage:
edges = [[1, 2], [1, 3], [2, 3]]  # Example input
print(findRedundantDirectedConnection(edges))  # Output should be [2, 3]

```