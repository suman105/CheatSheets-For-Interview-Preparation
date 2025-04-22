# Data Structures & Algorithms (DSA) Cheatsheet

## 1. Time & Space Complexity

| Operation                        | Array  | Linked List (No Tail Pointer) | Linked List (With Tail Pointer) | Stack  | Queue  | Binary Tree (Unbalanced) | Binary Tree (Balanced) | Binary Search Tree | Heap   |
|-----------------------------------|--------|-----------------------------|-----------------------------|--------|--------|---------------------|--------------------|--------------------|--------|
| **Accessing Elements**           | O(1)   | O(n)                        | O(n)                        | O(1)   | O(1)   | O(n)                | O(log n)           | O(log n)           | O(1)   |
| **Insertion (at beginning)**     | O(n)   | O(1)                        | O(1)                        | O(1)   | O(1)   | O(1)                | O(log n)           | O(log n)           | O(log n) |
| **Insertion (at end)**           | O(1) (amortized for dynamic arrays) | O(n)  | O(1)                        | O(1)   | O(1)   | O(1)                | O(log n)           | O(log n)           | O(log n) |
| **Deletion (at beginning)**      | O(n)   | O(1)                        | O(1)                        | O(1)   | O(1)   | O(1)                | O(log n)           | O(log n)           | O(log n) |
| **Deletion (at end)**            | O(1)   | O(n)                        | O(1)                        | O(1)   | O(1)   | O(1)                | O(log n)           | O(log n)           | O(log n) |
| **Search (unsorted)**            | O(n)   | O(n)                        | O(n)                        | O(n)   | O(n)   | O(n)                | O(n)               | O(log n)           | O(log n) |
| **Search (sorted)**              | O(log n) | O(n)                     | O(log n) (if doubly linked list) | O(n)   | O(n)   | O(log n)            | O(log n)           | O(log n)           | O(log n) |
---

## 2. Data Structures

### Arrays
- An array is a collection of elements identified by index or key. It allows efficient indexing but has a fixed size.
### 1. Searching Algorithms
- **Linear Search** 
```js
// Linear Search: Iterates through the array to find the target
function linearSearch(arr, target) {
    // Loop through each element in the array
    for (let i = 0; i < arr.length; i++) {
        // If the current element is the target, return its index
        if (arr[i] === target) return i;
    }
    // If target is not found, return -1
    return -1;
}
```
- **Binary Search** 
```js
// Binary Search: Searches a sorted array by repeatedly dividing the search interval in half
function binarySearch(arr, target) {
    // Initialize pointers for the left and right ends of the array
    let left = 0, right = arr.length - 1;
    // Continue searching while the left pointer is less than or equal to the right
    while (left <= right) {
        // Calculate the middle index, avoiding overflow
        let mid = Math.floor(left + (right - left) / 2);
        // If the middle element is the target, return its index
        if (arr[mid] === target) return mid;
        // If target is greater, ignore the left half
        else if (arr[mid] < target) left = mid + 1;
        // If target is smaller, ignore the right half
        else right = mid - 1;
    }
    // If target is not found, return -1
    return -1;
}
```

- **Ternary Search** 
```js
// Ternary Search: Divides the sorted array into three parts and searches recursively
function ternarySearch(arr, left, right, target) {
    // Base case: If the search interval is valid
    if (right >= left) {
        // Calculate the two mid points dividing the array into three parts
        let mid1 = left + Math.floor((right - left) / 3);
        let mid2 = right - Math.floor((right - left) / 3);
        // If target is found at mid1, return its index
        if (arr[mid1] === target) return mid1;
        // If target is found at mid2, return its index
        if (arr[mid2] === target) return mid2;
        // If target is less than mid1, search the left third
        if (target < arr[mid1]) return ternarySearch(arr, left, mid1 - 1, target);
        // If target is greater than mid2, search the right third
        else if (target > arr[mid2]) return ternarySearch(arr, mid2 + 1, right, target);
        // Otherwise, search the middle third
        else return ternarySearch(arr, mid1 + 1, mid2 - 1, target);
    }
    // If target is not found, return -1
    return -1;
}
```
#### 2. Sorting Algorithms
- **Bubble Sort** 
```js
// Bubble Sort: Repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order
function bubbleSort(arr) {
    let n = arr.length;
    // Outer loop for multiple passes through the array
    for (let i = 0; i < n - 1; i++) {
        // Inner loop to compare adjacent elements
        for (let j = 0; j < n - i - 1; j++) {
            // Swap if the current element is greater than the next
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
        }
    }
}
```
- **Selection Sort**
```js
// Selection Sort: Repeatedly selects the minimum element from the unsorted portion and places it at the beginning
function selectionSort(arr) {
    let n = arr.length;
    // Loop through each element
    for (let i = 0; i < n - 1; i++) {
        // Assume the current index has the minimum value
        let minIndex = i;
        // Find the minimum element in the unsorted portion
        for (let j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        // Swap the found minimum element with the first element of the unsorted portion
        [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
}
```
- **Insertion Sort** 
```js
// Insertion Sort: Builds the sorted array one element at a time by inserting each element into its correct position
function insertionSort(arr) {
    let n = arr.length;
    // Start from the second element
    for (let i = 1; i < n; i++) {
        // Store the current element to be inserted
        let key = arr[i];
        let j = i - 1;
        // Move elements that are greater than key to one position ahead
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        // Place the key in its correct position
        arr[j + 1] = key;
    }
}
```
- **Merge Sort**
```js
// Merge: Merges two sorted subarrays into a single sorted array
function merge(arr, left, mid, right) {
    // Calculate sizes of the two subarrays
    let n1 = mid - left + 1;
    let n2 = right - mid;
    // Create temporary arrays for the left and right subarrays
    let L = new Array(n1);
    let R = new Array(n2);

    // Copy data to temporary arrays
    for (let i = 0; i < n1; i++) L[i] = arr[left + i];
    for (let i = 0; i < n2; i++) R[i] = arr[mid + 1 + i];

    // Merge the temporary arrays back into the original array
    let i = 0, j = 0, k = left;
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

    // Copy remaining elements of L, if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy remaining elements of R, if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Merge Sort: Recursively divides the array into halves and merges them in sorted order
function mergeSort(arr, left, right) {
    if (left < right) {
        // Calculate the middle point
        let mid = Math.floor(left + (right - left) / 2);
        // Recursively sort the left half
        mergeSort(arr, left, mid);
        // Recursively sort the right half
        mergeSort(arr, mid + 1, right);
        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}
```
- **Quick Sort** 
```js
// Partition: Selects a pivot and rearranges the array so that elements smaller than the pivot are on the left, and larger ones are on the right
function partition(arr, low, high) {
    // Choose the rightmost element as the pivot
    let pivot = arr[high];
    // Index of the smaller element
    let i = low - 1;
    // Traverse through all elements
    for (let j = low; j < high; j++) {
        // If current element is smaller than the pivot
        if (arr[j] < pivot) {
            i++;
            // Swap elements
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
    }
    // Place the pivot in its correct position
    [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];
    // Return the pivot's index
    return i + 1;
}

// Quick Sort: Recursively sorts the array by selecting a pivot and partitioning the array
function quickSort(arr, low, high) {
    if (low < high) {
        // Get the partition index
        let pi = partition(arr, low, high);
        // Recursively sort elements before and after the partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```
- **Heap Sort**
```js
// Heapify: Ensures the subtree rooted at index i maintains the max-heap property
function heapify(arr, n, i) {
    // Initialize largest as the root
    let largest = i;
    let left = 2 * i + 1;
    let right = 2 * i + 2;

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest]) largest = left;
    // If right child is larger than largest
    if (right < n && arr[right] > arr[largest]) largest = right;

    // If largest is not root, swap and continue heapifying
    if (largest !== i) {
        [arr[i], arr[largest]] = [arr[largest], arr[i]];
        heapify(arr, n, largest);
    }
}

// Heap Sort: Builds a max heap and repeatedly extracts the maximum element
function heapSort(arr) {
    let n = arr.length;
    // Build a max heap
    for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }

    // Extract elements from the heap one by one
    for (let i = n - 1; i > 0; i--) {
        // Move current root to the end
        [arr[0], arr[i]] = [arr[i], arr[0]];
        // Heapify the reduced heap
        heapify(arr, i, 0);
    }
}
```

- **Counting Sort** 
```js
// Counting Sort: Sorts an array by counting the frequency of each element
function countingSort(arr) {
    // Find the maximum value in the array
    let maxVal = Math.max(...arr);
    // Initialize count array with zeros
    let count = new Array(maxVal + 1).fill(0);
    // Initialize output array
    let output = new Array(arr.length);

    // Count occurrences of each element
    for (let i = 0; i < arr.length; i++) {
        count[arr[i]]++;
    }

    // Compute cumulative sum for sorting order
    for (let i = 1; i <= maxVal; i++) {
        count[i] += count[i - 1];
    }

    // Place elements in sorted order
    for (let i = arr.length - 1; i >= 0; i--) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

    // Copy sorted elements back to the original array
    for (let i = 0; i < arr.length; i++) {
        arr[i] = output[i];
    }
}
```
- **Radix Sort** 
```js
// Counting Sort for Radix Sort: Sorts based on the digit at the given exponent
function countingSortRadix(arr, exp) {
    // Initialize output and count arrays
    let output = new Array(arr.length);
    let count = new Array(10).fill(0);

    // Count occurrences of each digit
    for (let i = 0; i < arr.length; i++) {
        count[Math.floor(arr[i] / exp) % 10]++;
    }

    // Compute cumulative sum
    for (let i = 1; i < 10; i++) {
        count[i] += count[i - 1];
    }

    // Place elements in sorted order
    for (let i = arr.length - 1; i >= 0; i--) {
        output[count[Math.floor(arr[i] / exp) % 10] - 1] = arr[i];
        count[Math.floor(arr[i] / exp) % 10]--;
    }

    // Copy sorted elements back to the original array
    for (let i = 0; i < arr.length; i++) {
        arr[i] = output[i];
    }
}

// Radix Sort: Sorts numbers digit by digit using Counting Sort
function radixSort(arr) {
    // Find the maximum value to determine the number of digits
    let maxVal = Math.max(...arr);
    // Process each digit
    for (let exp = 1; Math.floor(maxVal / exp) > 0; exp *= 10) {
        countingSortRadix(arr, exp);
    }
}
```

### Linked List
- A Linked List is a linear data structure where elements (nodes) are connected using pointers. Each node contains a data part and a pointer to the next node.
-  **Singly Linked List (Node Structure):**
```js
// Node class for a singly linked list
class Node {
    constructor(data) {
        this.data = data; // Data stored in the node
        this.next = null; // Pointer to the next node
    }
}
```
- **Insertion at the head:** O(1)
```js
// Insert a node at the head of the linked list
function insertAtHead(head, value) {
    // Create a new node with the given value
    let newNode = new Node(value);
    // Point the new node to the current head
    newNode.next = head;
    // Return the new node as the new head
    return newNode;
}
```
 - **Insertion at the tail:** O(n)
```js
// Insert a node at the tail of the linked list
function insertAtTail(head, value) {
    // Create a new node with the given value
    let newNode = new Node(value);
    // If the list is empty, return the new node as head
    if (!head) return newNode;
    // Traverse to the last node
    let temp = head;
    while (temp.next) temp = temp.next;
    // Append the new node
    temp.next = newNode;
    // Return the head
    return head;
}
```
 - **Insertion at a specific position:** O(n)
```js
// Insert a node at a specific position in the linked list
function insertAtPosition(head, value, position) {
    // If inserting at position 1, use insertAtHead
    if (position === 1) return insertAtHead(head, value);
    // Traverse to the node before the insertion point
    let temp = head;
    for (let i = 1; i < position - 1; i++) {
        if (!temp) return head;
        temp = temp.next;
    }
    // If position is invalid, return the head
    if (!temp) return head;
    // Create and insert the new node
    let newNode = new Node(value);
    newNode.next = temp.next;
    temp.next = newNode;
    // Return the head
    return head;
}
```
 - **Deletion from the head:** O(1)
```js
// Delete the head node of the linked list
function deleteAtHead(head) {
    // If the list is empty, return null
    if (!head) return null;
    // Move head to the next node
    return head.next;
}
```
 - **Deletion from the tail:** O(n)
```js
// Delete the tail node of the linked list
function deleteAtTail(head) {
    // If the list is empty, return null
    if (!head) return null;
    // If there's only one node, return null
    if (!head.next) return null;
    // Traverse to the second-to-last node
    let temp = head;
    while (temp.next && temp.next.next) {
        temp = temp.next;
    }
    // Remove the last node
    temp.next = null;
    // Return the head
    return head;
}
```
- **Deletion at a specific position:** O(n)
```js
// Delete a node at a specific position in the linked list
function deleteAtPosition(head, position) {
    // If deleting at position 1, use deleteAtHead
    if (position === 1) return deleteAtHead(head);
    // Traverse to the node before the deletion point
    let temp = head;
    for (let i = 1; i < position - 1; i++) {
        if (!temp) return head;
        temp = temp.next;
    }
    // If position is invalid, return the head
    if (!temp || !temp.next) return head;
    // Skip the node to be deleted
    temp.next = temp.next.next;
    // Return the head
    return head;
}
```
- **Display List:** O(n)
```js
// Display all nodes in the linked list
function displayList(head) {
    // Start from the head
    let temp = head;
    let result = [];
    // Traverse the list and collect node data
    while (temp) {
        result.push(temp.data);
        temp = temp.next;
    }
    // Print the list
    console.log(result.join(' '));
}
```
- **Doubly Linked List (Node Structure):**
```js
// Node class for a doubly linked list
class DNode {
    constructor(data) {
        this.data = data; // Data stored in the node
        this.prev = null; // Pointer to the previous node
        this.next = null; // Pointer to the next node
    }
}
``` 

### Stack
- A Stack is a linear data structure that follows the LIFO (Last In, First Out) principle.
- **Node Structure (Stack):**
```js
// Stack class implementation using an array
class Stack {
    constructor() {
        this.arr = []; // Array to store stack elements
        this.top = -1; // Index of the top element
    }

    // Check if theנוstack is empty
    isEmpty() {
        return this.top === -1;
    }

    // Push an element onto the stack
    push(value) {
        // Add the element and increment top
        this.arr[++this.top] = value;
        console.log(`${value} pushed to stack`);
    }

    // Pop an element from the stack
    pop() {
        // If stack is empty, return -1
        if (this.isEmpty()) {
            console.log('Stack Underflow!');
            return -1;
        }
        // Return and remove the top element
        return this.arr[this.top--];
    }

    // Peek at the top element without removing it
    peek() {
        // If stack is empty, return -1
        if (this.isEmpty()) {
            console.log('Stack is empty!');
            return -1;
        }
        // Return the top element
        return this.arr[this.top];
    }

    // Display the stack elements
    display() {
        // If stack is empty, print message
        if (this.isEmpty()) {
            console.log('Stack is empty!');
            return;
        }
        // Print elements in reverse order (top to bottom)
        console.log('Stack:', this.arr.slice(0, this.top + 1).reverse().join(' '));
    }
}
```

### Queue
- A Queue is a linear data structure that follows the FIFO (First In, First Out) principle.
- **Node Structure (Queue):**
```js
// Queue class implementation using an array
class Queue {
    constructor() {
        this.arr = []; // Array to store queue elements
        this.front = -1; // Index of the front element
        this.rear = -1; // Index of the rear element
    }

    // Check if the queue is empty
    isEmpty() {
        return this.front === -1;
    }

    // Check if the queue is full (not typically used in dynamic arrays)
    isFull() {
        return this.rear === this.arr.length - 1;
    }

    // Enqueue an element into the queue
    enqueue(value) {
        // If queue is empty, set front to 0
        if (this.front === -1) this.front = 0;
        // Add element and increment rear
        this.arr[++this.rear] = value;
        console.log(`${value} enqueued to queue`);
    }

    // Dequeue an element from the queue
    dequeue() {
        // If queue is empty, return -1
        if (this.isEmpty()) {
            console.log('Queue Underflow!');
            return -1;
        }
        // Get the front element
        let value = this.arr[this.front];
        // If only one element, reset queue
        if (this.front === this.rear) {
            this.front = this.rear = -1;
        } else {
            // Move front to the next element
            this.front++;
        }
        // Return the dequeued value
        return value;
    }

    // Peek at the front element without removing it
    peek() {
        // If queue is empty, return -1
        if (this.isEmpty()) {
            console.log('Queue is empty!');
            return -1;
        }
        // Return the front element
        return this.arr[this.front];
    }

    // Display the queue elements
    display() {
        // If queue is empty, print message
        if (this.isEmpty()) {
            console.log('Queue is empty!');
            return;
        }
        // Print elements from front to rear
        console.log('Queue:', this.arr.slice(this.front, this.rear + 1).join(' '));
    }
}
```


### Heap (Binary Heap)

- A **Heap** is a complete binary tree, where each node satisfies the heap property:
  - **Min Heap**: The value of the parent node is less than or equal to the values of its children.
  - **Max Heap**: The value of the **parent** node is greater than or equal to the values of its children.

#### **Basic Heap Operations**

- **Insert Element in Heap**: \( O(log n) \)
```js
// Insert a value into a min heap
function insertHeap(heap, value) {
    // Add the value to the end of the heap
    heap.push(value);
    // Get the index of the newly added value
    let index = heap.length - 1;

    // Bubble up to maintain the min heap property
    while (index > 0) {
        // Calculate the parent index
        let parentIndex = Math.floor((index - 1) / 2);
        // If the new value is smaller than its parent, swap them
        if (heap[index] < heap[parentIndex]) {
            [heap[index], heap[parentIndex]] = [heap[parentIndex], heap[index]];
            index = parentIndex;
        } else {
            break;
        }
    }
}
```

- **Extract Min/Max from Heap**: \( O(log n) \)
```js
// Extract the minimum element from a min heap
function extractMin(heap) {
    // If heap is empty, return -1
    if (heap.length === 0) return -1;
    // Swap the root with the last element
    [heap[0], heap[heap.length - 1]] = [heap[heap.length - 1], heap[0]];
    // Store the minimum value
    let minValue = heap.pop();

    // Bubble down to maintain the min heap property
    let index = 0;
    while (index < heap.length) {
        let leftChildIndex = 2 * index + 1;
        let rightChildIndex = 2 * index + 2;
        let smallest = index;

        // Check if left child is smaller
        if (leftChildIndex < heap.length && heap[leftChildIndex] < heap[smallest]) {
            smallest = leftChildIndex;
        }
        // Check if right child is smaller
        if (rightChildIndex < heap.length && heap[rightChildIndex] < heap[smallest]) {
            smallest = rightChildIndex;
        }
        // If smallest is the current index, heap property is satisfied
        if (smallest === index) break;

        // Swap with the smallest child
        [heap[index], heap[smallest]] = [heap[smallest], heap[index]];
        index = smallest;
    }
    // Return the extracted minimum value
    return minValue;
}
```

- **Peek Min/Max (View top element without removal)**: \( O(1) \)
```js
// Peek at the minimum element in the heap without removing it
function peekMin(heap) {
    // If heap is empty, return -1
    if (heap.length === 0) return -1;
    // Return the root (minimum element)
    return heap[0];
}
```

- **Heapify an Array**: \( O(n) \)
```js
// Heapify a subtree rooted at index to maintain min heap property
function heapify(heap, n, index) {
    // Calculate indices of left and right children
    let leftChild = 2 * index + 1;
    let rightChild = 2 * index + 2;
    // Assume the smallest is the current index
    let smallest = index;

    // Check if left child is smaller
    if (leftChild < n && heap[leftChild] < heap[smallest]) {
        smallest = leftChild;
    }
    // Check if right child is smaller
    if (rightChild < n && heap[rightChild] < heap[smallest]) {
        smallest = rightChild;
    }

    // If smallest is not the current index, swap and continue heapifying
    if (smallest !== index) {
        [heap[index], heap[smallest]] = [heap[smallest], heap[index]];
        heapify(heap, n, smallest);
    }
}
```

- **Build Min Heap**: \( O(n) \)
```js
// Build a min heap from an array
function buildMinHeap(heap) {
    let n = heap.length;
    // Start from the last non-leaf node and heapify each node
    for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
        heapify(heap, n, i);
    }
}
```

- **Heap Sort**: \( O(n log n) \)
```js
// Heap Sort: Uses a min heap to sort the array
function heapSort(arr) {
    // Build a min heap
    buildMinHeap(arr);
    let n = arr.length;

    // Extract elements from the heap one by one
    for (let i = n - 1; i >= 0; i--) {
        // Move current root to the end
        [arr[0], arr[i]] = [arr[i], arr[0]];
        // Heapify the reduced heap
        heapify(arr, i, 0);
    }
}
```

### Priority Queue (using Heap)
- A **priority queue** is an abstract data structure that supports efficiently retrieving the element with the highest or lowest priority. It can be implemented using a **heap**.

```js
// Priority Queue class using a min heap
class PriorityQueue {
    constructor() {
        this.heap = []; // Array to store the heap
    }

    // Insert a value into the priority queue
    push(value) {
        insertHeap(this.heap, value);
    }

    // Remove and return the minimum value
    pop() {
        return extractMin(this.heap);
    }

    // Peek at the minimum value without removing it
    top() {
        return peekMin(this.heap);
    }
}
```

---

### Binary Search Tree (BST)
- A Binary Search Tree (BST) is a binary tree with the property that for each node:
    - All nodes in the left subtree have values less than the node.
    - All nodes in the right subtree have values greater than the node.
- **Node Structure (Binary Search Tree):**
```js
// Node class for a binary search tree
class TreeNode {
    constructor(data) {
        this.data = data; // Data stored in the node
        this.left = null; // Pointer to the left child
        this.right = null; // Pointer to the right child
    }
}
```

#### Basic Tree Operations
- **Insert Node (BST):** O(logn)
```js
// Insert a value into a binary search tree
function insert(root, value) {
    // If the tree is empty, create a new node
    if (!root) return new TreeNode(value);
    // If value is less than root, insert into left subtree
    if (value < root.data) {
        root.left = insert(root.left, value);
    } else {
        // If value is greater, insert into right subtree
        root.right = insert(root.right, value);
    }
    // Return the unchanged root
    return root;
}
```
- **In-order Traversal:** O(n)
```js
// Perform in-order traversal of a binary tree (left, root, right)
function inorder(root) {
    // Base case: If tree is empty, return
    if (!root) return;
    // Recursively traverse the left subtree
    inorder(root.left);
    // Process the current node
    console.log(root.data);
    // Recursively traverse the right subtree
    inorder(root.right);
}
```
- **Pre-order Traversal:** O(n)
```js
// Perform pre-order traversal of a binary tree (root, left, right)
function preorder(root) {
    // Base case: If tree is empty, return
    if (!root) return;
    // Process the current node
    console.log(root.data);
    // Recursively traverse the left subtree
    preorder(root.left);
    // Recursively traverse the right subtree
    preorder(root.right);
}
```
- **Post-order Traversal:** O(n)
```js
// Perform post-order traversal of a binary tree (left, right, root)
function postorder(root) {
    // Base case: If tree is empty, return
    if (!root) return;
    // Recursively traverse the left subtree
    postorder(root.left);
    // Recursively traverse the right subtree
    postorder(root.right);
    // Process the current node
    console.log(root.data);
}
```
- **Height of Tree:** O(n)
```js
// Calculate the height of a binary tree
function height(root) {
    // Base case: If tree is empty, height is 0
    if (!root) return 0;
    // Recursively compute the height of left and right subtrees
    return Math.max(height(root.left), height(root.right)) + 1;
}
```
- **Search in BST**: O(logn)
```js
// Search for a key in a binary search tree
function search(root, key) {
    // Base case: If tree is empty or key is found
    if (!root || root.data === key) return root;
    // If key is less than root, search left subtree
    if (key < root.data) return search(root.left, key);
    // If key is greater, search right subtree
    return search(root.right, key);
}
```
- **Delete Node in BST:** O(logn)
```js
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

