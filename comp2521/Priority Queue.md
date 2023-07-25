[[Heaps]] behaviour is exactly behaviour required for Priority Queue:
- Insert ensures highest value is at top
- delete takes the highest value

### Example Code
```c
typedef Heap PQueue;

void join(PQueue pq, Item it) { HeapInsert(pq,it); }

Item leave(PQueue pq) { return HeapDelete(pq); }
```

### Implementation comparison 
![](https://lh4.googleusercontent.com/N8FnnYfPpRCmGNhxlAh17BKSPtgfklxbPTIXNxPI2z-ktsrx_FWG46QWeceBx_bPEyNLPar4DO4uYdTV27pVKXz9W31UoPO9n0zVAmaCQErHEm8xHb_iSqtxQ_P6WfLb1ToIS_UoTs_pSsEFMLePEaA)