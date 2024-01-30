
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

### 28. find index of first occurence in a string
S: one trick to find same substring: if the lasted element is not the same, then, try to row back to the last same one according to the False Table! This is important as even the false table uses the same idea!

Q: Key idea of KMP  
A: just comparing from point, that we already compared for last n-1 elements!
S: that's why, we want to find the longest same prefix-suffix substring!