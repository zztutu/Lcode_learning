### 977 Squares of a sorted array  
T: The double pointer method could also move the pointers from the seperate directions (start, end) of the array, interesting.  
C: How to initialize arrays?  
A: new_list = [float('inf')]*len(nums)

### 209 minimum size subarray sum
T: typical sliding window questions.  
Q: what's the core of sliding window?  
A: story of "丢玉米": define "removing" conditions

### 59 spiral matrix II
Q: How to define length of rows/columns?  
A: n *n = n^2  
S: be extremly careful with the "offset"  
A: image in your head, max(offset) = n//2