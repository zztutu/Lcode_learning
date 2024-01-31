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