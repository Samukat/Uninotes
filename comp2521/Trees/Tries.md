# Tries
A Trie are a data structure for representing strings that support O(L) lookup and insertion (L is length of string).

- Every node in a trie
    - Contains one part of a key (usually a character)
    - May have up to 26 children
    - May be flagged as a ‘finishing’ node
- Time complexity of searching: O(d), where d is the depth

A type of [[Tree]], similar to a [[B-Tree]]/[[2-3-4-tree]].
<p align="center">
<img width= 500 src=https://lh5.googleusercontent.com/vqJIRFqHUFr6WWex3yCFYgzHsj149jRj0LDAhniI2xo224ocqOtL-QwgZeRNuDA6K64dc2Vt9ccfVovMt4kCk_o32_7iWbZtTan9BALReEpKb9tCA7G1fo2OYQGPBSp0EP12VQkhxGEIdtgjfMW7IaM> </p>
End of word is marked (In image case in red)


## Implementation
```c
#define ALPHABET_SIZE 26

typedef struct Node *Trie;

typedef struct Node {
	char onechar;
	Trie child[ALPHABET_SIZE];
	bool finish;
	Item data;
} Node;

typedef char *Key;
```
>This implementation is quite memory heavy, ~214 bytes per node



## Compressed Tries
**Compressed Tries**
- Obtained from standard tries by compressing ‘redundant’ chains of nodes
<p align="center">
<img width=400 src=https://lukakerr.github.io/assets/img/2521/text4.png> </p>
