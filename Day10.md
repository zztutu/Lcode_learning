> 栈(stack) 提供 push 和 pop 等接口，所有元素必须符合先进后出规则
> 队列(queue)，先进先出的数据结构

### 232.用栈实现队列
- push(x) -- 将一个元素放入队列的尾部。
- pop() -- 从队列首部移除元素。
- peek() -- 返回队列首部的元素。
- empty() -- 返回队列是否为空。
> stack: self.stack = []
> pop: Removes the element from in front of queue and returns that element.

```python
class MyQueue:

    def __init__(self):
        """
        in主要负责push，out主要负责pop
        """
        self.stack_in = []
        self.stack_out = []


    def push(self, x: int) -> None:
        """
        有新元素进来，就往in里面push
        """
        self.stack_in.append(x)


    def pop(self) -> int:
        """
        Removes the element from in front of queue and returns that element.
        """
        if self.empty():
            return None
        
        if self.stack_out:
            return self.stack_out.pop()
        else:
            for i in range(len(self.stack_in)):
                self.stack_out.append(self.stack_in.pop())
            return self.stack_out.pop()


    def peek(self) -> int:
        """
        Get the front element.
        """
        ans = self.pop()
        self.stack_out.append(ans)
        return ans


    def empty(self) -> bool:
        """
        只要in或者out有元素，说明队列不为空
        """
        return not (self.stack_in or self.stack_out)
```


### 225. 用队列实现栈 
> queue in python, deque()
> top/pop in stack with queue: popleft() return the last one
```python
for i in range(len(self.queue_in) - 1):
    self.queue_out.append(self.queue_in.popleft())
self.queue_in, self.queue_out = self.queue_out, self.queue_in 
temp = self.queue_out.popleft()   
self.queue_in.append(temp)
```
```python
for i in range(len(self.queue_in) - 1):
    self.queue_out.append(self.queue_in.popleft())
self.queue_in, self.queue_out = self.queue_out, self.queue_in    # 交换in和out，这也是为啥in只用来存
return self.queue_out.popleft()
```


### 20. 有效的括号
> 这种对消匹配的问题，用stack
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        
        for item in s:
            if item == '(':
                stack.append(')')
            elif item == '[':
                stack.append(']')
            elif item == '{':
                stack.append('}')
            elif not stack or stack[-1] != item:
                return False
            else:
                stack.pop()
        
        return True if not stack else False
```


### 1047. 删除字符串中的所有相邻重复项 
- 匹配对消，stack

```python
# 方法一，使用栈
class Solution:
    def removeDuplicates(self, s: str) -> str:
        res = list()
        for item in s:
            if res and res[-1] == item:
                res.pop()
            else:
                res.append(item)
        return "".join(res)  # 字符串拼接
```