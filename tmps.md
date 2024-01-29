
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


### 344. reverse string
Q: why not while left <= right?  
A: when left == right, why bother exchange the same letter?  
T: swap element in python: A, B = B, A


### 541. reverse string ii
Q: difference with last one?  
A: reverse within some range:0-k,2k    
T: put range into the loop: (0, len(s), 2*k)

### replace number in string
Q: How to tell numbers from strings?  
A: ord("0") <= ord(ss) <= ord("9") 
S: Key: transform string to list! Replace the number then!  

### 151. reverse words in a string
S: reverse string with all letters and then, reverse letters within words!







