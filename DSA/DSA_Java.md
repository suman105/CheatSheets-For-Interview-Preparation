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
- An array is a collection of elements identified by index or key. In Java, arrays have a fixed size, but `ArrayList` can be used for dynamic sizing.
### 1. Searching Algorithms
- **Linear Search** 
```java
// Linear Search: Iterates through the array to find the target
public static int linearSearch(int[] arr, int target) {
    // Loop through each element in the array
    for (int i = 0; i < arr.length; i++) {
        // If the current element is the target, return its index
        if (arr[i] == target) return i;
    }
    // If target is not found, return -1
    return -1;
}
```
- **Binary Search** 
```java
// Binary Search: Searches a sorted array by repeatedly dividing the search interval in half
public static int binarySearch(int[] arr, int target) {
    // Initialize pointers for the left and right ends of the array
    int left = 0, right = arr.length - 1;
    // Continue searching while the left pointer is less than or equal to the right
    while (left <= right) {
        // Calculate the middle index, avoiding overflow
        int mid = left + (right - left) / 2;
        // If the middle element is the target, return its index
        if (arr[mid] == target) return mid;
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
```java
// Ternary Search: Divides the sorted array into three parts and searches recursively
public static int ternarySearch(int[] arr, int left, int right, int target) {
    // Base case: If the search interval is valid
    if (right >= left) {
        // Calculate the two mid points dividing the array into three parts
        int mid1 = left + (right - left) / 3;
        int mid2 = right - (right - left) / 3;
        // If target is found at mid1, return its index
        if (arr[mid1] == target) return mid1;
        // If target is found at mid2, return its index
        if (arr[mid2] == target) return mid2;
        // If target is less than mid1, search the left third
        if (target < arr[mid1]) 
            return ternarySearch(arr, left, mid1 - 1, target);
        // If target is greater than mid2, search the right third
        else if (target > arr[mid2]) 
            return ternarySearch(arr, mid2 + 1, right, target);
        // Otherwise, search the middle third
        else 
            return ternarySearch(arr, mid1 + 1, mid2 - 1, target);
    }
    // If target is not found, return -1
    return -1;
}
```
#### 2. Sorting Algorithms
- **Bubble Sort** 
```java
// Bubble Sort: Repeatedly steps through the array, compares adjacent elements and swaps them if they are in the wrong order
public static void bubbleSort(int[] arr) {
    // Get the length of the array
    int n = arr.length;
    // Outer loop for multiple passes through the array
    for (int i = 0; i < n - 1; i++) {
        // Inner loop to compare adjacent elements
        for (int j = 0; j < n - i - 1; j++) {
            // Swap if the current element is greater than the next
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```
- **Selection Sort**
```java
// Selection Sort: Repeatedly selects the minimum element from the unsorted portion and places it at the beginning
public static void selectionSort(int[] arr) {
    // Get the length of the array
    int n = arr.length;
    // Loop through each element
    for (int i = 0; i < n - 1; i++) {
        // Assume the current index has the minimum value
        int minIndex = i;
        // Find the minimum element in the unsorted portion
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        // Swap the found minimum element with the first element of the unsorted portion
        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}
```
- **Insertion Sort** 
```java
// Insertion Sort: Builds the sorted array one element at a time by inserting each element into its correct position
public static void insertionSort(int[] arr) {
    // Get the length of the array
    int n = arr.length;
    // Start from the second element
    for (int i = 1; i < n; i++) {
        // Store the current element to be inserted
        int key = arr[i];
        // Move elements that are greater than key to one position ahead
        int j = i - 1;
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
```java
// Merge: Merges two sorted subarrays into a single sorted array
private static void merge(int[] arr, int left, int mid, int right) {
    // Calculate sizes of the two subarrays
    int n1 = mid - left + 1;
    int n2 = right - mid;
    // Create temporary arrays for the left and right subarrays
    int[] L = new int[n1], R = new int[n2];
    
    // Copy data to temporary arrays
    System.arraycopy(arr, left, L, 0, n1);
    System.arraycopy(arr, mid + 1, R, 0, n2);
    
    // Merge the temporary arrays back into the original array
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        arr[k++] = L[i] <= R[j] ? L[i++] : R[j++];
    }
    // Copy remaining elements of L, if any
    while (i < n1) arr[k++] = L[i++];
    // Copy remaining elements of R, if any
    while (j < n2) arr[k++] = R[j++];
}

// Merge Sort: Recursively divides the array into halves and merges them in sorted order
public static void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        // Calculate the middle point
        int mid = left + (right - left) / 2;
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
```java
// Partition: Selects a pivot and rearranges the array so that elements smaller than the pivot are on the left, and larger ones are on the right
private static int partition(int[] arr, int low, int high) {
    // Choose the rightmost element as the pivot
    int pivot = arr[high];
    // Index of the smaller element
    int i = low - 1;
    // Traverse through all elements
    for (int j = low; j < high; j++) {
        // If current element is smaller than the pivot
        if (arr[j] < pivot) {
            i++;
            // Swap elements
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    // Place the pivot in its correct position
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    // Return the pivot's index
    return i + 1;
}

// Quick Sort: Recursively sorts the array by selecting a pivot and partitioning the array
public static void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        // Get the partition index
        int pi = partition(arr, low, high);
        // Recursively sort elements before and after the partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```
- **Heap Sort**
```java
// Heapify: Ensures the subtree rooted at index i maintains the max-heap property
private static void heapify(int[] arr, int n, int i) {
    // Initialize largest as the root
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    // If left child is larger than root
    if (left < n && arr[left] > arr[largest]) largest = left;
    // If right child is larger than largest
    if (right < n && arr[right] > arr[largest]) largest = right;
    // If largest is not root, swap and continue heapifying
    if (largest != i) {
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;
        heapify(arr, n, largest);
    }
}

// Heap Sort: Builds a max heap and repeatedly extracts the maximum element
public static void heapSort(int[] arr) {
    // Get the length of the array
    int n = arr.length;
    // Build a max heap
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
    // Extract elements from the heap one by one
    for (int i = n - 1; i > 0; i--) {
        // Move current root to the end
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        // Heapify the reduced heap
        heapify(arr, i, 0);
    }
}
```

- **Counting Sort** 
```java
// Counting Sort: Sorts an array by counting the frequency of each element
public static void countingSort(int[] arr) {
    // Find the maximum value in the array
    int max = Arrays.stream(arr).max().getAsInt();
    // Initialize count array with zeros
    int[] count = new int[max + 1];
    // Initialize output array
    int[] output = new int[arr.length];
    
    // Count occurrences of each element
    for (int num : arr) count[num]++;
    // Compute cumulative sum for sorting order
    for (int i = 1; i <= max; i++) count[i] += count[i - 1];
    // Place elements in sorted order
    for (int i = arr.length - 1; i >= 0; i--) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }
    // Copy sorted elements back to the original array
    System.arraycopy(output, 0, arr, 0, arr.length);
}
```
- **Radix Sort** 
```java
// Counting Sort for Radix Sort: Sorts based on the digit at the given exponent
private static void countingSortRadix(int[] arr, int exp) {
    // Initialize output and count arrays
    int[] output = new int[arr.length];
    int[] count = new int[10];
    
    // Count occurrences of each digit
    for (int num : arr) count[(num / exp) % 10]++;
    // Compute cumulative sum
    for (int i = 1; i < 10; i++) count[i] += count[i - 1];
    // Place elements in sorted order
    for (int i = arr.length - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }
    // Copy sorted elements back to the original array
    System.arraycopy(output, 0, arr, 0, arr.length);
}

// Radix Sort: Sorts numbers digit by digit using Counting Sort
public static void radixSort(int[] arr) {
    // Find the maximum value to determine the number of digits
    int max = Arrays.stream(arr).max().getAsInt();
    // Process each digit
    for (int exp = 1; max / exp > 0; exp *= 10) {
        countingSortRadix(arr, exp);
    }
}
```

### Linked List
- A Linked List is a linear data structure where elements (nodes) are connected using pointers. Each node contains a data part and a pointer to the next node.
-  **Singly Linked List (Node Structure):**
```java
// Node class for a singly linked list
class ListNode {
    int val; // Data stored in the node
    ListNode next; // Pointer to the next node
    ListNode(int x) { val = x; } // Constructor to initialize the node with a value
}
```
- **Insertion at the head:** O(1)
```java
 public void addAtHead(int val) 
 {
    // Create a new node with the given value
    ListNode newNode = new ListNode(val);
    // Point the new node to the current head
    newNode.next = head;
    // Update the head to the new node
    head = newNode;
}
```
 - **Insertion at the tail:** O(n)
```java
public void addAtTail(int val) 
{
    // If the list is empty, add at head
    if (head == null) {
        head = new ListNode(val);
        return;
    }
    // Traverse to the last node
    ListNode curr = head;
    while (curr.next != null) curr = curr.next;
    // Append the new node
    curr.next = new ListNode(val);
} 
```
 - **Insertion at a specific position:** O(n)
```java
public void addAtIndex(int index, int val) 
{
    // If inserting at index 0, use addAtHead
    if (index == 0) {
        addAtHead(val);
        return;
    }
    // Traverse to the node before the insertion point
    ListNode curr = head;
    for (int i = 0; i < index - 1 && curr != null; i++) {
        curr = curr.next;
    }
    // If index is invalid, return
    if (curr == null) return;
    // Create and insert the new node
    ListNode newNode = new ListNode(val);
    newNode.next = curr.next;
    curr.next = newNode;
}
```
 - **Deletion from the head:** O(1)
```java
public void deleteAtHead() 
{
    // If the list is not empty, move head to the next node
    if (head != null) head = head.next;
}
```
 - **Deletion from the tail:** O(n)
```java
    public void deleteAtTail() {
        // If the list is empty or has one node, set head to null
        if (head == null || head.next == null) {
            head = null;
            return;
        }
        // Traverse to the second-to-last node
        ListNode curr = head;
        while (curr.next.next != null) curr = curr.next;
        // Remove the last node
        curr.next = null;
    }
```
- **Deletion at a specific position:** O(n)
```java
  public void deleteAtIndex(int index) {
    // If deleting at index 0, use deleteAtHead
    if (index == 0) {
        deleteAtHead();
        return;
    }
    // Traverse to the node before the deletion point
    ListNode curr = head;
    for (int i = 0; i < index - 1 && curr != null; i++) {
        curr = curr.next;
    }
    // If index is invalid, return
    if (curr == null || curr.next == null) return;
    // Skip the node to be deleted
    curr.next = curr.next.next;
}
```

- **Display:** O(n)
```java
public void display() {
    // Start from the head
    ListNode curr = head;
    // Traverse the list and print node values
    while (curr != null) {
        System.out.print(curr.val + " ");
        curr = curr.next;
    }
    System.out.println();
}
```

- **Doubly Linked List (Node Structure):**
```java
// Node class for a doubly linked list
class ListDNode {
    int data; // Data stored in the node
    ListDNode prev; // Pointer to the previous node
    ListDNode next; // Pointer to the next node
    
    // Constructor to initialize the node with a value
    ListDNode(int val) {
        data = val;
        prev = null;
        next = null;
    }
}
``` 

### Stack
- A Stack is a linear data structure that follows the LIFO (Last In, First Out) principle.
#### **Stack Implementation:**
```java
// Stack class implementation using an array
class ArrayStack {
    private int maxSize; // Maximum size of the stack
    private int[] stackArray; // Array to store stack elements
    private int top; // Index of the top element
    
    // Constructor to initialize the stack with a given size
    public ArrayStack(int size) {
        maxSize = size;
        stackArray = new int[maxSize];
        top = -1;
    }
    
    // Push an element onto the stack
    public void push(int x) {
        // Check for stack overflow
        if (isFull()) throw new RuntimeException("Stack overflow");
        // Add element and increment top
        stackArray[++top] = x;
    }
    
    // Pop an element from the stack
    public int pop() {
        // Check for stack underflow
        if (isEmpty()) throw new RuntimeException("Stack underflow");
        // Return and remove the top element
        return stackArray[top--];
    }
    
    // Peek at the top element without removing it
    public int peek() {
        // Check if stack is empty
        if (isEmpty()) throw new RuntimeException("Stack is empty");
        // Return the top element
        return stackArray[top];
    }
    
    // Check if the stack is empty
    public boolean isEmpty() {
        return top == -1;
    }
    
    // Check if the stack is full
    public boolean isFull() {
        return top == maxSize - 1;
    }
    
    // Display the stack elements
    public void display() {
        // If stack is empty, print message
        if (isEmpty()) {
            System.out.println("Stack is empty");
            return;
        }
        // Print elements from top to bottom
        System.out.print("Stack: ");
        for (int i = top; i >= 0; i--) {
            System.out.print(stackArray[i] + " ");
        }
        System.out.println();
    }
}
```

### Queue
- A Queue is a linear data structure that follows the FIFO (First In, First Out) principle.
#### **Queue Implementation:**
```java
// Queue class implementation using an array
class ArrayQueue {
    private int[] arr; // Array to store queue elements
    private int front, rear, capacity; // Indices and capacity of the queue
    
    // Constructor to initialize the queue with a given size
    public ArrayQueue(int size) {
        capacity = size;
        arr = new int[capacity];
        front = rear = -1;
    }
    
    // Enqueue an element into the queue
    public void enqueue(int x) {
        // Check for queue overflow
        if (isFull()) throw new RuntimeException("Queue overflow");
        // If queue is empty, set front to 0
        if (isEmpty()) front = 0;
        // Add element and increment rear
        arr[++rear] = x;
    }
    
    // Dequeue an element from the queue
    public int dequeue() {
        // Check for queue underflow
        if (isEmpty()) throw new RuntimeException("Queue underflow");
        // Get the front element
        int x = arr[front];
        // If only one element, reset queue
        if (front == rear) front = rear = -1;
        // Otherwise, increment front
        else front++;
        // Return the dequeued value
        return x;
    }
    
    // Peek at the front element without removing it
    public int peek() {
        // Check if queue is empty
        if (isEmpty()) throw new RuntimeException("Queue is empty");
        // Return the front element
        return arr[front];
    }
    
    // Check if the queue is empty
    public boolean isEmpty() {
        return front == -1;
    }
    
    // Check if the queue is full
    public boolean isFull() {
        return rear == capacity - 1;
    }
    
    // Display the queue elements
    public void display() {
        // If queue is empty, print message
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return;
        }
        // Print elements from front to rear
        System.out.print("Queue: ");
        for (int i = front; i <= rear; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}
```


### Heap (Binary Heap)

- A **Heap** is a complete binary tree, where each node satisfies the heap property:
  - **Min Heap**: The value of the parent node is less than or equal to the values of its children.
  - **Max Heap**: The value of the **parent** node is greater than or equal to the values of its children.
```java
// Min Heap class implementation using an array
class MinHeap {
    private int[] heap; // Array to store heap elements
    private int size; // Current size of the heap
    private int capacity; // Maximum capacity of the heap
    
    // Constructor to initialize the heap with a given capacity
    public MinHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        heap = new int[capacity];
    }
    
    // Get the parent index of a node
    private int parent(int i) {
        return (i - 1) / 2;
    }
    
    // Get the left child index of a node
    private int left(int i) {
        return 2 * i + 1;
    }
    
    // Get the right child index of a node
    private int right(int i) {
        return 2 * i + 2;
    }
    
    // Insert a value into the heap: O(log n)
    public void insert(int k) {
        // Check for heap overflow
        if (size == capacity) throw new RuntimeException("Heap overflow");
        // Add the value to the end of the heap
        heap[size++] = k;
        // Bubble up to maintain the min heap property
        int i = size - 1;
        while (i != 0 && heap[parent(i)] > heap[i]) {
            swap(i, parent(i));
            i = parent(i);
        }
    }
    
    // Extract the minimum element: O(log n)
    public int extractMin() {
        // Check for heap underflow
        if (size <= 0) throw new RuntimeException("Heap underflow");
        // If only one element, return it
        if (size == 1) return heap[--size];
        
        // Store the minimum value
        int root = heap[0];
        // Move the last element to the root
        heap[0] = heap[--size];
        // Bubble down to maintain the min heap property
        heapify(0);
        // Return the extracted minimum value
        return root;
    }
    
    // Heapify a subtree rooted at index i: O(log n)
    private void heapify(int i) {
        // Initialize smallest as the current index
        int l = left(i), r = right(i), smallest = i;
        // Check if left child is smaller
        if (l < size && heap[l] < heap[i]) smallest = l;
        // Check if right child is smaller
        if (r < size && heap[r] < heap[smallest]) smallest = r;
        // If smallest is not the current index, swap and continue
        if (smallest != i) {
            swap(i, smallest);
            heapify(smallest);
        }
    }
    
    // Swap two elements in the heap
    private void swap(int i, int j) {
        int temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }
    
    // Build a min heap from an array: O(n)
    public void buildHeap(int[] arr) {
        // Check if array is too large
        if (arr.length > capacity) throw new RuntimeException("Array too large");
        // Copy array to heap
        System.arraycopy(arr, 0, heap, 0, arr.length);
        size = arr.length;
        // Start from the last non-leaf node and heapify each node
        for (int i = size / 2 - 1; i >= 0; i--) {
            heapify(i);
        }
    }
    
    // Peek at the minimum element: O(1)
    public int peek() {
        // Check if heap is empty
        if (size == 0) throw new RuntimeException("Heap is empty");
        // Return the root (minimum element)
        return heap[0];
    }
    
    // Display the heap: O(n)
    public void display() {
        // If heap is empty, print message
        if (size == 0) {
            System.out.println("Heap is empty");
            return;
        }
        // Print heap elements
        System.out.print("Heap: ");
        for (int i = 0; i < size; i++) {
            System.out.print(heap[i] + " ");
        }
        System.out.println();
    }
}
```

### Priority Queue (using Heap)
- A priority queue is an abstract data structure that supports efficiently retrieving the element with the highest or lowest priority.
  
#### **Priority Queue Implementation:**
```java
// Priority Queue class using a min heap
class PriorityQueue {
    private MinHeap heap; // MinHeap to store elements

    // Constructor to initialize the priority queue with a given capacity
    public PriorityQueue(int capacity) {
        heap = new MinHeap(capacity);
    }

    // Insert a value into the priority queue
    public void push(int value) {
        heap.insert(value);
    }

    // Remove and return the minimum value
    public int pop() {
        return heap.extractMin();
    }

    // Peek at the minimum value without removing it
    public int top() {
        return heap.peek();
    }

    // Check if the priority queue is empty
    public boolean isEmpty() {
        return heap.peek() == 0; // Assuming peek throws exception or returns 0 for empty
    }

    // Display the priority queue
    public void display() {
        heap.display();
    }
}
```


---

### Binary Search Tree (BST)
- A Binary Search Tree (BST) is a binary tree with the property that for each node:
    - All nodes in the left subtree have values less than the node.
    - All nodes in the right subtree have values greater than the node.
- **Node Structure (Binary Search Tree):**
```java
// Definition for a Binary Tree Node
class TreeNode {
    int data;   // Stores the value of the node
    TreeNode left;  // Reference to the left child
    TreeNode right; // Reference to the right child

    // Constructor to initialize a new node
    TreeNode(int val) {
        data = val;
        left = null;
        right = null;
    }
}
```

#### Basic Tree Operations
- **Insert Node (BST):** O(logn)
```java
// Function to insert a value into a Binary Search Tree (BST)
public TreeNode insert(TreeNode root, int value) {
    // Base case: If the tree is empty, create a new node and return it
    if (root == null) {
        return new TreeNode(value);
    }

    // If the value to insert is smaller, recurse on the left subtree
    if (value < root.data) {
        root.left = insert(root.left, value);
    } 
    // If the value to insert is greater, recurse on the right subtree
    else {
        root.right = insert(root.right, value);
    }

    // Return the unchanged root pointer
    return root;
}
```
- **In-order Traversal:** O(n)
```java
// Function to perform inorder traversal of a Binary Tree
public void inorder(TreeNode root) {
    // Base case: If the tree is empty, return
    if (root == null) 
        return;

    // Recursively visit the left subtree
    inorder(root.left);

    // Process the current node (print its data)
    System.out.print(root.data + " ");

    // Recursively visit the right subtree
    inorder(root.right);
}
```
- **Pre-order Traversal:** O(n)
```java
// Function to perform preorder traversal of a Binary Tree
public void preorder(TreeNode root) {
    // Base case: If the tree is empty, return
    if (root == null) 
        return;

    // Process the current node (print its data)
    System.out.print(root.data + " ");

    // Recursively visit the left subtree
    preorder(root.left);

    // Recursively visit the right subtree
    preorder(root.right);
}
```
- **Post-order Traversal:** O(n)
```java
// Function to perform postorder traversal of a Binary Tree
public void postorder(TreeNode root) {
    // Base case: If the tree is empty, return
    if (root == null) 
        return;

    // First, recursively visit the left subtree
    postorder(root.left);

    // Then, recursively visit the right subtree
    postorder(root.right);

    // Finally, process the current node (print its data)
    System.out.print(root.data + " ");
}
```
- **Height of Tree:** O(n)
```java
// Function to calculate the height of a Binary Tree
public int height(TreeNode root) {
    // Base case: If the tree is empty, height is 0
    if (root == null) 
        return 0;

    // Recursively compute the height of the left and right subtrees
    // The height of the tree is the maximum height of the left or right subtree plus 1 (for the root)
    return Math.max(height(root.left), height(root.right)) + 1;
}
```
- **Search in BST**: O(logn)
```java
// Function to search for a key in a Binary Search Tree (BST)
public TreeNode search(TreeNode root, int key) {
    // Base case: If the tree is empty or the key is found at the root
    if (root == null || root.data == key) 
        return root;

    // If the key is smaller than the root's key, search in the left subtree
    if (key < root.data) 
        return search(root.left, key);

    // If the key is greater than the root's key, search in the right subtree
    return search(root.right, key);
}
```
- **Delete Node in BST:** O(logn)
```java
// Function to delete a node from a Binary Search Tree (BST)
public TreeNode deleteNode(TreeNode root, int key) {
    // Base case: If the tree is empty or key is not found
    if (root == null) return root;

    // If the key is smaller than the root's key, it lies in the left subtree
    if (key < root.data) {
        root.left = deleteNode(root.left, key);
    }
    // If the key is greater than the root's key, it lies in the right subtree
    else if (key > root.data) {
        root.right = deleteNode(root.right, key);
    }
    // If the key is the same as root's key, then this is the node to be deleted
    else {
        // Case 1: Node has no left child
        if (root.left == null) {
            TreeNode temp = root.right; // Store the right child
            root = null; // Allow garbage collection to free the current node
            return temp; // Return the right child to maintain BST structure
        }
        // Case 2: Node has no right child
        else if (root.right == null) {
            TreeNode temp = root.left; // Store the left child
            root = null; // Allow garbage collection to free the current node
            return temp; // Return the left child to maintain BST structure
        }

        // Case 3: Node has two children
        // Find the inorder successor (smallest node in the right subtree)
        TreeNode temp = minValueNode(root.right);
        
        // Copy the inorder successor's value to this node
        root.data = temp.data;
        
        // Delete the inorder successor from the right subtree
        root.right = deleteNode(root.right, temp.data);
    }

    return root; // Return the modified root node
}

// Function to find the node with the smallest value in a BST
public TreeNode minValueNode(TreeNode node) {
    TreeNode current = node;

    // The leftmost leaf will have the smallest value
    while (current != null && current.left != null) {
        current = current.left;
    }

    return current; // Return the node with the smallest value
}
```

---

