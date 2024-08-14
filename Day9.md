### 151.翻转字符串里的单词
- word-level
- 遍历，切片
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        # 删除前后空白
        s = s.strip()
        # 反转整个字符串
        s = s[::-1]
        # 将字符串拆分为单词，并反转每个单词
        s = ' '.join(word[::-1] for word in s.split())
        return s
```


### 55.右旋转字符串
- 切片
```python
s = s[len(s)-k:] + s[:len(s)-k]
```

### 实现 strStr()
- 问题：匹配，找到起点
- 当出现字符串不匹配时，可以记录一部分之前已经匹配的文本内容，利用这些信息避免从头再去做匹配。
- Next: find first time position
- Main function: find length with same letters, if not, jump to last matched position

```python
def getNext(self, next, s):
        j = -1
        next[0] = j
        for i in range(1, len(s)):
            while j >= 0 and s[i] != s[j+1]:
                j = next[j]
            if s[i] == s[j+1]:
                j += 1
            next[i] = j
```

```python
for i in range(len(haystack)):
    while j >= 0 and haystack[i] != needle[j+1]:
        j = next[j]
    if haystack[i] == needle[j+1]:
        j += 1
    if j == len(needle) - 1:
        return i - len(needle) + 1
```
### 459.重复的子字符串
- kmp 
- the last next position value should be s/n

```python
if nxt[-1] != -1 and len(s) % (len(s) - (nxt[-1] + 1)) == 0:
    return True
```