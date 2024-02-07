
102. binary-tree-level-order-traversal

S: level traversal template via recursion methods:
```python
def levelTraversal(self, root):
    levels = []
    self.traversalLayer(root, 0, levels)
    return levels
def traversalLayer(self, note, level, levels):
    if not note:
        return
    if len(levels) == level:
        return []
    levels[level].append(node.val)
    self.traversalLayer(node.left, level+1, levels)
    self.traversalLayer(node.right, level+1, levels)
```

S: template via queue:
```python
def levelTraversal(self, root):
    if not root:
        return []
    queue = collections.deque([root])
    result = []
    while queue:
        level = []
        for _ in range(len(queue)):
            cur = queue.popleft()
            level.append(cur.val)
            if cur.left:
                queue.append(cur.left)
            if cur.right:
                queue.append(cur.right)
        result.append(level)
    return result 
```

### Sources
- [video illustration for layerTraversal](https://www.google.com/search?q=+binary-tree-level-order-traversal+python+recursion&sca_esv=f3a40c3638357365&biw=1774&bih=934&tbm=vid&sxsrf=ACQVn08A8VP-Fytu6c0QpAwkXiAsyec6Ww%3A1707267566941&ei=7tXCZYGGOc7d2roPjd2w4Aw&ved=0ahUKEwiBtfSmg5iEAxXOrlYBHY0uDMwQ4dUDCA0&uact=5&oq=+binary-tree-level-order-traversal+python+recursion&gs_lp=Eg1nd3Mtd2l6LXZpZGVvIjMgYmluYXJ5LXRyZWUtbGV2ZWwtb3JkZXItdHJhdmVyc2FsIHB5dGhvbiByZWN1cnNpb24yCBAAGIAEGKIEMggQABiABBiiBEjc2gFQuZQBWIXVAXACeACQAQCYAcQCoAGuJaoBCDAuMy4xNy4xuAEDyAEA-AEC-AEBwgIEECMYJ8ICCBAAGIAEGMsBwgIEEAAYHsICBhAAGB4YCsICBhAAGAgYHsICBxAhGAoYoAGIBgE&sclient=gws-wiz-video#fpstate=ive&vld=cid:8e5deac8,vid:lXIk1PXb1Jc,st:0)