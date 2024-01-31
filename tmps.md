### 28. find index of first occurence in a string
S: one trick to find same substring: if the lasted element is not the same, then, try to row back to the last same one according to the False Table! This is important as even the false table uses the same idea!

Q: Key idea of KMP  
A: just comparing from point, that we already compared for last n-1 elements!
S: that's why, we want to find the longest same prefix-suffix substring!