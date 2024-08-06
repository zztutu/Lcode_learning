### 反转字符串
- inplace 
- 字符串遍历
- 
```python
while left < right:
    s[left], s[right] = s[right], s[left]
    left += 1
    right -= 1
```


### 反转字符串2
- 指定位置的replcae
- 遍历

```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        # Two pointers. Another is inside the loop.
        p = 0
        while p < len(s):
            p2 = p + k
            # Written in this could be more pythonic.
            s = s[:p] + s[p: p2][::-1] + s[p2:]
            p = p + 2 * k
        return s
```

### 替换数字
- .join
- 
```python
class Solution:
    def change(self, s):
        lst = list(s) # Python里面的string也是不可改的，所以也是需要额外空间的。空间复杂度：O(n)。
        for i in range(len(lst)):
            if lst[i].isdigit():
                lst[i] = "number"
        return ''.join(lst)
```