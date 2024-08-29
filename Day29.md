### 134. 加油站 
- 如果总油量减去总消耗大于等于零那么一定可以跑完一圈，说明 各个站点的加油站 剩油量rest[i]相加一定是大于等于零的。
- i从0开始累加rest[i]，和记为curSum，一旦curSum小于零，说明[0, i]区间都不能作为起始位置，因为这个区间选择任何一个位置作为起点，到i这里都会断油，那么起始位置从i+1算起，再从0计算curSum。
- 能不能
- 找到起点，问题变为第一个positive的位置，变简单

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        curSum = 0  # 当前累计的剩余油量
        totalSum = 0  # 总剩余油量
        start = 0  # 起始位置

        for i in range(len(gas)):
            curSum += gas[i] - cost[i]
            totalSum += gas[i] - cost[i]

            if curSum < 0:  # 当前累计剩余油量curSum小于0
                start = i + 1  # 起始位置更新为i+1
                curSum = 0  # curSum重新从0开始累计

        if totalSum < 0:
            return -1  # 总剩余油量totalSum小于0，说明无法环绕一圈
        return start
```

### 135. 分发糖果 
- 需要准备的 最少糖果数目
- 有条件的赋值问题，同时min cost，听上去像kkt
> 处理好一边再处理另一边，不要两边想着一起兼顾：只要右边评分比左边大，右边的孩子就多一个糖果
- 我感觉可以sort先，左右只是求sum

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        candyVec = [1] * len(ratings)

        # 从前向后遍历，处理右侧比左侧评分高的情况
        for i in range(1, len(ratings)):
            if ratings[i] > ratings[i - 1]:
                candyVec[i] = candyVec[i - 1] + 1

        # 从后向前遍历，处理左侧比右侧评分高的情况
        for i in range(len(ratings) - 2, -1, -1):
            if ratings[i] > ratings[i + 1]:
                candyVec[i] = max(candyVec[i], candyVec[i + 1] + 1)

        # 统计结果
        result = sum(candyVec)
        return result
```

### 860.柠檬水找零 
- 维护element数量
  
```python
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        five = 0
        ten = 0
        twenty = 0

        for bill in bills:
            # 情况一：收到5美元
            if bill == 5:
                five += 1

            # 情况二：收到10美元
            if bill == 10:
                if five <= 0:
                    return False
                ten += 1
                five -= 1

            # 情况三：收到20美元
            if bill == 20:
                # 先尝试使用10美元和5美元找零
                if five > 0 and ten > 0:
                    five -= 1
                    ten -= 1
                    #twenty += 1
                # 如果无法使用10美元找零，则尝试使用三张5美元找零
                elif five >= 3:
                    five -= 3
                    #twenty += 1
                else:
                    return False

        return True
```


### 406.根据身高重建队列 
> 遇到两个维度权衡的时候，一定要先确定一个维度，再确定另一个维度。如果两个维度一起考虑一定会顾此失彼。
- 感觉和之前那个蛮想，类似kkt，有条件的xxx

```python
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
    	# 先按照h维度的身高顺序从高到低排序。确定第一个维度
        # lambda返回的是一个元组：当-x[0](维度h）相同时，再根据x[1]（维度k）从小到大排序
        people.sort(key=lambda x: (-x[0], x[1]))
        que = []
	
	# 根据每个元素的第二个维度k，贪心算法，进行插入
        # people已经排序过了：同一高度时k值小的排前面。
        for p in people:
            que.insert(p[1], p)
        return que
```

