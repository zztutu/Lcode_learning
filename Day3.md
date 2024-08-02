### 203 移除链表元素
- 虚拟头结点的使用 dummy head
``` python
dummy_head = ListNode(next = head)
current = dummy_head
```
- 链表遍历
``` python
while current.next:
    if current.next.val == val:
        current.next = current.next.next
    else:
        current = current.next
```
### 707 设计链表
- huge pain in the ass
- index是从0开始

### 206 反转链表
- exchange element 
```python
temp = cur.next
cur.next = pre #反转
#更新pre、cur指针
pre = cur
cur = temp
```
![](https://code-thinking.cdn.bcebos.com/gifs/206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.gif)