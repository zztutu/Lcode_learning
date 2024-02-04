### 239. sliding-window-maximum
Q: why we need compare first element in pop(value), just delete it?  
A: the elements in queue is not in same order with nums (we re-order them for finding the max!), so you cannot just pop() directly. 

### 347. top-k-frequent-elements
B: result[i] = heapq.heapqpop(pri_que)[1]. Why [1]: This is common in priority queues where each entry is a tuple in the form (priority, value), and by using [1], you retrieve the value.  
