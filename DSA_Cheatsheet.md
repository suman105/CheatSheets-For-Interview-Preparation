
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
```

- **Basic Operations (Insertion and Deletion):**
```cpp
// Insert at the beginning
void insertAtBeginning(Node*& head, int value) {
    Node* newNode = new Node;
    newNode->data = value;
    newNode->next = head;
    head = newNode;
}

// Delete at the beginning
void deleteAtBeginning(Node*& head) {
    if (head != nullptr) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }
}
```

### Stack

- **Node Structure (Stack):**
```cpp
struct Node {
    int data;
    Node* next;
};
```

- **Operations:**
```cpp
// Push to stack
void push(Node*& top, int value) {
    Node* newNode = new Node;
    newNode->data = value;
    newNode->next = top;
    top = newNode;
}

// Pop from stack
int pop(Node*& top) {
    if (top == nullptr) return -1; // Stack is empty
    Node* temp = top;
    int value = top->data;
    top = top->next;
    delete temp;
    return value;
}
```

### Queue

- **Node Structure (Queue):**
```cpp
struct Node {
    int data;
    Node* next;
};
```

- **Operations:**
```cpp
// Enqueue (Insert)
void enqueue(Node*& front, Node*& rear, int value) {
    Node* newNode = new Node;
    newNode->data = value;
    newNode->next = nullptr;
    if (rear != nullptr) rear->next = newNode;
    rear = newNode;
    if (front == nullptr) front = newNode;
}

// Dequeue (Remove)
int dequeue(Node*& front) {
    if (front == nullptr) return -1; // Queue is empty
    Node* temp = front;
    int value = front->data;
    front = front->next;
    delete temp;
    return value;
}
```

### Binary Tree

- **Node Structure (Binary Tree):**
```cpp
struct Node {
    int data;
    Node* left;
    Node* right;
};
```

### Binary Search Tree (BST)

- **Node Structure (Binary Search Tree):**
```cpp
struct Node {
    int data;
    Node* left;
    Node* right;
};
```

---

### Heap (Binary Heap)

- A **Heap** is a complete binary tree, where each node satisfies the heap property:
  - **Min Heap**: The value of the parent node is less than or equal to the values of its children.
  - **Max Heap**: The value of the parent node is greater than or equal to the values of its children.

#### **Heap Node Structure**
```cpp
struct HeapNode {
    int data;
};
```

#### **Basic Heap Operations**

- **Insert Element in Heap**: \( O(\log n) \)
```cpp
void insertHeap(vector<int>& heap, int value) {
    heap.push_back(value); // Add to the end of the heap
    int index = heap.size() - 1;
    
    // Heapify up (bubble up)
    while (index > 0) {
        int parentIndex = (index - 1) / 2;
        if (heap[index] < heap[parentIndex]) { // Min Heap property
            swap(heap[index], heap[parentIndex]);
            index = parentIndex;
        } else {
            break;
        }
    }
}
```

- **Extract Min/Max from Heap**: \( O(\log n) \)
```cpp
int extractMin(vector<int>& heap) {
    if (heap.size() == 0) return -1; // Heap is empty
    
    // Swap the root with the last element and remove the last element
    swap(heap[0], heap[heap.size() - 1]);
    int minValue = heap.back();
    heap.pop_back();
    
    // Heapify down (bubble down)
    int index = 0;
    while (index < heap.size()) {
        int leftChildIndex = 2 * index + 1;
        int rightChildIndex = 2 * index + 2;
        int smallest = index;
        
        if (leftChildIndex < heap.size() && heap[leftChildIndex] < heap[smallest]) {
            smallest = leftChildIndex;
        }
        
        if (rightChildIndex < heap.size() && heap[rightChildIndex] < heap[smallest]) {
            smallest = rightChildIndex;
        }
        
        if (smallest == index) break;
        
        swap(heap[index], heap[smallest]);
        index = smallest;
    }
    
    return minValue;
}
```

- **Peek Min/Max (View top element without removal)**: \( O(1) \)
```cpp
int peekMin(const vector<int>& heap) {
    if (heap.size() == 0) return -1; // Heap is empty
    return heap[0]; // Min element is always at the root
}
```

- **Heapify an Array**: \( O(n) \)
```cpp
void heapify(vector<int>& heap, int n, int index) {
    int leftChild = 2 * index + 1;
    int rightChild = 2 * index + 2;
    int smallest = index;

    if (leftChild < n && heap[leftChild] < heap[smallest]) {
        smallest = leftChild;
    }
    if (rightChild < n && heap[rightChild] < heap[smallest]) {
        smallest = rightChild;
    }
    if (smallest != index) {
        swap(heap[index], heap[smallest]);
        heapify(heap, n, smallest);
    }
}
```

- **Build Min Heap**: \( O(n) \)
```cpp
void buildMinHeap(vector<int>& heap) {
    int n = heap.size();
    // Start from the last non-leaf node and heapify each node
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(heap, n, i);
    }
}
```

- **Heap Sort**: \( O(n \log n) \)
```cpp
void heapSort(vector<int>& arr) {
    buildMinHeap(arr);
    int n = arr.size();
    
    for (int i = n - 1; i >= 0; i--) {
        swap(arr[0], arr[i]); // Move the current root (min) to the end
        heapify(arr, i, 0);    // Heapify the reduced heap
    }
}
```

### Priority Queue (using Heap)
- A **priority queue** is an abstract data structure that supports efficiently retrieving the element with the highest or lowest priority. It can be implemented using a **heap**.

```cpp
priority_queue<int, vector<int>, greater<int>> pq; // Min-heap implementation

// Insertion in priority queue
pq.push(10);
pq.push(5);
pq.push(20);

// Extract the top element
int minValue = pq.top();
pq.pop();
```

---

## 3. Sorting Algorithms
(Refer to previous responses for sorting algorithms)

## 4. Searching Algorithms
(Refer to previous responses for searching algorithms)
