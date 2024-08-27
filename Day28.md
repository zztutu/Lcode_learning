### 122.买卖股票的最佳时机II 
- 你在任何时候 最多 只能持有 一股 股票。
- 这个题还是蛮奇怪的
- 找递增数列？
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        result = 0
        for i in range(1, len(prices)):
            result += max(prices[i] - prices[i - 1], 0)
        return result
```


### 55. 跳跃游戏
- 数组中的每个元素代表你在该位置可以跳跃的最大长度。
- 贪心算法局部最优解：每次取最大跳跃步数（取最大覆盖范围）
- 其实就是，在一步的过程中，走最大
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        cover = 0
        if len(nums) == 1: return True
        i = 0
        # python不支持动态修改for循环中变量,使用while循环代替
        while i <= cover:
            cover = max(i + nums[i], cover)
            if cover >= len(nums) - 1: return True
            i += 1
        return False
```

### 45.跳跃游戏II
- 你的目标是使用最少的跳跃次数到达数组的最后一个位置。
- 从覆盖范围出发，以最小的步数增加覆盖范围，覆盖范围一旦覆盖了终点，得到的就是最少步数
- 当前距离和下一个距离，有个比较
  
```python
class Solution:
    def jump(self, nums):
        cur_distance = 0  # 当前覆盖的最远距离下标
        ans = 0  # 记录走的最大步数
        next_distance = 0  # 下一步覆盖的最远距离下标
        
        for i in range(len(nums) - 1):  # 注意这里是小于len(nums) - 1，这是关键所在
            next_distance = max(nums[i] + i, next_distance)  # 更新下一步覆盖的最远距离下标
            if i == cur_distance:  # 遇到当前覆盖的最远距离下标
                cur_distance = next_distance  # 更新当前覆盖的最远距离下标
                ans += 1
        
        return ans
```



### 1005.K次取反后最大化的数组和 
- 是一个蛮奇怪的题目
- 贪心在于把所有的负数去做reverse
- 如果都是正数，找到最小的元素
  
```python
class Solution:
    def largestSumAfterKNegations(self, A: List[int], K: int) -> int:
        A.sort(key=lambda x: abs(x), reverse=True)  # 第一步：按照绝对值降序排序数组A

        for i in range(len(A)):  # 第二步：执行K次取反操作
            if A[i] < 0 and K > 0:
                A[i] *= -1
                K -= 1

        if K % 2 == 1:  # 第三步：如果K还有剩余次数，将绝对值最小的元素取反
            A[-1] *= -1

        result = sum(A)  # 第四步：计算数组A的元素和
        return result
```
