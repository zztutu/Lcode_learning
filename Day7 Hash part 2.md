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


### 18. 4sum
S: very similar to 3sum, just adding one more **loop layer**!  
This is important as xxsum can follow the similar way!  
Q: what's the **key idea** of these xxsum questions?  
A: Iterate the array, use left (i+1) and right (from n-1 inversely) to find propor combinations!  