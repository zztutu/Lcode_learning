### 24. swap-nodes-in-pairs  
S: template of swap elements   
- tmp = first  
- pre.append(second)  
- second.append(tmp) # first  
- tmp.append(rest)  

### 19. remove-nth-node-from-end
T: double pointers when "within one loop" is required  

Q: How many steps between fast and slow?  
Q: How to define step of 'fast' pointer?  
A: ''nth node from the end'': n!  

### 160. intersection of two linked lists  
B: do not interate list with "head", you can never look back    
C: in python, swap values just with "A, B = B, A"  

Q: How many steps should we move A (A is longer)?  
A: len(A) - len(B) (currentA is already the one step)  


### 142. linked list cycle ii  
Q: How to tell whether's a loop inside the liked list?  
A: dual pointers (fast, slow) encounter!  
Q: How to determine the starting point of the loop?  
A: two pointers (same pace, starting from head and encountered point seperatedly!) encounter again! Then, that is the staring point!  


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





