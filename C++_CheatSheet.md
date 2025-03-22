# C++ Cheat Sheet

## 1. Basics

### 1.1 Install C++
Download from [C++](https:#isocpp.org/get-started) and verify installation:
```sh
g++ --version
```
### 1.2 Variables & Data Types
```sh
int x = 10;         # Integer
float y = 3.14f;    # Float
double z = 3.1415;  # Double
char c = 'A';       # Char
bool flag = true;   # Boolean
string str = "Hello"; # String (using <string> header)
```

### 1.3 Conditional Statements
```sh
if (x > 5) {
    # code to execute
} else if (x == 5) {
    # code to execute
} else {
    # code to execute
}
```

### 1.4 Loops
```sh
# Basic for loop
for (int i = 0; i < n; ++i) {
    # code to execute
}

# For loop with multiple variables
for (int i = 0, j = n - 1; i < j; ++i, --j) {
    # code to execute
}

# Range-based for loop (C++11 and above)
for (const auto& elem : container) {
    # code to execute
}

# While loop
int n = 0;
while (n < 5) {
    # code to execute
}

# do while loop
do {
    # code to execute
} while (condition);
```

### 1.5 String, Char, Integer Conversion
```sh
# Convert int to string
to_string(num);
# Convert string to int
stoi(s);
# Convert char to string
string(1, ch);
# Convert char array to string
string(charArr);
```

## 2. Functions
### 2.1 Function Without Parameters
```sh
void greet() {
    cout << "Hello, world!" << endl;
}

greet();  # Output: Hello, world!
```
### 2.2 Function With Parameters
```sh
void greet(string name) {
    cout << "Hello, " << name << "!" << endl;
}

greet("Shreyas");  # Output: Hello, Shreyas!
```
### 2.3 Function With Return Value
```sh
int add(int a, int b) {
    return a + b;
}

int result = add(5, 3);  # Output: 8
cout << result << endl;
```
### 2.4 Function With Default Parameters
```sh
void greet(string name = "Guest") {
    cout << "Hello, " << name << "!" << endl;
}

greet();           # Output: Hello, Guest!
greet("Shreyas");  # Output: Hello, Shreyas!
```
### 2.5 Lambda Functions
```sh
auto square = [](int x) { return x * x; };
cout << square(5) << endl;  # Output: 25

auto add = [](int x, int y) { return x + y; };
cout << add(3, 4) << endl;  # Output: 7
```
### 2.6 Function With Multiple Parameters
```sh
int add(int a, int b, int c) {
    return a + b + c;
}

cout << add(1, 2, 3) << endl;  # Output: 6
```

## 3. Data Structures
### 3.1 Arrays (Fixed Size)
```sh
#include <array>
#include <algorithm>  # For algorithms like sort, reverse, etc.

# C-style array initialization
int arr[5] = {1, 2, 3, 4, 5};

# array initialization (fixed size array)
array<int, 5> arr_std = {1, 2, 3, 4, 5};

# Default initialization with std::array (all elements set to 0)
std::array<int, 10> arr_default = {0}; 

# Modifying elements of std::array
arr[2] = 99;  #Set the 3rd element to 99

reverse(begin(arr), end(arr));   # reverse the array
sort(arr_sort.begin(), arr_sort.end());  # Sort the array
fill(arr_sort.begin(), arr_sort.end(), 10); # fill all elements with 10
iota(arr_range.begin(), arr_range.end(), 1); # Fill with values 1, 2, 3, 4, 5
```
### 3.2 Strings
```sh
# Initial string
string str = "1234";

int len = str.size();  # Length of the string
string sub = str.substr(start, length);  # Extracts substring from start, length
str.append("abc");  # Append to string
str.insert(2, "sz");    # Insert into string at position 2
str.replace(pos, len_to_replace, "newStr"); # Replace part of the string starting from position 3 with a new string
str.erase(pos, len_to_replace); # Erase a portion of the string (starting from pos, length `len_to_replace`)

# Search for substring in the string
size_t found = str.find("abc");
if (found != std::string::npos) 
{
    # present at index `found`
}

reverse(str.begin(), str.end());    # Reverse the string
str.compare(str2) == 0 # Equal
str.clear(); # Clear the string
str.empty(); # Check the string is empty or not
size_t char_pos = str.find_first_of("z"); # Find the first occurrence of a character
size_t last_char_pos = str.find_last_of("z"); # Find the last occurrence of a character
transform(str.begin(), str.end(), str.begin(), toupper); #Convert to uppercase
transform(str.begin(), str.end(), str.begin(), tolower); # Convert to lowercase
string repeated_str(5, 'A');  # 5 occurrences of 'A'

# String split (split by delimiter ' ')
std::string data = "apple orange banana";
size_t pos_start = 0, pos_end;
while ((pos_end = data.find(' ', pos_start)) != std::string::npos) {
    std::cout << "Split part: " << data.substr(pos_start, pos_end - pos_start) << std::endl;
    pos_start = pos_end + 1;
}
std::cout << "Last part: " << data.substr(pos_start) << std::endl;  # Output: banana

```
### 3.3 Vector
```sh
vector<int> v;  # Creates an empty vector of integers
vector<int> v(5);  # Creates a vector of size 5, with all elements initialized to 0
vector<int> v(5, 10);  # Creates a vector of size 5, with all elements initialized to 10

vector<int> v = {1, 2, 3, 4};  # Initializes vector with values 1, 2, 3, 4
vector<int> v(v2);  # Copy constructor, initializes with another vector `v2`

vector<int> v(arr + start, arr + end);  # Initializes vector `v` with a range from array `arr` between start and end indices
vector<int> v(v2.begin(), v2.end());  # Copies elements from another vector `v2`
vector<int> v{1, 2, 3, 4};  # Initializes vector with values 1, 2, 3, 4
vector<vector<int>> v(N);  # Creates a 2D vector with `N` rows and no initialized columns
vector<vector<int>> v(N, vector<int>(M, 0));  # Creates a 2D vector of size NxM, initialized to 0
vector<int> v = {1, 2, 3, 4};  # Creates a vector and initializes it with values 1, 2, 3, 4
vector<int> v = move(v2);  # Move constructor, transfers ownership of `v2` to `v`

v.push_back(e);  # Add element `e` at the end of the vector.
v.pop_back();    # Remove the last element.
v.clear();       # Remove all elements from the vector.
v.insert(v.begin(), var);  # Insert element `var` at the beginning.
v.erase(v.begin() + 5);    # Erase the element at index 5 (6th element).
v.resize(new_size);        # Resize the vector to the specified size.
v.front();      # Get the first element of the vector.
v.back();       # Get the last element of the vector.

sort(v.begin(), v.end());  # Sort the vector in ascending order.
sort(v.begin(), v.end(), greater<int>());  # Sort in descending order using a custom comparator
reverse(v.begin(), v.end());  # Reverse the elements in the vector
auto it = find(v.begin(), v.end(), 5);  # Find the element 5 in the vector
int count = count(v.begin(), v.end(), 5);  # Count how many times the element 5 appears in the vector 
int sum = accumulate(v.begin(), v.end(), 0);  # Sum of all elements, starting from 0
transform(v.begin(), v.end(), v.begin(), [](int x) { return x * 2; });  # Multiply all elements by 2

#Unique (Remove Duplicates)
auto it = unique(v.begin(), v.end());  # Removes consecutive duplicates
v.resize(distance(v.begin(), it));  # Resize vector to new size

# Lower Bound / Upper Bound (Binary Search)
auto it_lower = std::lower_bound(v.begin(), v.end(), 5);  # Find the first position where 5 could be inserted
auto it_upper = std::upper_bound(v.begin(), v.end(), 5);  # Find the position just after all occurrences of 5

bool found = std::binary_search(v.begin(), v.end(), 5);  # Check if 5 exists in the sorted vector
int max_val = *std::max_element(v.begin(), v.end());  # Find the maximum element in the vector
int min_val = *std::min_element(v.begin(), v.end());  # Find the minimum element in the vector

auto result = std::minmax_element(v.begin(), v.end());  # Find the min and max element
# "Min: " << *result.first << ", Max: " << *result.second

bool all_positive = std::all_of(v.begin(), v.end(), [](int x) { return x > 0; });  # Check if all elements are positive
bool any_negative = std::any_of(v.begin(), v.end(), [](int x) { return x < 0; });  # Check if any element is negative
bool none_negative = std::none_of(v.begin(), v.end(), [](int x) { return x < 0; });  # Check if no element is negative

for_each(v.begin(), v.end(), [](int& x) { x += 1; });  # Increment every element by 1
```
## 3.4 Maps

### 3.4.1 Definition and Initialization
#### Ordered Map (`map`)
```sh
#include <map>
map<int, string> treeMap;  # Empty ordered map
map<int, string> treeMap = {{1, "one"}, {2, "two"}, {3, "three"}};  # Initialized map
```

#### Unordered Map `(unordered_map`)
```sh
#include <unordered_map>
unordered_map<int, string> hashMap;  # Empty unordered map
unordered_map<int, string> hashMap = {{1, "one"}, {2, "two"}, {3, "three"}};  # Initialized unordered map
```

### 3.4.2 Insertion Methods
#### Using Bracket Notation
```sh
treeMap[1] = "one";  # Inserts key=1, value="one"
treeMap[2] = "two";  # Inserts key=2, value="two"
```

#### Using `.insert()`
```sh
treeMap.insert({3, "three"});  # Insert key=3, value="three"
treeMap.insert(make_pair(4, "four"));  # Using make_pair
treeMap.insert(pair<int, string>(5, "five"));  # Explicit pair
```
#### Using `.emplace()` (Avoids Copy Overhead)
```sh
treeMap.emplace(6, "six");  # Faster than insert
```

### 3.4.3 Accessing Elements
#### Using Bracket Notation (`operator[]`)
```sh
string val = treeMap[1];  # Returns "one"
```

#### Using `.at()`
```sh
cout << treeMap.at(1) << endl;  # Access existing element safely
```

#### Checking if a Key Exists
```sh
if (treeMap.find(3) != treeMap.end()) 
{
    # element found
}
```

### 3.4.4 Deletion Methods
#### Remove an Element by Key
```sh
treeMap.erase(2);  # Removes key=2
```
#### Using Iterator to Erase
```sh
auto it = treeMap.find(3);
if (it != treeMap.end()) {
    treeMap.erase(it);
}
```
#### Remove All Elements
```sh 
treeMap.clear();  # Empties the map 
```

#### Checking Size and Emptiness
```sh
cout << "Size: " << treeMap.size() << endl;  # Number of elements
if (treeMap.empty()) {
    cout << "Map is empty!" << endl;
}

```

### 3.4.5 Iterating Over a Map
#### Using a `for` Loop (Key-Value Pairs)
```sh
for (const auto& pair : treeMap) {
    cout << pair.first << " -> " << pair.second << endl;
}
```

#### Using an Iterator
```sh
for (auto it = treeMap.begin(); it != treeMap.end(); ++it) {
    cout << it->first << " -> " << it->second << endl;
}
```

#### Reverse Iteration
```sh
for (auto it = treeMap.rbegin(); it != treeMap.rend(); ++it) {
    cout << it->first << " -> " << it->second << endl;
}
```

### 3.4.6 Finding Elements
#### Check If a Key Exists
```sh
if (treeMap.find(4) != treeMap.end()) {
    std::cout << "Key 4 exists." << std::endl;
}
```
#### Find the First Element Greater or Equal (`lower_bound`)
```sh
auto it = treeMap.lower_bound(3);  # Smallest key ≥ 3
if (it != treeMap.end()) {
    std::cout << "Lower bound: " << it->first << " -> " << it->second << std::endl;
}
```
#### Find the First Element Strictly Greater (`upper_bound`)
```sh
auto it = treeMap.upper_bound(3);  # Smallest key > 3
if (it != treeMap.end()) {
    std::cout << "Upper bound: " << it->first << " -> " << it->second << std::endl;
}
```

### 3.4.7 Using `multimap` and `unordered_multimap`
#### MultiMap (Allows Duplicate Keys)
```sh
#include <map>
std::multimap<int, std::string> multiMap;
multiMap.insert({1, "one"});
multiMap.insert({1, "uno"});
multiMap.insert({2, "two"});
```
#### Unordered MultiMap
```sh
#include <unordered_map>
std::unordered_multimap<int, std::string> umultiMap;
umultiMap.insert({1, "one"});
umultiMap.insert({1, "uno"});
umultiMap.insert({2, "two"});
```

## 3.5  Sets
### 3.5.1  Definition and Initialization
#### Ordered Set (`std::set`)
```sh
#include <set>
std::set<int> orderedSet;  # Empty ordered set
std::set<int> orderedSet = {1, 2, 3, 4, 5};  # Initialization with values
```
#### Unordered Set (`std::unordered_set`)
```sh
#include <unordered_set>
std::unordered_set<int> unorderedSet;  # Empty unordered set
std::unordered_set<int> unorderedSet = {1, 2, 3, 4, 5};  # Initialization
```
#### Multiset (`std::multiset`) - Allows Duplicate Elements
```sh
#include <set>
std::multiset<int> multiSet;  # Empty multiset
std::multiset<int> multiSet = {1, 1, 2, 2, 3};  # Allows duplicates
```
#### Unordered Multiset (`std::unordered_multiset`)
```sh
#include <unordered_set>
std::unordered_multiset<int> unorderedMultiSet = {1, 1, 2, 2, 3};  # Allows duplicates
```

### 3.5.2  Inserting Elements
#### Insert Single Element
```sh
orderedSet.insert(10);
unorderedSet.insert(10);
```
#### Insert Multiple Elements (Initializer List)
```sh
orderedSet.insert({20, 30, 40});
unorderedSet.insert({20, 30, 40});
```
#### Using `.emplace()` (Avoids Copy Overhead)
```sh
orderedSet.emplace(50);
unorderedSet.emplace(50);
```

### 3.5.3 Deleting Elements
####  Remove a Specific Element
```sh
orderedSet.erase(20);  # Removes element with value 20
unorderedSet.erase(30);
```
#### Erase Using Iterator
```sh
auto it = orderedSet.find(10);
if (it != orderedSet.end()) {
    orderedSet.erase(it);
}
```
#### Erase a Range of Elements
```sh
orderedSet.erase(orderedSet.begin(), orderedSet.end());  # Clears the entire set
```
#### Clear All Elements
```sh
orderedSet.clear();
unorderedSet.clear();
```

### 3.5.6 Checking Size and Emptiness
```sh
cout << "Size: " << orderedSet.size() << endl;
if (orderedSet.empty()) {
    cout << "Set is empty!" << endl;
}
```

### 3.5.7 Searching for Elements
#### Check If an Element Exists
```sh
if (orderedSet.find(10) != orderedSet.end()) {
    cout << "10 exists in the set" << endl;
}
```
#### Count Occurrences (Useful for `multiset`)
```sh
cout << "Count of 1 in multiset: " << multiSet.count(1) << endl;
```

### 3.5.8  Iterating Over a Set
#### Using a `for` Loop
```sh
for (const auto& elem : orderedSet) {
    std::cout << elem << " ";
}
```
#### Using Iterators
```sh
for (auto it = orderedSet.begin(); it != orderedSet.end(); ++it) {
    std::cout << *it << " ";
}
```
#### Reverse Iteration
```sh
for (auto it = orderedSet.rbegin(); it != orderedSet.rend(); ++it) {
    std::cout << *it << " ";
}
```

### 3.5.8 Lower and Upper Bound (Only for `std::set)`
#### Find the First Element Greater or Equal (`lower_bound`)
```sh
auto it = orderedSet.lower_bound(3);
if (it != orderedSet.end()) {
    std::cout << "Lower bound: " << *it << std::endl;
}
```
#### Find the First Element Strictly Greater (`upper_bound`)
```sh
auto it = orderedSet.lower_bound(3);
if (it != orderedSet.end()) {
    std::cout << "Lower bound: " << *it << std::endl;
}
```

### 3.5.9 Using `std::multiset` and `std::unordered_multiset`
#### MultiSet (Allows Duplicate Elements)
```sh
std::multiset<int> multiSet = {1, 1, 2, 2, 3};  # Allows duplicates
multiSet.insert(2);  # Insert another 2
std::cout << "Count of 2: " << multiSet.count(2) << std::endl;
```
#### Unordered MultiSet
```sh
std::unordered_multiset<int> unorderedMultiSet = {1, 1, 2, 2, 3};  # Allows duplicates
```

## 3.6  Lists
### 3.6.1  Definition and Initialization
#### Basic List Declaration
```sh
#include <list>
list<int> myList;  # Empty list
```
#### Initialize with Values
```sh
#include <unordered_set>
list<int> myList = {1, 2, 3, 4, 5};  # List with initial values
```
#### Initialize with a Fixed Size and Default Value
```sh
list<int> myList(5, 10);  # List of size 5, all elements initialized to 10
```
#### Copy Constructor
```sh
list<int> newList(myList);  # Copy existing list
```
#### Move Constructor
```sh
list<int> movedList(move(myList));  # Move elements from another list
```

### 3.6.2  Inserting Elements
#### Push Elements at the Front and Back
```sh
myList.push_back(10);  # Add element to the end
myList.push_front(5);  # Add element to the beginning

```
#### Insert at a Specific Position
```sh
auto it = myList.begin();
std::advance(it, 2);  # Move iterator to the 3rd position (0-based index)
myList.insert(it, 99);  # Insert 99 at the 3rd position
```
#### Insert Multiple Elements
```sh
myList.insert(it, 3, 20);  # Insert three 20s at the specified position
```
#### Insert from Another List
```sh
std::list<int> anotherList = {50, 60};
myList.insert(it, anotherList.begin(), anotherList.end());  # Insert another list's elements
```
#### Emplace (Avoids Copy Overhead)
```sh
myList.emplace(myList.begin(), 42);  #Efficiently inserts 42 at the beginning
```

### 3.6.3 Deleting Elements
####  Remove Specific Element
```sh
myList.remove(99);  # Removes all occurrences of 99
```
#### Erase an Element by Position
```sh
auto it = myList.begin();
std::advance(it, 2);  # Move iterator to the 3rd element
myList.erase(it);  # Remove element at that position
```
#### Erase a Range of Elements
```sh
auto start = myList.begin();
auto end = myList.begin();
std::advance(end, 3);  # Move end iterator to the 4th element
myList.erase(start, end);  # Remove elements from 1st to 3rd position
```
#### Pop Elements from Front and Back
```sh
myList.pop_front();  # Removes first element
myList.pop_back();   # Removes last element
```

#### Clear the List
```sh
myList.clear();  # Removes all elements
```

### 3.6.6 Checking Size and Emptiness
```sh
cout << "Size: " << myList.size() << endl;
if (myList.empty()) {
    cout << "List is empty!" << endl;
}
```

### 3.6.7 Accessing Elements
```sh
cout << "First: " << myList.front() << endl;
cout << "Last: " << myList.back() << endl;
```

### 3.6.8  Searching for Elements
```sh
#include <algorithm>
auto it = std::find(myList.begin(), myList.end(), 42);
if (it != myList.end()) {
    std::cout << "Element found: " << *it << std::endl;
}
```

### 3.6.8 Iterating Over a List
#### Using a `for` Loop
```sh
for (const auto& elem : myList) {
    std::cout << elem << " ";
}
```
#### Using Iterators
```sh
for (auto it = myList.begin(); it != myList.end(); ++it) {
    std::cout << *it << " ";
}
```
#### Reverse Iteration
```sh
for (auto it = myList.rbegin(); it != myList.rend(); ++it) {
    std::cout << *it << " ";
}
```

### 3.6.9 Sorting and Reversing
### Sorting a List
```sh
myList.sort();  # Sorts in ascending order
```
### Sorting with a Custom Comparator
```sh
myList.sort([](int a, int b) { return a > b; });  # Sorts in descending order
```
### Reversing a List
```sh
myList.reverse();
```

### 3.6.10 Merging and Splicing
#### Merging Two Sorted Lists
```sh
std::list<int> list1 = {1, 3, 5};
std::list<int> list2 = {2, 4, 6};
list1.merge(list2);  # Merges list2 into list1
```
#### Splicing (Move Elements from One List to Another)
```sh
std::list<int> source = {7, 8, 9};
std::list<int> destination = {1, 2, 3};

# Move all elements from source to destination
destination.splice(destination.end(), source);
```

#### 3.6.11 Removing Duplicates
```sh
myList.unique();  # Removes consecutive duplicate elements
```

## 3.7 Queue
#### 3.7.1 Definition and Initialization
```sh
#include <queue>
queue<int> myQueue;  # Empty queue
queue<int> myQueue({1, 2, 3, 4, 5});  # C++17 and later (optional)
queue<int> queueCopy(myQueue);  # Copy an existing queue
queue<int> movedQueue(move(myQueue));  # Move contents of an existing queue
```

#### 3.7.2 Basic Operations
```sh
myQueue.push(10);  # Insert element at the back
myQueue.pop();  # Removes the front element

std::cout << "Front: " << myQueue.front() << std::endl;
std::cout << "Back: " << myQueue.back() << std::endl;

myQueue.size() # Calculate the Size
myQueue.empty() # Returns True if it is Empty
```

#### 3.7.3 Iterating Over a Queue
```sh
std::queue<int> tempQueue = myQueue;  # Create a copy to avoid modifying original queue

while (!tempQueue.empty()) {
    std::cout << tempQueue.front() << " ";
    tempQueue.pop();  # Remove the processed element
}
```
#### 3.7.4 Priority Queue (`std::priority_queue`) & Deque
```sh
# Max-Heap Priority Queue (By Default)
priority_queue<int> pq;
pq.push(3);
pq.push(5);
pq.push(1);

cout << pq.top() << endl;  # Output: 5 (largest element)
pq.pop();  # Removes 5

# Min-Heap Priority Queue
priority_queue<int, vector<int>, greater<int>> minHeap;
minHeap.push(3);
minHeap.push(5);
minHeap.push(1);

cout << minHeap.top() << endl;  # Output: 1 (smallest element)

# A queue that supports efficient insertions and deletions from both ends.
deque<int> dq = {1, 2, 3};
queue<int, deque<int>> dequeQueue(dq);
```

## 3.8 Stacks
### 3.8.1 Definition and Initialization
```sh
#include <stack>
stack<int> myStack;  # Empty stack
stack<int> myStack({1, 2, 3, 4, 5});  # Not standard in all compilers
stack<int> stackCopy(myStack);  # Copy constructor
stack<int> movedStack(move(myStack));  # Move contents
```

### 3.8.2 Basic Operations
```sh
myStack.push(10);
myStack.pop();  # Removes the top element
cout << "Top: " << myStack.top() << endl;
myStack.size()  # Calculates the size 
myStack.empty() # Check whether the stack is Empty ot not
```

### 3.8.3 Iterating Over a Stack
```sh
stack<int> tempStack = myStack;  # Create a copy to avoid modifying original stack

while (!tempStack.empty()) {
    cout << tempStack.top() << " ";
    tempStack.pop();  # Remove the processed element
}
```

## 5. Object-Oriented Programming (OOP)
- Classes define the blueprint for objects, and objects are instances of a class.
### 5.1 Classes and Objects
```sh
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
```sh
#include <iostream>
using namespace std;

class BankAccount {
private:
    double balance;  # Private data member

public:
    # Constructor to initialize balance
    BankAccount(double initialBalance) {
        balance = (initialBalance >= 0) ? initialBalance : 0;
    }

    # Public methods to interact with private data
    void deposit(double amount) { balance += amount; }
    void withdraw(double amount) { if (amount <= balance) balance -= amount; }
    double getBalance() { return balance; }
};

int main() {
    BankAccount account(1000);
    account.deposit(500);
    account.withdraw(300);
    cout << "Balance: $" << account.getBalance() << endl;  # Output: Balance: $1200
    return 0;
}
```
### 5.3 Inheritance (Allows Code Reuse Between Classes)
- Inheritance allows a class to inherit properties and methods from another class.
```sh
#include <iostream>
using namespace std;

# Base class (Parent)
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
```sh
#include <iostream>
using namespace std;

class Math {
public:
    # Function Overloading: Same function name, different parameters
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
};

int main() {
    Math obj;
    cout << obj.add(5, 3) << endl;     # Output: 8
    cout << obj.add(2.5, 1.5) << endl; # Output: 4.0
    return 0;
}
```

- #### 5.4.2 Example of Function Overriding (Run-time Polymorphism):
```sh
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
```sh
#include <iostream>
using namespace std;

# Abstract class (interface)
class Shape {
public:
    virtual void draw() = 0;  # Pure virtual function
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

    shape1->draw();  # Output: Drawing a Circle
    shape2->draw();  # Output: Drawing a Rectangle

    delete shape1;
    delete shape2;
    return 0;
}
```

### 5.6 Constructor (`__init__`)
```sh
#include <iostream>
using namespace std;

class Car {
private:
    string brand;
    int speed;

public:
    # Constructor
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

### 5.7 Destructor (`__del__`)
```sh
#include <iostream>
using namespace std;

class Car {
public:
    Car() { cout << "Car is created!" << endl; }
    
    ~Car() { cout << "Car is destroyed!" << endl; }
};

int main() {
    Car myCar;  # Constructor is called automatically
    return 0;   # Destructor is called automatically when object goes out of scope
}

``` 
