# Data Structures & Algorithms (DSA) Cheatsheet

## 1. Time & Space Complexity

| Operation                        | Array  | Linked List | Stack  | Queue  | Binary Tree | Binary Search Tree | Heap   |
|-----------------------------------|--------|-------------|--------|--------|-------------|--------------------|--------|
| Accessing Elements               | O(1)   | O(n)        | O(1)   | O(1)   | O(n)        | O(log n)           | O(1)   |
| Insertion (at beginning)         | O(n)   | O(1)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Insertion (at end)               | O(1)   | O(n)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Deletion (at beginning)          | O(n)   | O(1)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Deletion (at end)                | O(1)   | O(n)        | O(1)   | O(1)   | O(log n)    | O(log n)           | O(log n)|
| Search (unsorted)                | O(n)   | O(n)        | O(n)   | O(n)   | O(n)        | O(log n)           | O(log n)|
| Search (sorted)                  | O(log n)| O(n)       | O(n)   | O(n)   | O(log n)    | O(log n)           | O(log n)|

---

## 2. Data Structures

### Arrays
- An array is a collection of elements identified by index or key. It allows efficient indexing but has a fixed size.
### 1. Searching Algorithms
- **Linear Search** 
```cpp
int linearSearch(const vector<int>& arr, int target) {
    // Iterate through the entire array
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == target) return i; // Return index if target is found
    }
    return -1; // Return -1 if not found
}
```
- **Binary Search** 
```cpp
int binarySearch(const vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid; // Target found
        else if (arr[mid] < target) left = mid + 1; // Search in the right half
        else right = mid - 1; // Search in the left half
    }
    return -1; // Return -1 if not found
}
```

- **Ternary Search** 
```cpp
int ternarySearch(const vector<int>& arr, int left, int right, int target) {
    if (right >= left) {
        int mid1 = left + (right - left) / 3;
        int mid2 = right - (right - left) / 3;
        if (arr[mid1] == target) return mid1; // Target found at mid1
        if (arr[mid2] == target) return mid2; // Target found at mid2
        if (target < arr[mid1]) return ternarySearch(arr, left, mid1 - 1, target); // Search left of mid1
        else if (target > arr[mid2]) return ternarySearch(arr, mid2 + 1, right, target); // Search right of mid2
        else return ternarySearch(arr, mid1 + 1, mid2 - 1, target); // Search between mid1 and mid2
    }
    return -1; // Return -1 if not found
}
```
#### 2. Sorting Algorithms
- **Bubble Sort** 
```cpp
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    // Perform multiple passes through the array
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            // Swap adjacent elements if they are in wrong order
            if (arr[j] > arr[j+1]) {
                swap(arr[j], arr[j+1]);
            }
        }
    }
}
```
- **Selection Sort**
```cpp
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    // Select the minimum element in each pass
    for (int i = 0; i < n-1; i++) {
        int minIndex = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j; // Update minimum index
            }
        }
        // Swap the found minimum element with the first element
        swap(arr[i], arr[minIndex]);
    }
}
```
- **Insertion Sort** 
```cpp
void insertionSort(vector<int>& arr) {
    int n = arr.size();
    // Build the sorted array one element at a time
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        // Move elements of arr[0..i-1] that are greater than key
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key; // Insert the key at the correct position
    }
}
```
- **Merge Sort**
```cpp
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    vector<int> L(n1), R(n2);

    // Copy data into temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int i = 0; i < n2; i++) R[i] = arr[mid + 1 + i];

    int i = 0, j = 0, k = left;
    // Merge the temp arrays back into the original array
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

    // Copy remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);   // Sort the left half
        mergeSort(arr, mid+1, right); // Sort the right half
        merge(arr, left, mid, right); // Merge the sorted halves
    }
}
```
- **Quick Sort** 
```cpp
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Set pivot element to the last element
    int i = low - 1; // Initialize smaller index
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]); // Place pivot at correct position
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high); // Partition index
        quickSort(arr, low, pi - 1);  // Sort left half
        quickSort(arr, pi + 1, high); // Sort right half
    }
}
```
- **Heap Sort**
```cpp
void heapify(vector<int>& arr, int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // Left child
    int right = 2 * i + 2; // Right child

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest]) largest = left;
    // If right child is larger than largest
    if (right < n && arr[right] > arr[largest]) largest = right;

    // If largest is not root, swap and heapify
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(vector<int>& arr) {
    int n = arr.size();
    // Build a max heap
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }

    // One by one extract elements from heap
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]); // Swap root with last element
        heapify(arr, i, 0);    // Heapify the reduced heap
    }
}
```

- **Counting Sort** 
```cpp
void countingSort(vector<int>& arr) {
    int maxVal = *max_element(arr.begin(), arr.end()); // Find the maximum value in the array
    vector<int> count(maxVal + 1, 0), output(arr.size()); // Create count and output arrays

    // Step 1: Count the occurrences of each element
    for (int i = 0; i < arr.size(); i++) 
        count[arr[i]]++;

    // Step 2: Compute cumulative sum in count array (for sorting order)
    for (int i = 1; i <= maxVal; i++) 
        count[i] += count[i-1];

    // Step 3: Place elements in sorted order in the output array
    for (int i = arr.size()-1; i >= 0; i--) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--; // Decrement the count
    }

    // Step 4: Copy sorted elements back to the original array
    for (int i = 0; i < arr.size(); i++) 
        arr[i] = output[i];
}
```
- **Radix Sort** 
```cpp
void countingSortRadix(vector<int>& arr, int exp) {
    vector<int> output(arr.size()); // Output array to store sorted elements
    vector<int> count(10, 0); // Count array to store frequency of digits (0-9)

    // Step 1: Count occurrences of each digit at the current exponent place
    for (int i = 0; i < arr.size(); i++) 
        count[(arr[i] / exp) % 10]++;

    // Step 2: Compute cumulative sum in count array
    for (int i = 1; i < 10; i++) 
        count[i] += count[i - 1];

    // Step 3: Place elements in sorted order based on current digit
    for (int i = arr.size() - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--; // Decrement the count
    }

    // Step 4: Copy sorted elements back to the original array
    for (int i = 0; i < arr.size(); i++) 
        arr[i] = output[i];
}

// Radix Sort: Sorts numbers digit by digit using Counting Sort
void radixSort(vector<int>& arr) {
    int maxVal = *max_element(arr.begin(), arr.end()); // Find the maximum value in the array

    // Apply Counting Sort for each digit (place value increases by powers of 10)
    for (int exp = 1; maxVal / exp > 0; exp *= 10) {
        countingSortRadix(arr, exp);
    }
}
```

### Linked List
- A Linked List is a linear data structure where elements (nodes) are connected using pointers. Each node contains a data part and a pointer to the next node.
-  **Singly Linked List (Node Structure):**
```cpp
// Structure for a Singly Linked List Node
struct Node {
    int data;
    Node* next;
    
    // Constructor to initialize the node with a value
    Node(int val) {
        data = val;
        next = NULL;
    }
};
```
- **Insertion at the head:** O(1)
```cpp
void insertAtHead(Node*& head, int value) {
    Node* newNode = new Node(value); // Create a new node
    newNode->next = head; // Point new node to the old head
    head = newNode; // Update head pointer
}
```
 - **Insertion at the tail:** O(n)
```cpp
void insertAtTail(Node*& head, int value) {
    Node* newNode = new Node(value); // Create a new node
    if (!head) { // If list is empty, make new node the head
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next) temp = temp->next; // Traverse to last node
    temp->next = newNode; // Append new node at the end
}
```
 - **Insertion at a specific position:** O(n)
```cpp
void insertAtPosition(Node*& head, int value, int position) {
    if (position == 1) { // Insert at head if position is 1
        insertAtHead(head, value);
        return;
    }
    Node* temp = head;
    for (int i = 1; i < position - 1; i++) { // Traverse to (position-1)th node
        if (temp == NULL) return; // If position is out of bounds, return
        temp = temp->next;
    }
    Node* newNode = new Node(value);
    newNode->next = temp->next;
    temp->next = newNode; // Link new node in the list
}
```
 - **Deletion from the head:** O(1)
```cpp
void deleteAtHead(Node*& head) {
    if (head == NULL) return; // If list is empty, return
    Node* temp = head;
    head = head->next; // Move head to next node
    delete temp; // Delete the old head node
}
```
 - **Deletion from the tail:** O(n)
```cpp
void deleteAtTail(Node*& head) {
    if (head == NULL) return; // If list is empty, return
    if (head->next == NULL) { // If only one node is present
        delete head;
        head = NULL;
        return;
    }
    Node* temp = head;
    while (temp->next && temp->next->next) { // Traverse to second last node
        temp = temp->next;
    }
    delete temp->next; // Delete last node
    temp->next = NULL; // Set second-last node's next to NULL
}
```
- **Deletion at a specific position:** O(n)
```cpp
void deleteAtPosition(Node*& head, int position) {
    if (position == 1) { // If deleting head, call deleteAtHead
        deleteAtHead(head);
        return;
    }
    Node* temp = head;
    for (int i = 1; i < position - 1; i++) { // Traverse to (position-1)th node
        if (temp == NULL) return; // If position is out of bounds, return
        temp = temp->next;
    }
    if (temp == NULL || temp->next == NULL) return; // If position is invalid, return
    Node* toDelete = temp->next;
    temp->next = temp->next->next; // Link previous node to next node
    delete toDelete; // Delete the node
}
```
- **Display List:** O(n)
```cpp
void displayList(Node* head) {
    Node* temp = head;
    while (temp != NULL) { // Iterate through the list
        cout << temp->data << " ";
        temp = temp->next;
    }
    cout << endl;
}
```
- **Doubly Linked List (Node Structure):**
```cpp
// Structure for a Doubly Linked List Node
struct DNode {
    int data;
    DNode* prev;
    DNode* next;
    
    // Constructor to initialize the node with a value
    DNode(int val) {
        data = val;
        prev = NULL;
        next = NULL;
    }
};
``` 

### Stack
- A Stack is a linear data structure that follows the LIFO (Last In, First Out) principle.
- **Node Structure (Stack):**
```cpp
// Stack class
class Stack {
private:
    int arr[MAX];  // Array to store stack elements
    int top;       // Index of the top element in the stack

public:
    // Constructor to initialize the stack
    Stack() {
        top = -1;  // Stack is initially empty
    }

    // Function to check if the stack is full
    bool isFull() {
        return top == MAX - 1;
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == -1;
    }

    // Function to push an element onto the stack
    void push(int value) {
        if (isFull()) {
            cout << "Stack Overflow!" << endl;
            return;
        }
        arr[++top] = value;  // Increment top and insert value
        cout << value << " pushed to stack" << endl;
    }

    // Function to pop an element from the stack
    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow!" << endl;
            return -1;
        }
        return arr[top--];  // Return top value and decrement top
    }

    // Function to return the top element of the stack
    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty!" << endl;
            return -1;
        }
        return arr[top];  // Return the top element
    }

    // Function to display the stack elements
    void display() {
        if (isEmpty()) {
            cout << "Stack is empty!" << endl;
            return;
        }
        cout << "Stack: ";
        for (int i = top; i >= 0; i--) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
};
```

### Queue
- A Queue is a linear data structure that follows the FIFO (First In, First Out) principle.
- **Node Structure (Queue):**
```cpp
#define MAX 100 // Maximum size of the queue

// Queue class
class Queue {
private:
    int arr[MAX];  // Array to store queue elements
    int front;     // Index of the front element in the queue
    int rear;      // Index of the rear element in the queue

public:
    // Constructor to initialize the queue
    Queue() {
        front = -1;  // Queue is initially empty
        rear = -1;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == -1; // If front is -1, the queue is empty
    }

    // Function to check if the queue is full
    bool isFull() {
        return rear == MAX - 1; // If rear is at the maximum index, the queue is full
    }

    // Function to enqueue (insert) an element into the queue
    void enqueue(int value) {
        if (isFull()) {
            cout << "Queue Overflow!" << endl;
            return;
        }
        if (front == -1) front = 0; // If queue is empty, set front to 0
        arr[++rear] = value; // Insert value at rear and increment rear
        cout << value << " enqueued to queue" << endl;
    }

    // Function to dequeue (remove) an element from the queue
    int dequeue() {
        if (isEmpty()) {
            cout << "Queue Underflow!" << endl;
            return -1;
        }
        int value = arr[front]; // Get the value at the front
        if (front == rear) {    // If there is only one element
            front = rear = -1;  // Reset the queue
        } else {
            front++;            // Increment front to remove the element
        }
        return value; // Return the dequeued value
    }

    // Function to return the front element of the queue
    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty!" << endl;
            return -1;
        }
        return arr[front]; // Return the element at the front
    }

    // Function to display the queue elements
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty!" << endl;
            return;
        }
        cout << "Queue: ";
        for (int i = front; i <= rear; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
};

```


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

- **Insert Element in Heap**: \( O(log n) \)
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

- **Extract Min/Max from Heap**: \( O(log n) \)
```cpp
int extractMin(vector<int>& heap) {
    // If the heap is empty, return -1 as there is no element to extract
    if (heap.size() == 0) return -1; // Heap is empty
    
    // Swap the root (min element) with the last element in the heap
    // This is done to remove the root and prepare the heap for heapify operation
    swap(heap[0], heap[heap.size() - 1]);
    
    // Store the min value (which is now at the last element before removing it)
    int minValue = heap.back();
    
    // Remove the last element (which was the original root)
    heap.pop_back();
    
    // Heapify down (bubble down) the new root element to restore heap property
    int index = 0;  // Start at the root of the heap
    while (index < heap.size()) {
        int leftChildIndex = 2 * index + 1;   // Left child index
        int rightChildIndex = 2 * index + 2;  // Right child index
        int smallest = index; // Assume the smallest element is the current index
        
        // If the left child exists and is smaller than the current smallest, update smallest
        if (leftChildIndex < heap.size() && heap[leftChildIndex] < heap[smallest]) {
            smallest = leftChildIndex;
        }
        
        // If the right child exists and is smaller than the current smallest, update smallest
        if (rightChildIndex < heap.size() && heap[rightChildIndex] < heap[smallest]) {
            smallest = rightChildIndex;
        }
        
        // If the smallest element is the current index, the heap property is restored
        // Break out of the loop as no further bubbling down is needed
        if (smallest == index) break;
        
        // Swap the current element with the smallest child to move the smaller element up
        swap(heap[index], heap[smallest]);
        
        // Move to the index of the child that was swapped
        index = smallest;
    }
    
    // Return the original root (min value) that was extracted
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
    // Calculate the indices of the left and right children of the current node
    int leftChild = 2 * index + 1;
    int rightChild = 2 * index + 2;
    
    // Assume the smallest element is at the current index
    int smallest = index;

    // If the left child exists and is smaller than the current smallest element, update smallest
    if (leftChild < n && heap[leftChild] < heap[smallest]) {
        smallest = leftChild;
    }

    // If the right child exists and is smaller than the current smallest element, update smallest
    if (rightChild < n && heap[rightChild] < heap[smallest]) {
        smallest = rightChild;
    }

    // If the smallest element is not at the current index, swap the elements and continue heapifying
    if (smallest != index) {
        swap(heap[index], heap[smallest]);  // Swap the elements to maintain heap property
        heapify(heap, n, smallest);         // Recursively heapify the affected subtree
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

- **Heap Sort**: \( O(n log n) \)
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

### Binary Search Tree (BST)
- A Binary Search Tree (BST) is a binary tree with the property that for each node:
    - All nodes in the left subtree have values less than the node.
    - All nodes in the right subtree have values greater than the node.
- **Node Structure (Binary Search Tree):**
```cpp
// Definition for a Binary Tree Node
struct Node {
    int data;   // Stores the value of the node
    Node* left;  // Pointer to the left child
    Node* right; // Pointer to the right child

    // Constructor to initialize a new node
    Node(int val) : data(val), left(NULL), right(NULL) {}
};
```

#### Basic Tree Operations
- **Insert Node (BST):** O(logn)
```cpp
// Function to insert a value into a Binary Search Tree (BST)
TreeNode* insert(TreeNode* root, int value) {
    // Base case: If the tree is empty, create a new node and return it
    if (root == NULL) {
        return new TreeNode(value);
    }

    // If the value to insert is smaller, recurse on the left subtree
    if (value < root->data) {
        root->left = insert(root->left, value);
    } 
    // If the value to insert is greater, recurse on the right subtree
    else {
        root->right = insert(root->right, value);
    }

    // Return the unchanged root pointer
    return root;
}
```
- **In-order Traversal:** O(n)
```cpp
// Function to perform inorder traversal of a Binary Tree
void inorder(TreeNode* root) {
    // Base case: If the tree is empty, return
    if (root == NULL) 
        return;

    // Recursively visit the left subtree
    inorder(root->left);

    // Process the current node (print its data)
    cout << root->data << " ";

    // Recursively visit the right subtree
    inorder(root->right);
}
```
- **Pre-order Traversal:** O(n)
```cpp
// Function to perform preorder traversal of a Binary Tree
void preorder(TreeNode* root) {
    // Base case: If the tree is empty, return
    if (root == NULL) 
        return;

    // Process the current node (print its data)
    cout << root->data << " ";

    // Recursively visit the left subtree
    preorder(root->left);

    // Recursively visit the right subtree
    preorder(root->right);
}
```
- **Post-order Traversal:** O(n)
```cpp
// Function to perform postorder traversal of a Binary Tree
void postorder(TreeNode* root) {
    // Base case: If the tree is empty, return
    if (root == NULL) 
        return;

    // First, recursively visit the left subtree
    postorder(root->left);

    // Then, recursively visit the right subtree
    postorder(root->right);

    // Finally, process the current node (print its data)
    cout << root->data << " ";
}
```
- **Height of Tree:** O(n)
```cpp
// Function to calculate the height of a Binary Tree
int height(TreeNode* root) {
    // Base case: If the tree is empty, height is 0
    if (root == NULL) 
        return 0;

    // Recursively compute the height of the left and right subtrees
    // The height of the tree is the maximum height of the left or right subtree plus 1 (for the root)
    return max(height(root->left), height(root->right)) + 1;
}
```
- **Search in BST**: O(logn)
```cpp
// Function to search for a key in a Binary Search Tree (BST)
TreeNode* search(TreeNode* root, int key) {
    // Base case: If the tree is empty or the key is found at the root
    if (root == NULL || root->data == key) 
        return root;

    // If the key is smaller than the root's key, search in the left subtree
    if (key < root->data) 
        return search(root->left, key);

    // If the key is greater than the root's key, search in the right subtree
    return search(root->right, key);
}
```
- **Delete Node in BST:** O(logn)
```cpp
// Function to delete a node from a Binary Search Tree (BST)
TreeNode* deleteNode(TreeNode* root, int key) {
    // Base case: If the tree is empty or key is not found
    if (root == NULL) return root;

    // If the key is smaller than the root's key, it lies in the left subtree
    if (key < root->data) {
        root->left = deleteNode(root->left, key);
    }
    // If the key is greater than the root's key, it lies in the right subtree
    else if (key > root->data) {
        root->right = deleteNode(root->right, key);
    }
    // If the key is the same as root's key, then this is the node to be deleted
    else {
        // Case 1: Node has no left child
        if (root->left == NULL) {
            TreeNode* temp = root->right; // Store the right child
            delete root; // Delete the current node
            return temp; // Return the right child to maintain BST structure
        }
        // Case 2: Node has no right child
        else if (root->right == NULL) {
            TreeNode* temp = root->left; // Store the left child
            delete root; // Delete the current node
            return temp; // Return the left child to maintain BST structure
        }

        // Case 3: Node has two children
        // Find the inorder successor (smallest node in the right subtree)
        TreeNode* temp = minValueNode(root->right);
        
        // Copy the inorder successor's value to this node
        root->data = temp->data;
        
        // Delete the inorder successor from the right subtree
        root->right = deleteNode(root->right, temp->data);
    }

    return root; // Return the modified root node
}

// Function to find the node with the smallest value in a BST
TreeNode* minValueNode(TreeNode* node) {
    TreeNode* current = node;

    // The leftmost leaf will have the smallest value
    while (current && current->left != NULL) {
        current = current->left;
    }

    return current; // Return the node with the smallest value
}
```

---

