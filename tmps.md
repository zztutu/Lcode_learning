### 242. Valid anagram
S: string, number counter number same or not: counter()  
T: python counter: from collections import Counter  
B:  Counter is a dictionary!

### 349. intersection of two arrays
T: list(set(nums1) & (nums2))

### 202. Happy number
S: conditions to break the loop: same number appears again!  
Q: why O(logn)?  
A: TBD  
T: calculate the sum: sum(int(i)**2 for i in str(n))!  

### 1. two sum
Q: why using hash?  
A: flag: find **if** target in the array; return **index**  
Q: Why not using set() in python?  
A: We have to store value and index, typical dict() data structure!  

### 454. 4sum-ii
S: key of xxsum questions: find if target -val1 in array!  
T: for hashmap in python:  
- hashmap[value] = index
- if target - val in hashmap:  return hashmap[target-value] # index!

### 15. 3sum
Q: logic of the answer?  
A: sort the array, starting from index0, find the other two number with pointers from index1 and index-1  
Q: how to removing repeatings?  
A: if nums[i] == nums[i-1]: continue 



