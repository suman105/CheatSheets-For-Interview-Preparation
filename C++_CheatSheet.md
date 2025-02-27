# C++ Cheat Sheet

## Max, Min Value

```cpp
#include<climits>
INT_MAX = ~(1 << 31);   // for 64-bit machine
INT_MIN = 1 << 31;      // for 64-bit machine
UINT_MAX = (uint)(~0);  // 32-bit all equal 1
LONG_MAX;
LONG_MIN;
ULONG_MAX;
```

## String, Char, Integer Conversion

```cpp
// Convert int to string
std::to_string(num);
// Convert string to int
std::stoi(s);
// Convert char to string
std::string(1, ch);
// Convert char array to string
std::string(charArr);
```

## Strings in C++

Strings in C++ are mutable and provide various methods for manipulation:

```cpp
std::string str = "1234";
char ch = str[i]; // Access ith character
size_t len = str.size();
std::string sub = str.substr(start, length);

// String modifications
str.append("abc");
str.insert(2, "sz");
str.replace(pos, len, "newStr");
str.erase(pos, length);

// Search
size_t found = str.find("ab");
if (found != std::string::npos) std::cout << "found";

// Reverse
std::reverse(str.begin(), str.end());
```

## Arrays

```cpp
#include <array>
int nums[10] = {0};
std::array<int, 10> arr = {0};
std::vector<int> vec(std::begin(nums), std::end(nums)); // Convert array to vector
```

## Vectors

```cpp
#include <vector>
std::vector<int> v(size, 0);
std::vector<std::vector<int>> v(N, std::vector<int>(M, 0));

// Operations
v.push_back(e);
v.pop_back();
v.clear();
v.insert(v.begin(), var);
v.erase(v.begin() + 5);
v.resize(new_size);
v.front();
v.back();

// Sorting
std::sort(v.begin(), v.end());
```

## Maps

```cpp
#include <map>
#include <unordered_map>
std::unordered_map<int, std::string> Map;
std::map<int, std::string> treeMap;

// Insert, access, and erase
Map[1] = "one";
std::string str = Map[1];
if (Map.find(1) != Map.end()) std::cout << Map[1] << std::endl;
Map.erase(1);
Map.size();
Map.empty();
```

## Sets

```cpp
#include <set>
#include <unordered_set>
std::unordered_set<int> Set;
Set.insert(val);
Set.erase(val);
Set.find(1);
Set.size();
Set.empty();

// Ordered set operations
std::set<int>::iterator it = Set.upper_bound(val);
std::set<int>::iterator it = Set.lower_bound(val);
```

## Priority Queue (Heap)

```cpp
#include <queue>
std::priority_queue<int> pq;
std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;

pq.push(val);
pq.pop();
int top = pq.top();
pq.size();
pq.empty();
```

## Stack

```cpp
#include <stack>
std::stack<int> s;
s.push(1);
s.pop();
int top = s.top();
bool isEmpty = s.empty();
s.size();
```

## Queue

```cpp
#include <queue>
std::queue<int> q;
q.push(1);
q.pop();
int front = q.front();
int back = q.back();
bool isEmpty = q.empty();
q.size();
```

## Deque

```cpp
#include <deque>
std::deque<int> dq;
dq.push_back(1);
dq.push_front(-1);
dq.pop_back();
dq.pop_front();
dq.front();
dq.back();
dq.size();
```

## Node Structures

```cpp
class ListNode{
public:
    int val;
    ListNode* next;
    ListNode(int val) { this->val = val; this->next = nullptr; }
};

class TreeNode{
public:
    int val;
    TreeNode *left, *right;
    TreeNode(int val) { this->val = val; this->left = this->right = nullptr; }
};
```

## Random Number Generation

```cpp
#include <cstdlib>
#include <ctime>
srand(static_cast<unsigned>(time(0)));
int randNum = rand() % 100 + 1;
```

## Mathematical Functions

```cpp
#include <cmath>
double pi = M_PI;
double root = std::sqrt(16);
double power = std::pow(2, 3);
double sine = std::sin(M_PI / 2);
double cosine = std::cos(M_PI / 3);
```

This cheat sheet covers fundamental C++ data structures, methods, and algorithms. Let me know if you need more additions!

