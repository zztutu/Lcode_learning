### 209.长度最小的子数组
- 滑动窗口的典型例子，左右point动态调节
- output长度，动态比较调节
```
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        l = len(nums)
        left = 0
        right = 0
        min_len = float('inf')
        cur_sum = 0 #当前的累加值
        
        while right < l:
            cur_sum += nums[right]
            
            while cur_sum >= s: # 当前累加值大于目标值
                min_len = min(min_len, right - left + 1)
                cur_sum -= nums[left]
                left += 1
            
            right += 1
        
        return min_len if min_len != float('inf') else 0
```

### 59.螺旋矩阵II
比较古怪的题目，遍历，注意边界问题和offset的value


### 58. 区间和, 44. 开发商购买土地
> 前缀和算法（Prefix Sum: 它通过预先计算数组中每个位置前所有元素的累加和，将这些部分和存储在一个新的数组中，从而在需要计算某个区间的和时，可以通过简单的减法操作得到结果，而不必重新遍历整个区间。
- smart的操作，和后面KMP算法比较像，核心避免重复计算

> 一维前缀和：给定一个整数数组 Array，请计算该数组在每个指定区间内元素的总. (58. 区间和)

```
    p = [0] * n
    presum = 0
    for i in range(n):
        presum += vec[i]
        p[i] = presum

    results = []
    while index < len(data):
        a = int(data[index])
        b = int(data[index + 1])
        index += 2

        if a == 0:
            sum_value = p[b]
        else:
            sum_value = p[b] - p[a - 1]

        results.append(sum_value)
```
> 二维前缀和：给你一个n行m列的矩阵A ，下标从1开始。请输出以 (x1, y1) 为左上角 , (x2,y2) 为右下角的子矩阵的和。(44. 开发商购买土地)

```
    idx = 0
    n = int(data[idx])
    idx += 1
    m = int(data[idx])
    idx += 1
    sum = 0
    vec = []
    for i in range(n):
        row = []
        for j in range(m):
            num = int(data[idx])
            idx += 1
            row.append(num)
            sum += num
        vec.append(row)

    # 统计横向
    horizontal = [0] * n
    for i in range(n):
        for j in range(m):
            horizontal[i] += vec[i][j]

    # 统计纵向
    vertical = [0] * m
    for j in range(m):
        for i in range(n):
            vertical[j] += vec[i][j]

    result = float('inf')
    horizontalCut = 0
    for i in range(n):
        horizontalCut += horizontal[i]
        result = min(result, abs(sum - 2 * horizontalCut))

    verticalCut = 0
    for j in range(m):
        verticalCut += vertical[j]
        result = min(result, abs(sum - 2 * verticalCut))

    print(result)
```
- 感觉也可以用递归求解的样子