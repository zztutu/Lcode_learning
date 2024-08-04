### 24. 两两交换链表中的节点
- 链表遍历，跳位的遍历
```python
while current.next and current.next.next:
    temp = current.next # 防止节点修改
    temp1 = current.next.next.next
            
    current.next = current.next.next
    current.next.next = temp
    temp.next = temp1
    current = current.next.next
```
### 19. 删除链表的倒数第 N 个结点
- 链表 iteration
```python
# 快指针比慢指针快 n+1 步
for i in range(n+1):
    fast = fast.next
# 移动两个指针，直到快速指针到达链表的末尾
while fast:
    slow = slow.next
    fast = fast.next
# 通过更新第 (n-1) 个节点的 next 指针删除第 n 个节点
slow.next = slow.next.next
```
### 面试题 02.07. 链表相交
- 如何判断相交
```python
# 遍历两个链表直到指针相交
while pointerA != pointerB:
    # 将指针向前移动一个节点
    pointerA = pointerA.next if pointerA else headB
    pointerB = pointerB.next if pointerB else headA
```
### 142. 环形链表 II
- 数学推导，求相接口
```python
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
            
# If there is a cycle, the slow and fast pointers will eventually meet
    if slow == fast:
# Move one of the pointers back to the start of the list
        slow = head
        while slow != fast:
            slow = slow.next
            fast = fast.next
        return slow
```