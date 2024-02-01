### 28. find index of first occurence in a string
S: one trick to find same substring: if the lasted element is not the same, then, try to row back to the last same one according to the False Table! This is important as even the false table uses the same idea!

Q: Key idea of KMP  
A: just comparing from point, that we already compared for last n-1 elements!
S: that's why, we want to find the longest same prefix-suffix substring!


### 459. repeated substring pattern
B: In line "if next[-1] != -1 and len(s) % (len(s) - (next[-1] + 1)) == 0", we have (next[-1]+1)! not (len-val+1)!   
Q: Further understand False table (Next) arracy calculation:  
A: with i increases (for i in range(1, len(s))), we want to find longest prefix-suffix subsubstring within substring ending with s[i]! But, **j also increases**! Take the example of "AABAACXXXX".  
Q: How to tell the value of j?  
A: in "AABBAACXXX", next["c"-1] = 1, which is j value when loop at "C"  