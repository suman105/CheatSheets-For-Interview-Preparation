# C++ Cheat Sheet

## 1. Basics

### 1.1 Install C++
Download from [C++](https://isocpp.org/get-started) and verify installation:
```sh
g++ --version
```
### 1.2 Variables & Data Types
```sh
int x = 10;         // Integer
float y = 3.14f;    // Float
double z = 3.1415;  // Double
char c = 'A';       // Char
bool flag = true;   // Boolean
string str = "Hello"; // String (using <string> header)
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

greet();  // Output: Hello, world!
```
### 2.2 Function With Parameters
```sh
void greet(string name) {
    cout << "Hello, " << name << "!" << endl;
}

greet("Shreyas");  // Output: Hello, Shreyas!
```
### 2.3 Function With Return Value
```sh
int add(int a, int b) {
    return a + b;
}

int result = add(5, 3);  // Output: 8
cout << result << endl;
```
### 2.4 Function With Default Parameters
```sh
void greet(string name = "Guest") {
    cout << "Hello, " << name << "!" << endl;
}

greet();           // Output: Hello, Guest!
greet("Shreyas");  // Output: Hello, Shreyas!
```
### 2.5 Lambda Functions
```sh
auto square = [](int x) { return x * x; };
cout << square(5) << endl;  // Output: 25

auto add = [](int x, int y) { return x + y; };
cout << add(3, 4) << endl;  // Output: 7
```
### 2.6 Function With Multiple Parameters
```sh
int add(int a, int b, int c) {
    return a + b + c;
}

cout << add(1, 2, 3) << endl;  // Output: 6
```

## 3. Data Structures
### 3.1 Arrays (Fixed Size)
```sh
#include <array>
#include <algorithm>  // For algorithms like sort, reverse, etc.

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
auto it = treeMap.lower_bound(3);  // Smallest key ≥ 3
if (it != treeMap.end()) {
    std::cout << "Lower bound: " << it->first << " -> " << it->second << std::endl;
}
```
#### Find the First Element Strictly Greater (`upper_bound`)
```sh
auto it = treeMap.upper_bound(3);  // Smallest key > 3
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
