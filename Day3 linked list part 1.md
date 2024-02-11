### 203 Remove linked list elements
S: Linked list using dummay head  
Q: How to iterate linked list?  
A: current = current.next  

### 707 Design linked list
**pay attention to the contditions!**  
- index starts from **0**  
- while "get", "insert before Index", "delete at Index"  all require loop, the Node ''Cur'' refered to, is different! That's why we have different cur initial values.
  - For Get, cur denotes the Node; 
  - For the other two, we refer to the node **before** the interested Node  

### 206 reverse linked list
S: reverse something inplace -- double pointers  
S: swaping element template  
  - store following
  - cur.next = pre
  - pre = cur
  - cur = following
