
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
- #### 1. Searching Algorithms

**1. Linear Search** 
```cpp
int linearSearch(const vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == target) return i;
    }
    return -1;
}
```
**2. Binary Search** 
```cpp
int binarySearch(const vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

**3. Ternary Search** 
```cpp
int ternarySearch(const vector<int>& arr, int left, int right, int target) {
    if (right >= left) {
        int mid1 = left + (right - left) / 3;
        int mid2 = right - (right - left) / 3;
        if (arr[mid1] == target) return mid1;
        if (arr[mid2] == target) return mid2;
        if (target < arr[mid1]) return ternarySearch(arr, left, mid1 - 1, target);
        else if (target > arr[mid2]) return ternarySearch(arr, mid2 + 1, right, target);
        else return ternarySearch(arr, mid1 + 1, mid2 - 1, target);
    }
    return -1;
}

```
- #### 2. Sorting Algorithms
**1. Bubble Sort** 
```cpp
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                swap(arr[j], arr[j+1]);
            }
        }
    }
}
```
**2. Selection Sort**
```cpp
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n-1; i++) {
        int minIndex = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}
```
**3. Insertion Sort** 
```cpp
void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}
```
**4. Merge Sort**
```cpp
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    vector<int> L(n1), R(n2);
    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int i = 0; i < n2; i++) R[i] = arr[mid + 1 + i];
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    while (i < n1) { arr[k] = L[i]; i++; k++; }
    while (j < n2) { arr[k] = R[j]; j++; k++; }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid+1, right);
        merge(arr, left, mid, right);
    }
}
```
**5. Quick Sort** 
```cpp
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i+1], arr[high]);
    return i+1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```
**6. Heap Sort**
```cpp
void heapify(vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;
    if (left < n && arr[left] > arr[largest]) largest = left;
    if (right < n && arr[right] > arr[largest]) largest = right;
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = n/2 - 1; i >= 0; i--) heapify(arr, n, i);
    for (int i = n-1; i >= 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}
```

**7. Counting Sort** 
```cpp
void countingSort(vector<int>& arr) {
    int maxVal = *max_element(arr.begin(), arr.end());
    vector<int> count(maxVal + 1, 0), output(arr.size());
    for (int i = 0; i < arr.size(); i++) count[arr[i]]++;
    for (int i = 1; i <= maxVal; i++) count[i] += count[i-1];
    for (int i = arr.size()-1; i >= 0; i--) {
        output[count[arr[i]]-1] = arr[i];
        count[arr[i]]--;
    }
    for (int i = 0; i < arr.size(); i++) arr[i] = output[i];
}
```
**8. Radix Sort** 
```cpp
void countingSortRadix(vector<int>& arr, int exp) {
    vector<int> output(arr.size());
    vector<int> count(10, 0);
    for (int i = 0; i < arr.size(); i++) count[(arr[i]/exp) % 10]++;
    for (int i = 1; i < 10; i++) count[i] += count[i-1];
    for (int i = arr.size()-1; i >= 0; i--) {
        output[count[(arr[i]/exp) % 10] - 1] = arr[i];
        count[(arr[i]/exp) % 10]--;
    }
    for (int i = 0; i < arr.size(); i++) arr[i] = output[i];
}

void radixSort(vector<int>& arr) {
    int maxVal = *max_element(arr.begin(), arr.end());
    for (int exp = 1; maxVal / exp > 0; exp *= 10) {
        countingSortRadix(arr, exp);
    }
}
```

### Linked List

- **Node Structure (Singly Linked List):**
```cpp
struct Node {
    int data;
    Node* next;
    Node(int val) {
        data = val;
        next = NULL;
    }
};

```
  - **Insertion at the head:**O(1)
    ```cpp
    void insertAtHead(Node*& head, int value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
    }
    ```
     - **Insertion at the tail:**O(n)
    ```cpp
    void insertAtTail(Node*& head, int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next) temp = temp->next;
        temp->next = newNode;
    }
    ```
     - **Insertion at a specific position:**O(n)
    ```cpp
    void insertAtPosition(Node*& head, int value, int position) {
        if (position == 1) {
            insertAtHead(head, value);
            return;
        }
        Node* temp = head;
        for (int i = 1; i < position - 1; i++) {
            if (temp == NULL) return; // Position out of bounds
            temp = temp->next;
        }
        Node* newNode = new Node(value);
        newNode->next = temp->next;
        temp->next = newNode;
    }
    ```
     - **Deletion from the head:**O(1)
    ```cpp
    void deleteAtHead(Node*& head) {
        if (head == NULL) return;
        Node* temp = head;
        head = head->next;
        delete temp;
    }
    ```
     - **Deletion from the tail:**O(n)
    ```cpp
    void deleteAtTail(Node*& head) {
        if (head == NULL) return;
        if (head->next == NULL) {
            delete head;
            head = NULL;
            return;
        }
        Node* temp = head;
        while (temp->next && temp->next->next) {
            temp = temp->next;
        }
        delete temp->next;
        temp->next = NULL;
    }
    ```
    - **Deletion at a specific position:**O(n)
    ```cpp
    void deleteAtPosition(Node*& head, int position) {
        if (position == 1) {
            deleteAtHead(head);
            return;
        }
        Node* temp = head;
        for (int i = 1; i < position - 1; i++) {
            if (temp == NULL) return; // Position out of bounds
            temp = temp->next;
        }
        if (temp == NULL || temp->next == NULL) return;
        Node* toDelete = temp->next;
        temp->next = temp->next->next;
        delete toDelete;
    }
    ```
    - **Display List:**O(n)
    ```cpp
    void displayList(Node* head) {
        Node* temp = head;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
    ```
- **Node Structure (Doubly Linked List):**
```cpp
    struct DNode {
        int data;
        DNode* prev;
        DNode* next;
        DNode(int val) {
            data = val;
            prev = NULL;
            next = NULL;
        }
    };
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
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
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
