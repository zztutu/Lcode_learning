### 739. 每日温度 
- 通常是一维数组，要寻找任一个元素的右边或者左边第一个比自己大或者小的元素的位置，此时我们就要想到可以用单调栈了
- 本质是用空间换时间，用一个栈来记录我们遍历过的元素
- 有顺序的栈的建立：有条件的记录

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        answer = [0]*len(temperatures)
        stack = [0]
        for i in range(1,len(temperatures)):
            # 情况一和情况二
            if temperatures[i]<=temperatures[stack[-1]]:
                stack.append(i)
            # 情况三
            else:
                while len(stack) != 0 and temperatures[i]>temperatures[stack[-1]]:
                    answer[stack[-1]]=i-stack[-1]
                    stack.pop()
                stack.append(i)

        return answer
```

### 496.下一个更大元素 I
- 为什么用单调栈：显然要遍历，同时，可能跳过一些element，遍历中有条件的select
- 换个角度看，和上面一样，找到比xxx大的元素

```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        result = [-1]*len(nums1)
        stack = [0]
        for i in range(1,len(nums2)):
            # 情况一情况二
            if nums2[i]<=nums2[stack[-1]]:
                stack.append(i)
            # 情况三
            else:
                while len(stack)!=0 and nums2[i]>nums2[stack[-1]]:
                    if nums2[stack[-1]] in nums1:
                        index = nums1.index(nums2[stack[-1]])
                        result[index]=nums2[i]
                    stack.pop()                 
                stack.append(i)
        return result
```

### 503.下一个更大元素II 
- 区别：是有循环
- 循环的处理：之前有个小偷的，也有循环，处理
  - 拼接
  - 走两遍：在遍历的过程中模拟走了两边nums

```python
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        dp = [-1] * len(nums)
        stack = []
        for i in range(len(nums)*2):
            while(len(stack) != 0 and nums[i%len(nums)] > nums[stack[-1]]):
                    dp[stack[-1]] = nums[i%len(nums)]
                    stack.pop()
            stack.append(i%len(nums))
        return dp
```