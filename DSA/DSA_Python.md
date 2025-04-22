# Data Structures & Algorithms (DSA) Cheatsheet

## 1. Time & **Space** Complexity

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
```py
// Linear Search: Iterates through the list to find the target
def linear_search(arr, target):
    // Loop through each element in the list
    for i in range(len(arr)):
        // If the current element is the target, return its index
        if arr[i] == target:
            return i
    // If target is not found, return -1
    return -1
```
- **Binary Search** 
```py
// Binary Search: Searches a sorted list by repeatedly dividing the search interval in half
def binary_search(arr, target):
    // Initialize pointers for the left and right ends of the list
    left, right = 0, len(arr) - 1
    // Continue searching while the left pointer is less than or equal to the right
    while left <= right:
        // Calculate the middle index, avoiding overflow
        mid = left + (right - left) // 2
        // If the middle element is the target, return its index
        if arr[mid] == target:
            return mid
        // If target is greater, ignore the left half
        elif arr[mid] < target:
            left = mid + 1
        // If target is smaller, ignore the right half
        else:
            right = mid - 1
    // If target is not found, return -1
    return -1
```

- **Ternary Search** 
```py
// Ternary Search: Divides the sorted list into three parts and searches recursively
def ternary_search(arr, left, right, target):
    // Base case: If the search interval is valid
    if right >= left:
        // Calculate the two mid points dividing the list into three parts
        mid1 = left + (right - left) // 3
        mid2 = right - (right - left) // 3
        // If target is found at mid1, return its index
        if arr[mid1] == target:
            return mid1
        // If target is found at mid2, return its index
        if arr[mid2] == target:
            return mid2
        // If target is less than mid1, search the left third
        if target < arr[mid1]:
            return ternary_search(arr, left, mid1 - 1, target)
        // If target is greater than mid2, search the right third
        elif target > arr[mid2]:
            return ternary_search(arr, mid2 + 1, right, target)
        // Otherwise, search the middle third
        else:
            return ternary_search(arr, mid1 + 1, mid2 - 1, target)
    // If target is not found, return -1
    return -1
```
#### 2. Sorting Algorithms
- **Bubble Sort** 
```py
// Bubble Sort: Repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order
def bubble_sort(arr):
    // Get the length of the list
    n = len(arr)
    // Outer loop for multiple passes through the list
    for i in range(n):
        // Inner loop to compare adjacent elements
        for j in range(0, n - i - 1):
            // Swap if the current element is greater than the next
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
```
- **Selection Sort**
```py
// Selection Sort: Repeatedly selects the minimum element from the unsorted portion and places it at the beginning
def selection_sort(arr):
    // Loop through each element
    for i in range(len(arr)):
        // Assume the current index has the minimum value
        min_idx = i
        // Find the minimum element in the unsorted portion
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[min_idx]:
                min_idx = j
        // Swap the found minimum element with the first element of the unsorted portion
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
```
- **Insertion Sort** 
```py
// Insertion Sort: Builds the sorted list one element at a time by inserting each element into its correct position
def insertion_sort(arr):
    // Start from the second element
    for i in range(1, len(arr)):
        // Store the current element to be inserted
        key = arr[i]
        // Move elements that are greater than key to one position ahead
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        // Place the key in its correct position
        arr[j + 1] = key
```
- **Merge Sort**
```py
// Merge Sort: Recursively divides the list into halves and merges them in sorted order
def merge_sort(arr):
    // Base case: If list has more than one element
    if len(arr) > 1:
        // Calculate the middle point
        mid = len(arr) // 2
        // Divide the list into left and right halves
        L = arr[:mid]
        R = arr[mid:]
        
        // Recursively sort the left and right halves
        merge_sort(L)
        merge_sort(R)
        
        // Merge the sorted halves
        i = j = k = 0
        // Compare elements from both halves and merge in sorted order
        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1
        
        // Copy remaining elements of L, if any
        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1
        
        // Copy remaining elements of R, if any
        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1
```
- **Quick Sort** 
```py
// Partition: Selects a pivot and rearranges the list so that elements smaller than the pivot are on the left, and larger ones are on the right
def partition(arr, low, high):
    // Choose the rightmost element as the pivot
    pivot = arr[high]
    // Index of the smaller element
    i = low - 1
    // Traverse through all elements
    for j in range(low, high):
        // If current element is smaller than the pivot
        if arr[j] < pivot:
            i += 1
            // Swap elements
            arr[i], arr[j] = arr[j], arr[i]
    // Place the pivot in its correct position
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    // Return the pivot's index
    return i + 1

// Quick Sort: Recursively sorts the list by selecting a pivot and partitioning the list
def quick_sort(arr, low, high):
    if low < high:
        // Get the partition index
        pi = partition(arr, low, high)
        // Recursively sort elements before and after the partition
        quick_sort(arr, low, pi - 1)
        quick_sort(arr, pi + 1, high)
```
- **Heap Sort**
```py
// Heapify: Ensures the subtree rooted at index i maintains the max-heap property
def heapify(arr, n, i):
    // Initialize largest as the root
    largest = i
    l = 2 * i + 1
    r = 2 * i + 2
    
    // If left child is larger than root
    if l < n and arr[i] < arr[l]:
        largest = l
    // If right child is larger than largest
    if r < n and arr[largest] < arr[r]:
        largest = r
    // If largest is not root, swap and continue heapifying
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

// Heap Sort: Builds a max heap and repeatedly extracts the maximum element
def heap_sort(arr):
    // Get the length of the list
    n = len(arr)
    // Build a max heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)
    // Extract elements from the heap one by one
    for i in range(n - 1, 0, -1):
        // Move current root to the end
        arr[i], arr[0] = arr[0], arr[i]
        // Heapify the reduced heap
        heapify(arr, i, 0)
```

- **Counting Sort** 
```py
// Heapify: Ensures the subtree rooted at index i maintains the max-heap property
def heapify(arr, n, i):
    // Initialize largest as the root
    largest = i
    l = 2 * i + 1
    r = 2 * i + 2
    
    // If left child is larger than root
    if l < n and arr[i] < arr[l]:
        largest = l
    // If right child is larger than largest
    if r < n and arr[largest] < arr[r]:
        largest = r
    // If largest is not root, swap and continue heapifying
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

// Heap Sort: Builds a max heap and repeatedly extracts the maximum element
def heap_sort(arr):
    // Get the length of the list
    n = len(arr)
    // Build a max heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)
    // Extract elements from the heap one by one
    for i in range(n - 1, 0, -1):
        // Move current root to the end
        arr[i], arr[0] = arr[0], arr[i]
        // Heapify the reduced heap
        heapify(arr, i, 0)
```
- **Radix Sort** 
```py
// Counting Sort for Radix Sort: Sorts based on the digit at the given exponent
def counting_sort_radix(arr, exp):
    // Get the length of the list
    n = len(arr)
    // Initialize output and count arrays
    output = [0] * n
    count = [0] * 10
    
    // Count occurrences of each digit
    for i in range(n):
        index = arr[i] // exp
        count[index % 10] += 1
    
    // Compute cumulative sum
    for i in range(1, 10):
        count[i] += count[i - 1]
    
    // Place elements in sorted order
    i = n - 1
    while i >= 0:
        index = arr[i] // exp
        output[count[index % 10] - 1] = arr[i]
        count[index % 10] -= 1
        i -= 1
    
    // Copy sorted elements back to the original list
    for i in range(n):
        arr[i] = output[i]

// Radix Sort: Sorts numbers digit by digit using Counting Sort
def radix_sort(arr):
    // Find the maximum value to determine the number of digits
    max_val = max(arr)
    // Process each digit
    exp = 1
    while max_val // exp > 0:
        counting_sort_radix(arr, exp)
        exp *= 10
```

### Linked List
- A Linked List is a linear data structure where elements (nodes) are connected using pointers. Each node contains a data part and a pointer to the next node.
-  **Singly Linked List (Node Structure):**
```py
// Node class for a singly linked list
class Node:
    def __init__(self, data):
        self.data = data  // Data stored in the node
        self.next = None  // Pointer to the next node
```
- **Insertion at the head:** O(1)
```py
def insert_at_head(self, data):
    // Create a new node with the given data
    new_node = Node(data)
    // Point the new node to the current head
    new_node.next = self.head
    // Update the head to the new node
    self.head = new_node
```
 - **Insertion at the tail:** O(n)
```py
def insert_at_tail(self, data):
    // Create a new node with the given data
    new_node = Node(data)
    // If the list is empty, set the new node as head
    if not self.head:
        self.head = new_node
        return
    // Traverse to the last node
    last = self.head
    while last.next:
        last = last.next
    // Append the new node
    last.next = new_node
```
 - **Insertion at a specific position:** O(n)
```py
 def insert_at_position(self, data, position):
    // If inserting at position 1, use insert_at_head
    if position == 1:
        self.insert_at_head(data)
        return
    // Create a new node
    new_node = Node(data)
    // Traverse to the node before the insertion point
    temp = self.head
    for i in range(1, position - 1):
        if not temp:
            return  // Position out of bounds
        temp = temp.next
    // If position is invalid, return
    if not temp:
        return
    // Insert the new node
    new_node.next = temp.next
    temp.next = new_node
```
 - **Deletion from the head:** O(1)
```py
def delete_at_head(self):
    // If the list is empty, return
    if not self.head:
        return
    // Move head to the next node
    self.head = self.head.next
```
 - **Deletion from the tail:** O(n)
```py
def delete_at_tail(self):
    // If the list is empty, return
    if not self.head:
        return
    // If there's only one node, remove it
    if not self.head.next:
        self.head = None
        return
    // Traverse to the second-to-last node
    temp = self.head
    while temp.next and temp.next.next:
        temp = temp.next
    // Remove the last node
    temp.next = None
```
- **Deletion at a specific position:** O(n)
```py
def delete_at_position(self, position):
    // If deleting at position 1, use delete_at_head
    if position == 1:
        self.delete_at_head()
        return
    // Traverse to the node before the deletion point
    temp = self.head
    for i in range(1, position - 1):
        if not temp:
            return  // Position out of bounds
        temp = temp.next
    // If position is invalid, return
    if not temp or not temp.next:
        return
    // Skip the node to be deleted
    temp.next = temp.next.next
```
- **Display List:** O(n)
```py
def display(self):
    // Initialize an empty list to store node data
    elements = []
    // Start from the head
    current = self.head
    // Traverse the list and collect node data
    while current:
        elements.append(str(current.data))
        current = current.next
    // Print the list
    print(" -> ".join(elements))
```
- **Doubly Linked List (Node Structure):**
```py
// Node class for a doubly linked list
class DNode:
    def __init__(self, data):
        self.data = data  // Data stored in the node
        self.prev = None  // Pointer to the previous node
        self.next = None  // Pointer to the next node
``` 

### Stack
- A Stack is a linear data structure that follows the LIFO (Last In, First Out) principle.
- **Node Structure (Stack):**
```py
// Stack class implementation using a list
class Stack:
    def __init__(self):
        self.items = []  // Initialize an empty list to store stack elements

    // Push an element onto the stack
    def push(self, item):
        // Append the item to the end of the list
        self.items.append(item)

    // Pop an element from the stack
    def pop(self):
        // If stack is not empty, remove and return the top element
        if not self.is_empty():
            return self.items.pop()
        // If stack is empty, return None
        return None

    // Peek at the top element without removing it
    def peek(self):
        // If stack is not empty, return the top element
        if not self.is_empty():
            return self.items[-1]
        // If stack is empty, return None
        return None

    // Check if the stack is empty
    def is_empty(self):
        return len(self.items) == 0

    // Return the size of the stack
    def size(self):
        return len(self.items)

    // Display the stack elements
    def display(self):
        // Print elements in reverse order (top to bottom)
        print("Stack:", " ".join(map(str, self.items[::-1])))
```

### Queue
- A Queue is a linear data structure that follows the FIFO (First In, First Out) principle.
- **Node Structure (Queue):**
```py
// Import deque
from collections import deque

// Queue class implementation using a deque
class Queue:
    def __init__(self):
        self.items = deque()  // Initialize an empty deque to store queue elements

    // Enqueue an element into the queue
    def enqueue(self, item):
        // Append the item to the right end of the deque
        self.items.append(item)

    // Dequeue an element from the queue
    def dequeue(self):
        // If queue is not empty, remove and return the leftmost element
        if not self.is_empty():
            return self.items.popleft()
        // If queue is empty, return None
        return None

    // Peek at the front element without removing it
    def peek(self):
        // If queue is not empty, return the front element
        if not self.is_empty():
            return self.items[0]
        // If queue is empty, return None
        return None

    // Check if the queue is empty
    def is_empty(self):
        return len(self.items) == 0

    // Return the size of the queue
    def size(self):
        return len(self.items)

    // Display the queue elements
    def display(self):
        // Print elements from front to rear
        print("Queue:", " ".join(map(str, self.items)))
```


### Heap (Binary Heap)

- A **Heap** is a complete binary tree, where each node satisfies the heap property:
  - **Min Heap**: The value of the parent node is less than or equal to the values of its children.
  - **Max Heap**: The value of the **parent** node is greater than or equal to the values of its children.

#### **Heap Operations (using heapq):**
```py
import heapq

// Min Heap Operations
def min_heap_operations():
    // Initialize an empty min heap
    heap = []
    
    // Push elements: O(log n)
    heapq.heappush(heap, 3)  // Add 3 to the heap
    heapq.heappush(heap, 1)  // Add 1 to the heap
    heapq.heappush(heap, 2)  // Add 2 to the heap
    
    // Pop the smallest element: O(log n)
    min_val = heapq.heappop(heap)  // Returns 1
    
    // Peek at the smallest element: O(1)
    peek_val = heap[0] if heap else None  // Returns 2 if heap is not empty
    
    // Heapify a list: O(n)
    arr = [3, 1, 2]
    heapq.heapify(arr)  // Converts arr into a min heap
    
    return heap, min_val, peek_val, arr

// Max Heap Operations (using negative values)
def max_heap_operations():
    // Initialize an empty max heap
    max_heap = []
    
    // Push elements: O(log n)
    heapq.heappush(max_heap, -3)  // Add -3 to simulate 3
    heapq.heappush(max_heap, -1)  // Add -1 to simulate 1
    heapq.heappush(max_heap, -2)  // Add -2 to simulate 2
    
    // Pop the largest element: O(log n)
    max_val = -heapq.heappop(max_heap)  // Returns 3
    
    // Peek at the largest element: O(1)
    peek_val = -max_heap[0] if max_heap else None  // Returns 2 if heap is not empty
    
    return max_heap, max_val, peek_val
```

#### **Custom Min Heap Implementation:**
```py
// Custom Min Heap implementation
class MinHeap:
    def __init__(self):
        self.heap = []  // Initialize an empty list to store heap elements

    // Insert a value into the heap: O(log n)
    def insert(self, value):
        // Add the value to the end of the heap
        self.heap.append(value)
        // Bubble up to maintain the min heap property
        self._bubble_up(len(self.heap) - 1)

    // Helper function to bubble up an element
    def _bubble_up(self, index):
        // Calculate the parent index
        parent = (index - 1) // 2
        // Continue until the root or heap property is satisfied
        while index > 0 and self.heap[index] < self.heap[parent]:
            // Swap with parent
            self.heap[index], self.heap[parent] = self.heap[parent], self.heap[index]
            index = parent
            parent = (index - 1) // 2

    // Extract the minimum element: O(log n)
    def extract_min(self):
        // If heap is empty, return None
        if not self.heap:
            return None
        // If there's only one element, return it
        if len(self.heap) == 1:
            return self.heap.pop()
        // Store the minimum value
        min_val = self.heap[0]
        // Move the last element to the root
        self.heap[0] = self.heap.pop()
        // Bubble down to maintain the min heap property
        self._bubble_down(0)
        return min_val

    // Helper function to bubble down an element
    def _bubble_down(self, index):
        // Initialize the smallest as the current index
        smallest = index
        left = 2 * index + 1
        right = 2 * index + 2
        
        // Check if left child is smaller
        if left < len(self.heap) and self.heap[left] < self.heap[smallest]:
            smallest = left
        // Check if right child is smaller
        if right < len(self.heap) and self.heap[right] < self.heap[smallest]:
            smallest = right
        
        // If smallest is not the current index, swap and continue
        if smallest != index:
            self.heap[index], self.heap[smallest] = self.heap[smallest], self.heap[index]
            self._bubble_down(smallest)

    // Peek at the minimum element: O(1)
    def peek(self):
        // Return the root if heap is not empty, else None
        return self.heap[0] if self.heap else None

    // Heapify a list: O(n)
    def heapify(self, arr):
        // Copy the input list to the heap
        self.heap = arr[:]
        // Start from the last non-leaf node and heapify each node
        for i in range(len(self.heap) // 2 - 1, -1, -1):
            self._bubble_down(i)

    // Display the heap
    def display(self):
        print("Heap:", " ".join(map(str, self.heap)))
```

### Priority Queue (using Heap)
- A **priority queue** is an abstract data structure that supports efficiently retrieving the element with the highest or lowest priority. It can be implemented using a **heap**.

```py
// Priority Queue class using a min heap
class PriorityQueue:
    def __init__(self):
        self.heap = MinHeap()  // Use the custom MinHeap class

    // Insert a value into the priority queue
    def push(self, value):
        self.heap.insert(value)

    // Remove and return the minimum value
    def pop(self):
        return self.heap.extract_min()

    // Peek at the minimum value without removing it
    def top(self):
        return self.heap.peek()

    // Check if the priority queue is empty
    def is_empty(self):
        return not self.heap.heap

    // Display the priority queue
    def display(self):
        self.heap.display()
```

---

### Binary Search Tree (BST)
- A Binary Search Tree (BST) is a binary tree with the property that for each node:
    - All nodes in the left subtree have values less than the node.
    - All nodes in the right subtree have values greater than the node.
- **Node Structure (Binary Search Tree):**
```py
// Node class for a binary search tree
class TreeNode:
    def __init__(self, val):
        self.val = val  // Data stored in the node
        self.left = None  // Pointer to the left child
        self.right = None  // Pointer to the right child
```

#### Basic Tree Operations
- **Insert Node (BST):** O(logn)
```py
def insert(self, val):
    // If the tree is empty, set the new node as root
    if not self.root:
        self.root = TreeNode(val)
    else:
        // Recursively insert the value
        self._insert(self.root, val)

// Helper function to insert a value recursively
def _insert(self, node, val):
    // If value is less than node, insert into left subtree
    if val < node.val:
        if node.left:
            self._insert(node.left, val)
        else:
            node.left = TreeNode(val)
    // If value is greater, insert into right subtree
    else:
        if node.right:
            self._insert(node.right, val)
        else:
            node.right = TreeNode(val)
```
- **In-order Traversal:** O(n)
```py
def inorder(self):
    self._inorder(self.root)
    print()  // Newline for clean output

// Helper function for in-order traversal (left, root, right)
def _inorder(self, node):
    if node:
        // Recursively traverse the left subtree
        self._inorder(node.left)
        // Process the current node
        print(node.val, end=' ')
        // Recursively traverse the right subtree
        self._inorder(node.right)
```
- **Pre-order Traversal:** O(n)
```py
def preorder(self):
    self._preorder(self.root)
    print()

// Helper function for pre-order traversal (root, left, right)
def _preorder(self, node):
    if node:
        // Process the current node
        print(node.val, end=' ')
        // Recursively traverse the left subtree
        self._preorder(node.left)
        // Recursively traverse the right subtree
        self._preorder(node.right)
```
- **Post-order Traversal:** O(n)
```py
def postorder(self):
    self._postorder(self.root)
    print()

// Helper function for post-order traversal (left, right, root)
def _postorder(self, node):
    if node:
        // Recursively traverse the left subtree
        self._postorder(node.left)
        // Recursively traverse the right subtree
        self._postorder(node.right)
        // Process the current node
        print(node.val, end=' ')
```
- **Height of Tree:** O(n)
```py
 def height(self):
    return self._height(self.root)

// Helper function to calculate the height recursively
def _height(self, node):
    // Base case: If node is None, height is 0
    if not node:
        return 0
    // Recursively compute the height of left and right subtrees
    return max(self._height(node.left), self._height(node.right)) + 1
```
- **Search in BST**: O(logn)
```py
def search(self, val):
    return self._search(self.root, val)

// Helper function to search for a value recursively
def _search(self, node, val):
    // Base case: If node is None or value is found
    if not node:
        return False
    if node.val == val:
        return True
    // If value is less than node, search left subtree
    elif val < node.val:
        return self._search(node.left, val)
    // If value is greater, search right subtree
    else:
        return self._search(node.right, val)
```
- **Delete Node in BST:** O(logn)
```py
// Function to delete a node from a Binary Search Tree (BST)
def delete(self, val):
    self.root = self._delete(self.root, val)

// Helper function to delete a value recursively
def _delete(self, node, val):
    // Base case: If node is None
    if not node:
        return node
    
    // If value is less than node, recurse on left subtree
    if val < node.val:
        node.left = self._delete(node.left, val)
    // If value is greater, recurse on right subtree
    elif val > node.val:
        node.right = self._delete(node.right, val)
    else:
        // Node with the value found
        // Case 1: No left child
        if not node.left:
            return node.right
        // Case 2: No right child
        elif not node.right:
            return node.left
        
        // Case 3: Node with two children
        // Find the inorder successor (smallest node in right subtree)
        temp = self._min_value_node(node.right)
        // Copy the inorder successor's value
        node.val = temp.val
        // Delete the inorder successor
        node.right = self._delete(node.right, temp.val)
    
    // Return the modified node
    return node

// Helper function to find the node with the smallest value
def _min_value_node(self, node):
    // Traverse to the leftmost leaf
    current = node
    while current.left:
        current = current.left
    // Return the node with the smallest value
    return current

def minVal(self):
    return self._min_value_node(self, root)
```

---

