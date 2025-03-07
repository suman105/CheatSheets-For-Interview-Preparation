# Let's generate a .md file with all the content for the user.

cheatsheet_content = """
# Data Structures & Algorithms (DSA) Cheatsheet

## 1. Time & Space Complexity

| Operation                        | Array  | Linked List | Stack  | Queue  | Binary Tree | Binary Search Tree | Heap   |
|-----------------------------------|--------|-------------|--------|--------|-------------|--------------------|--------|
| Accessing Elements               | O(1)   | O(n)        | O(1)   | O(1)   | O(n)        | O(log n)           | O(1)   |
| Insertion (at beginning)         | O(n)   | O(1)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Insertion (at end)               | O(1)   | O(1)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Deletion (at beginning)          | O(n)   | O(1)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Deletion (at end)                | O(1)   | O(n)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Search (unsorted)                | O(n)   | O(n)        | O(n)   | O(n)   | O(n)        | O(log n)           | O(log n)|
| Search (sorted)                  | O(log n)| O(n)       | O(n)   | O(n)   | O(log n)    | O(log n)           | O(log n)|

---

## 2. Data Structures

### Arrays

- **Operations:**
  - Access: \( O(1) \)
  - Insertion (at beginning): \( O(n) \)
  - Insertion (at end): \( O(1) \)
  - Deletion (at beginning): \( O(n) \)
  - Deletion (at end): \( O(1) \)
  - Search (unsorted): \( O(n) \)
  - Search (sorted): \( O(\log n) \)

### Linked List

- **Node Structure (Singly Linked List):**
```cpp
struct Node {
    int data;
    Node* next;
};
