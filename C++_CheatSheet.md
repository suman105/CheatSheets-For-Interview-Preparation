# C++ Cheat Sheet 
## 1. Basics

### 1.1 Install C++
Download from [C++](https:#isocpp.org/get-started) and verify installation:
```cpp
g++ --version
```
### 1.2 Variables & Data Types
```cpp
int x = 10;         // Integer
float y = 3.14f;    // Float
double z = 3.1415;  // Double
char c = 'A';       // Char
bool flag = true;   // Boolean
string str = "Hello"; // String (using <string> header)
```

### 1.3 Conditional Statements
```cpp
if (x > 5) {
    // code to execute
} else if (x == 5) {
    // code to execute
} else {
    // code to execute
}
```

### 1.4 Loops
```cpp
// Basic for loop
for (int i = 0; i < n; ++i) {
    // code to execute
}

// For loop with multiple variables
for (int i = 0, j = n - 1; i < j; ++i, --j) {
    // code to execute
}

// Range-based for loop (C++11 and above)
for (const auto& elem : container) {
    // code to execute
}

// While loop
int n = 0;
while (n < 5) {
    // code to execute
}

// do while loop
do {
    // code to execute
} while (condition);
```

### 1.5 String, Char, Integer Conversion
```cpp
// Convert int to string
to_string(num);
// Convert string to int
stoi(s);
// Convert char to string
string(1, ch);
// Convert char array to string
string(charArr);
```

## 2. Functions
### 2.1 Function Without Parameters
```cpp
void greet() {
    cout << "Hello, world!" << endl;
}

greet();  // Output: Hello, world!
```
### 2.2 Function With Parameters
```cpp
void greet(string name) {
    cout << "Hello, " << name << "!" << endl;
}

greet("Shreyas");  // Output: Hello, Shreyas!
```
### 2.3 Function With Return Value
```cpp
int add(int a, int b) {
    return a + b;
}

int result = add(5, 3);  // Output: 8
cout << result << endl;
```
### 2.4 Function With Default Parameters
```cpp
void greet(string name = "Guest") {
    cout << "Hello, " << name << "!" << endl;
}

greet();           // Output: Hello, Guest!
greet("Shreyas");  // Output: Hello, Shreyas!
```
### 2.5 Lambda Functions
```cpp
auto square = [](int x) { return x * x; };
cout << square(5) << endl;  // Output: 25

auto add = [](int x, int y) { return x + y; };
cout << add(3, 4) << endl;  // Output: 7
```
### 2.6 Function With Multiple Parameters
```cpp
int add(int a, int b, int c) {
    return a + b + c;
}

cout << add(1, 2, 3) << endl;  // Output: 6
```

## 3. Data Structures
## 3.1 Arrays (Fixed Size)
### 3.1.1 Definition and Initialization
```cpp
#include <array>
#include <algorithm>  // For algorithms like sort, reverse, etc.

// C-style array initialization
int arr[5] = {1, 2, 3, 4, 5};

// std::array initialization (fixed-size array)
std::array<int, 5> arr_std = {1, 2, 3, 4, 5};

// Default initialization with std::array (all elements set to 0)
std::array<int, 10> arr_default = {0};
```

### 3.1.2 Modifying Elements
```cpp
arr_std[2] = 99;  // Set the 3rd element to 99
```

### 3.1.3 Sorting and Reversing
```cpp
std::reverse(arr_std.begin(), arr_std.end());   // Reverse the array
std::sort(arr_std.begin(), arr_std.end());  // Sort the array
```

### 3.1.4 Filling and Generating Sequences
```cpp
std::fill(arr_std.begin(), arr_std.end(), 10); // Fill all elements with 10
std::iota(arr_std.begin(), arr_std.end(), 1); // Fill with values 1, 2, 3, 4, 5
```


## 3.2 Strings

#### 3.2.1 Definition and Initialization
```cpp
// Initializing a string
std::string str = "1234";
std::string repeated_str(5, 'A');  // 5 occurrences of 'A'
```

#### 3.2.2 String Size and Substring Operations
```cpp
// Get string length
int len = str.size();  // Length of the string

// Extracting a substring
std::string sub = str.substr(start, length);  // Extracts substring from start, length
```

#### 3.2.3 Modifying Strings
```cpp
// Appending to a string
str.append("abc");  // Append "abc" to str

// Inserting into a string
str.insert(2, "sz");  // Insert "sz" at position 2

// Replacing part of the string
str.replace(pos, len_to_replace, "newStr"); // Replace part of the string starting from pos with "newStr"

// Erasing a portion of the string
str.erase(pos, len_to_replace);  // Remove characters from pos of length len_to_replace
```

#### 3.2.4 Searching in Strings
```cpp
// Find a substring within the string
size_t found = str.find("abc");
if (found != std::string::npos) {
    // "abc" found at index `found`
}

// Find the first occurrence of a character
size_t char_pos = str.find_first_of("z");

// Find the last occurrence of a character
size_t last_char_pos = str.find_last_of("z");
```

#### 3.2.5 String Comparisons and Checks
```cpp
// Compare strings
if (str.compare(str2) == 0) {
    // Strings are equal
}

// Clear the string
str.clear();

// Check if the string is empty
if (str.empty()) {
    // String is empty
}
```

#### 3.2.6 String Transformations
```cpp
// Reverse the string
std::reverse(str.begin(), str.end());

// Convert to uppercase
std::transform(str.begin(), str.end(), str.begin(), ::toupper);

// Convert to lowercase
std::transform(str.begin(), str.end(), str.begin(), ::tolower);
```

#### 3.2.7 Splitting a String by Delimiter
```cpp
// Split string by space (' ')
std::string data = "apple orange banana";
size_t pos_start = 0, pos_end;
while ((pos_end = data.find(' ', pos_start)) != std::string::npos) {
    std::cout << "Split part: " << data.substr(pos_start, pos_end - pos_start) << std::endl;
    pos_start = pos_end + 1;
}
std::cout << "Last part: " << data.substr(pos_start) << std::endl;  // Output: banana
```


## 3.3 Vectors

### 3.3.1 Definition and Initialization
```cpp
#include <vector>
using namespace std;

// Creating an empty vector
vector<int> v;

// Creating a vector with a specified size (default-initialized to 0)
vector<int> v(5);

// Creating a vector of size 5, initialized to 10
vector<int> v(5, 10);

// Initializing a vector with specific values
vector<int> v = {1, 2, 3, 4};

// Copy constructor (creates a vector from another vector)
vector<int> v(v2);

// Creating a vector from an array range
vector<int> v(arr + start, arr + end);

// Creating a vector from another vector range
vector<int> v(v2.begin(), v2.end());

// Move constructor (transfers ownership of `v2` to `v`)
vector<int> v = move(v2);

// Creating a 2D vector with N rows and no initialized columns
vector<vector<int>> v(N);

// Creating a 2D vector of size NxM, initialized to 0
vector<vector<int>> v(N, vector<int>(M, 0));
```

### 3.3.2 Insertion and Deletion
```cpp
// Adding elements to the end
v.push_back(e);

// Removing the last element
v.pop_back();

// Removing all elements
v.clear();

// Inserting an element at a specific position
v.insert(v.begin(), var);  // Inserts `var` at the beginning

// Erasing an element at a specific index
v.erase(v.begin() + 5);  // Erases the element at index 5

// Resizing the vector
v.resize(new_size);
```

### 3.3.3 Accessing Elements
```cpp
// Getting the first and last element
int first = v.front();
int last = v.back();
```

### 3.3.4 Sorting and Searching
```cpp
#include <algorithm>

// Sorting in ascending order
sort(v.begin(), v.end());

// Sorting in descending order
sort(v.begin(), v.end(), greater<int>());

// Reversing elements
reverse(v.begin(), v.end());

// Finding an element in the vector
auto it = find(v.begin(), v.end(), 5);

// Counting occurrences of an element
int count = count(v.begin(), v.end(), 5);

// Summing up all elements
#include <numeric>
int sum = accumulate(v.begin(), v.end(), 0);

// Transforming elements (multiplying all elements by 2)
transform(v.begin(), v.end(), v.begin(), [](int x) { return x * 2; });
```

### 3.3.5 Removing Duplicates
```cpp
// Removing consecutive duplicates
auto it = unique(v.begin(), v.end());
v.resize(distance(v.begin(), it));  // Resize vector to new size
```

### 3.3.6 Binary Search and Bounds
```cpp
// Lower bound: First element >= value
auto it_lower = lower_bound(v.begin(), v.end(), 5);

// Upper bound: First element > value
auto it_upper = upper_bound(v.begin(), v.end(), 5);

// Binary search (checks if element exists)
bool found = binary_search(v.begin(), v.end(), 5);
```

### 3.3.7 Finding Min/Max Elements
```cpp
// Maximum and minimum element
int max_val = *max_element(v.begin(), v.end());
int min_val = *min_element(v.begin(), v.end());

// Finding both min and max
auto result = minmax_element(v.begin(), v.end());
cout << "Min: " << *result.first << ", Max: " << *result.second << endl;
```

### 3.3.8 Checking Conditions on Elements
```cpp
// Checking if all elements are positive
bool all_positive = all_of(v.begin(), v.end(), [](int x) { return x > 0; });

// Checking if any element is negative
bool any_negative = any_of(v.begin(), v.end(), [](int x) { return x < 0; });

// Checking if no elements are negative
bool none_negative = none_of(v.begin(), v.end(), [](int x) { return x < 0; });
```

### 3.3.9 Iterating Over a Vector
```cpp
// Using range-based for loop
for (const auto& elem : v) {
    cout << elem << " ";
}
cout << endl;

// Using index-based iteration
for (size_t i = 0; i < v.size(); i++) {
    cout << v[i] << " ";
}
cout << endl;

// Using iterators
for (auto it = v.begin(); it != v.end(); ++it) {
    cout << *it << " ";
}
cout << endl;

// Reverse iteration
for (auto it = v.rbegin(); it != v.rend(); ++it) {
    cout << *it << " ";
}
cout << endl;
```

### 3.3.10 Modifying Elements
```cpp
// Incrementing every element by 1
for_each(v.begin(), v.end(), [](int& x) { x += 1; });
```


### 3.4 Maps

#### 3.4.1 Definition and Initialization
```cpp
// Ordered Map (`map`)
#include <map>
std::map<int, std::string> treeMap;  // Empty ordered map
std::map<int, std::string> treeMap = {{1, "one"}, {2, "two"}, {3, "three"}};  // Initialized map

// Unordered Map (`unordered_map`)
#include <unordered_map>
std::unordered_map<int, std::string> hashMap;  // Empty unordered map
std::unordered_map<int, std::string> hashMap = {{1, "one"}, {2, "two"}, {3, "three"}};  // Initialized unordered map
```

#### 3.4.2 Insertion Methods
```cpp
// Using Bracket Notation
treeMap[1] = "one";  // Inserts key=1, value="one"
treeMap[2] = "two";  // Inserts key=2, value="two"

// Using `.insert()`
treeMap.insert({3, "three"});  // Insert key=3, value="three"
treeMap.insert(std::make_pair(4, "four"));  // Using make_pair
treeMap.insert(std::pair<int, std::string>(5, "five"));  // Explicit pair

// Using `.emplace()` (Avoids Copy Overhead)
treeMap.emplace(6, "six");  // Faster than insert
```

#### 3.4.3 Accessing Elements
```cpp
// Using Bracket Notation (`operator[]`)
std::string val = treeMap[1];  // Returns "one"

// Using `.at()`
std::cout << treeMap.at(1) << std::endl;  // Access existing element safely

// Checking if a Key Exists
if (treeMap.find(3) != treeMap.end()) 
{
    // Element found
}
```

#### 3.4.4 Deletion Methods
```cpp
// Remove an Element by Key
treeMap.erase(2);  // Removes key=2

// Using Iterator to Erase
auto it = treeMap.find(3);
if (it != treeMap.end()) {
    treeMap.erase(it);
}

// Remove All Elements 
treeMap.clear();  // Empties the map 

// Checking Size and Emptiness
std::cout << "Size: " << treeMap.size() << std::endl;  // Number of elements
if (treeMap.empty()) {
    std::cout << "Map is empty!" << std::endl;
}
```

#### 3.4.5 Iterating Over a Map
```cpp
// Using a `for` Loop (Key-Value Pairs)
for (const auto& pair : treeMap) {
    std::cout << pair.first << " -> " << pair.second << std::endl;
}

// Using an Iterator
for (auto it = treeMap.begin(); it != treeMap.end(); ++it) {
    std::cout << it->first << " -> " << it->second << std::endl;
}

// Reverse Iteration
for (auto it = treeMap.rbegin(); it != treeMap.rend(); ++it) {
    std::cout << it->first << " -> " << it->second << std::endl;
}
```

#### 3.4.6 Finding Elements
```cpp
// Check If a Key Exists
if (treeMap.find(4) != treeMap.end()) {
    std::cout << "Key 4 exists." << std::endl;
}

// Find the First Element Greater or Equal (`lower_bound`)
auto it = treeMap.lower_bound(3);  // Smallest key ≥ 3
if (it != treeMap.end()) {
    std::cout << "Lower bound: " << it->first << " -> " << it->second << std::endl;
}

// Find the First Element Strictly Greater (`upper_bound`)
auto it = treeMap.upper_bound(3);  // Smallest key > 3
if (it != treeMap.end()) {
    std::cout << "Upper bound: " << it->first << " -> " << it->second << std::endl;
}
```

#### 3.4.7 Using `multimap` and `unordered_multimap`
```cpp
// MultiMap (Allows Duplicate Keys)
#include <map>
std::multimap<int, std::string> multiMap;
multiMap.insert({1, "one"});
multiMap.insert({1, "uno"});
multiMap.insert({2, "two"});

// Unordered MultiMap
#include <unordered_map>
std::unordered_multimap<int, std::string> umultiMap;
umultiMap.insert({1, "one"});
umultiMap.insert({1, "uno"});
umultiMap.insert({2, "two"});
```

## 3.5 Sets
### 3.5.1 Definition and Initialization
```cpp
// Ordered Set (`std::set`)
#include <set>
std::set<int> orderedSet;  // Empty ordered set
std::set<int> orderedSet = {1, 2, 3, 4, 5};  // Initialization with values

// Unordered Set (`std::unordered_set`)
#include <unordered_set>
std::unordered_set<int> unorderedSet;  // Empty unordered set
std::unordered_set<int> unorderedSet = {1, 2, 3, 4, 5};  // Initialization

// Multiset (`std::multiset`) - Allows Duplicate Elements
#include <set>
std::multiset<int> multiSet;  // Empty multiset
std::multiset<int> multiSet = {1, 1, 2, 2, 3};  // Allows duplicates

// Unordered Multiset (`std::unordered_multiset`)
#include <unordered_set>
std::unordered_multiset<int> unorderedMultiSet = {1, 1, 2, 2, 3};  // Allows duplicates
```

### 3.5.2 Inserting Elements
```cpp
// Insert Single Element
orderedSet.insert(10);
unorderedSet.insert(10);

// Insert Multiple Elements (Initializer List)
orderedSet.insert({20, 30, 40});
unorderedSet.insert({20, 30, 40});

// Using `.emplace()` (Avoids Copy Overhead)
orderedSet.emplace(50);
unorderedSet.emplace(50);
```

### 3.5.3 Deleting Elements
```cpp
// Remove a Specific Element
orderedSet.erase(20);  // Removes element with value 20
unorderedSet.erase(30);

// Erase Using Iterator
auto it = orderedSet.find(10);
if (it != orderedSet.end()) {
    orderedSet.erase(it);
}

// Erase a Range of Elements
orderedSet.erase(orderedSet.begin(), orderedSet.end());  // Clears the entire set

// Clear All Elements
orderedSet.clear();
unorderedSet.clear();
```

### 3.5.4 Checking Size and Emptiness
```cpp
cout << "Size: " << orderedSet.size() << endl;
if (orderedSet.empty()) {
    cout << "Set is empty!" << endl;
}
```

### 3.5.5 Searching for Elements
```cpp
// Check If an Element Exists
if (orderedSet.find(10) != orderedSet.end()) {
    cout << "10 exists in the set" << endl;
}

// Count Occurrences (Useful for `multiset`)
cout << "Count of 1 in multiset: " << multiSet.count(1) << endl;
```

### 3.5.6 Iterating Over a Set
```cpp
// Using a `for` Loop
for (const auto& elem : orderedSet) {
    std::cout << elem << " ";
}

// Using Iterators
for (auto it = orderedSet.begin(); it != orderedSet.end(); ++it) {
    std::cout << *it << " ";
}

// Reverse Iteration
for (auto it = orderedSet.rbegin(); it != orderedSet.rend(); ++it) {
    std::cout << *it << " ";
}
```

### 3.5.7 Lower and Upper Bound (Only for `std::set`)
```cpp
// Find the First Element Greater or Equal (`lower_bound`)
auto it = orderedSet.lower_bound(3);
if (it != orderedSet.end()) {
    std::cout << "Lower bound: " << *it << std::endl;
}

// Find the First Element Strictly Greater (`upper_bound`)
auto it = orderedSet.upper_bound(3);
if (it != orderedSet.end()) {
    std::cout << "Upper bound: " << *it << std::endl;
}
```

### 3.5.9 Using `std::multiset` and `std::unordered_multiset`
```cpp
// MultiSet (Allows Duplicate Elements)
std::multiset<int> multiSet = {1, 1, 2, 2, 3};  // Allows duplicates
multiSet.insert(2);  // Insert another 2
cout << "Count of 2: " << multiSet.count(2) << endl;

// Unordered MultiSet
std::unordered_multiset<int> unorderedMultiSet = {1, 1, 2, 2, 3};  // Allows duplicates
```

## 3.6  Lists
### 3.6.1  Definition and Initialization
```cpp
// Basic List Declaration
#include <list>
list<int> myList;  // Empty list

// Initialize with Values
#include <unordered_set>
list<int> myList = {1, 2, 3, 4, 5};  // List with initial values

// Initialize with a Fixed Size and Default Value
list<int> myList(5, 10);  // List of size 5, all elements initialized to 10

// Copy Constructor
list<int> newList(myList);  // Copy existing list

// Move Constructor
list<int> movedList(move(myList));  // Move elements from another list
```

### 3.6.2  Inserting Elements
```cpp
// Push Elements at the Front and Back
myList.push_back(10);  // Add element to the end
myList.push_front(5);  // Add element to the beginning

// Insert at a Specific Position
auto it = myList.begin();
std::advance(it, 2);  // Move iterator to the 3rd position (0-based index)
myList.insert(it, 99);  // Insert 99 at the 3rd position

// Insert Multiple Elements
myList.insert(it, 3, 20);  // Insert three 20s at the specified position

// Insert from Another List
std::list<int> anotherList = {50, 60};
myList.insert(it, anotherList.begin(), anotherList.end());  // Insert another list's elements

// Emplace (Avoids Copy Overhead)
myList.emplace(myList.begin(), 42);  // Efficiently inserts 42 at the beginning

```

### 3.6.3 Deleting Elements
```cpp
//  Remove Specific Element
myList.remove(99);  // Removes all occurrences of 99

// Erase an Element by Position
auto it = myList.begin();
std::advance(it, 2);  // Move iterator to the 3rd element
myList.erase(it);  // Remove element at that position

// Erase a Range of Elements
auto start = myList.begin();
auto end = myList.begin();
std::advance(end, 3);  // Move end iterator to the 4th element
myList.erase(start, end);  // Remove elements from 1st to 3rd position

// Pop Elements from Front and Back
myList.pop_front();  // Removes first element
myList.pop_back();   // Removes last element

// Clear the List
myList.clear();  // Removes all elements
```

### 3.6.6 Checking Size and Emptiness
```cpp
cout << "Size: " << myList.size() << endl;
if (myList.empty()) {
    cout << "List is empty!" << endl;
}
```

### 3.6.7 Accessing Elements
```cpp
cout << "First: " << myList.front() << endl;
cout << "Last: " << myList.back() << endl;
```

### 3.6.8  Searching for Elements
```cpp
#include <algorithm>
auto it = std::find(myList.begin(), myList.end(), 42);
if (it != myList.end()) {
    std::cout << "Element found: " << *it << std::endl;
}
```

### 3.6.8 Iterating Over a List
```cpp
// Using a `for` Loop
for (const auto& elem : myList) 
{
    std::cout << elem << " ";
}

// Using Iterators
for (auto it = myList.begin(); it != myList.end(); ++it) {
    std::cout << *it << " ";
}

// Reverse Iteration
for (auto it = myList.rbegin(); it != myList.rend(); ++it) {
    std::cout << *it << " ";
}
```

### 3.6.9 Sorting and Reversing
```cpp
// Sorting a List
myList.sort();  // Sorts in ascending order

// Sorting with a Custom Comparator
myList.sort([](int a, int b) { return a > b; });  // Sorts in descending order

// Reversing a List
myList.reverse();
```

### 3.6.10 Merging and Splicing
```cpp
// Merging Two Sorted Lists
std::list<int> list1 = {1, 3, 5};
std::list<int> list2 = {2, 4, 6};
list1.merge(list2);  // Merges list2 into list1

// Splicing (Move Elements from One List to Another)
std::list<int> source = {7, 8, 9};
std::list<int> destination = {1, 2, 3};

// Move all elements from source to destination
destination.splice(destination.end(), source);
```

### 3.6.11 Removing Duplicates
```cpp
myList.unique();  // Removes consecutive duplicate elements
```

## 3.7 Queue
#### 3.7.1 Definition and Initialization
```cpp
#include <queue>
queue<int> myQueue;  // Empty queue
queue<int> myQueue({1, 2, 3, 4, 5});  // C++17 and later (optional)
queue<int> queueCopy(myQueue);  // Copy an existing queue
queue<int> movedQueue(move(myQueue));  // Move contents of an existing queue
```

#### 3.7.2 Basic Operations
```cpp
myQueue.push(10);  // Insert element at the back
myQueue.pop();  // Removes the front element

cout << "Front: " << myQueue.front() << endl;
cout << "Back: " << myQueue.back() << endl;

myQueue.size() // Calculate the Size
myQueue.empty() // Returns True if it is Empty
```

#### 3.7.3 Iterating Over a Queue
```cpp
std::queue<int> tempQueue = myQueue;  // Create a copy to avoid modifying original queue

while (!tempQueue.empty()) {
    std::cout << tempQueue.front() << " ";
    tempQueue.pop();  // Remove the processed element
}
```
#### 3.7.4 Priority Queue (`std::priority_queue`) & Deque
```cpp
// Max-Heap Priority Queue (By Default)
priority_queue<int> pq;
pq.push(3);
pq.push(5);
pq.push(1);

cout << pq.top() << endl;  // Output: 5 (largest element)
pq.pop();  // Removes 5

// Min-Heap Priority Queue
priority_queue<int, vector<int>, greater<int>> minHeap;
minHeap.push(3);
minHeap.push(5);
minHeap.push(1);

cout << minHeap.top() << endl;  // Output: 1 (smallest element)

// A queue that supports efficient insertions and deletions from both ends.
deque<int> dq = {1, 2, 3};
queue<int, deque<int>> dequeQueue(dq);
```

## 3.8 Stacks
### 3.8.1 Definition and Initialization
```cpp
#include <stack>
stack<int> myStack;  // Empty stack
stack<int> myStack({1, 2, 3, 4, 5});  // Not standard in all compilers
stack<int> stackCopy(myStack);  // Copy constructor
stack<int> movedStack(move(myStack));  // Move contents
```

### 3.8.2 Basic Operations
```cpp
myStack.push(10);
myStack.pop();  // Removes the top element
cout << "Top: " << myStack.top() << endl;
myStack.size()  // Calculates the size 
myStack.empty() // Check whether the stack is Empty ot not
```

### 3.8.3 Iterating Over a Stack
```cpp
stack<int> tempStack = myStack;  // Create a copy to avoid modifying original stack

while (!tempStack.empty()) {
    cout << tempStack.top() << " ";
    tempStack.pop();  # Remove the processed element
}
```

## 5. Object-Oriented Programming (OOP)
- Classes define the blueprint for objects, and objects are instances of a class.
### 5.1 Classes and Objects
```cpp
class Person {
public:
    std::string name;
    int age;

    Person(std::string n, int a) : name(n), age(a) {}
    
    void greet() {
        std::cout << "Hello, my name is " << name << "!" << std::endl;
    }
};

Person p("Shreyas", 25);
p.greet();
```
### 5.2 Encapsulation (Restricts Direct Access to Data)
- Encapsulation hides the internal state and only allows access through public methods.
```cpp
#include <iostream>
using namespace std;

class BankAccount {
private:
    double balance;  // Private data member

public:
    // Constructor to initialize balance
    BankAccount(double initialBalance) {
        balance = (initialBalance >= 0) ? initialBalance : 0;
    }

    // Public methods to interact with private data
    void deposit(double amount) { balance += amount; }
    void withdraw(double amount) { if (amount <= balance) balance -= amount; }
    double getBalance() { return balance; }
};

int main() {
    BankAccount account(1000);
    account.deposit(500);
    account.withdraw(300);
    cout << "Balance: $" << account.getBalance() << endl;  // Output: Balance: $1200
    return 0;
}
```
### 5.3 Inheritance (Allows Code Reuse Between Classes)
- Inheritance allows a class to inherit properties and methods from another class.
```cpp
#include <iostream>
using namespace std;

// Base class (Parent)
class Animal {
public:
    void eat() {
        cout << "This animal eats food." << endl;
    }
};

# Derived class (Child)
class Dog : public Animal {
public:
    void bark() {
        cout << "The dog barks!" << endl;
    }
};

int main() {
    Dog myDog;
    myDog.eat();  # Inherited from Animal class
    myDog.bark(); # Defined in Dog class
    return 0;
}

```
### 5.4 Polymorphism (Same Interface, Different Implementation)
- #### 5.4.1 Example of Function Overloading (Compile-time Polymorphism):
```cpp
#include <iostream>
using namespace std;

class Math {
public:
    // Function Overloading: Same function name, different parameters
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
};

int main() {
    Math obj;
    cout << obj.add(5, 3) << endl;     // Output: 8
    cout << obj.add(2.5, 1.5) << endl; // Output: 4.0
    return 0;
}
```

- #### 5.4.2 Example of Function Overriding (Run-time Polymorphism):
```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void makeSound() { cout << "Animal makes a sound" << endl; }
};

class Dog : public Animal {
public:
    void makeSound() override { cout << "Dog barks" << endl; }
};

int main() {
    Animal* animal = new Dog();
    animal->makeSound();  // Output: Dog barks (Polymorphism at runtime)
    delete animal;
    return 0;
}
```

### 5.5 Abstraction (Hides Implementation Details)
- Abstraction allows you to define methods that must be implemented in derived classes, while hiding the details of the implementation.
```cpp
#include <iostream>
using namespace std;

// Abstract class (interface)
class Shape {
public:
    virtual void draw() = 0;  // Pure virtual function
};

class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Circle" << endl;
    }
};

class Rectangle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Rectangle" << endl;
    }
};

int main() {
    Shape* shape1 = new Circle();
    Shape* shape2 = new Rectangle();

    shape1->draw();  // Output: Drawing a Circle
    shape2->draw();  // Output: Drawing a Rectangle

    delete shape1;
    delete shape2;
    return 0;
}
```

### 5.6 Constructor
```cpp
#include <iostream>
using namespace std;

class Car {
private:
    string brand;
    int speed;

public:
    // Constructor
    Car(string b, int s) {
        brand = b;
        speed = s;
        cout << "Car object created!" << endl;
    }

    void display() {
        cout << "Brand: " << brand << ", Speed: " << speed << " km/h" << endl;
    }
};

int main() {
    Car myCar("Toyota", 120);  # Constructor is automatically called
    myCar.display();  
    return 0;
}
```

### 5.7 Destructor
```cpp
#include <iostream>
using namespace std;

class Car {
public:
    Car() { cout << "Car is created!" << endl; }
    
    ~Car() { cout << "Car is destroyed!" << endl; }
};

int main() {
    Car myCar;  // Constructor is called automatically
    return 0;   // Destructor is called automatically when object goes out of scope
}

``` 
