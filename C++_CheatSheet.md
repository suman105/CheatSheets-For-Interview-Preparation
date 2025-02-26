# C++ Cheat Sheet

## 1. **Max, Min Value**
- **Integer Limits:**
  - `INT_MAX = ~(1 << 31);` — Maximum int value (64-bit)
  - `INT_MIN = (1 << 31);` — Minimum int value (64-bit)
  - `UINT_MAX = (uint)(~0);` — Maximum unsigned int (32-bit)
  - `LONG_MAX, LONG_MIN, ULONG_MAX` — Limits for long integers

## 2. **String, Char, Integer Conversion**
- **Convert Between Types:**
  - `std::to_string(num);` — Convert int to string
  - `std::stoi(s);` — Convert string to int
  - `std::string(1, ch);` — Convert char to string
  - `std::string(charArr);` — Convert char array to string

## 3. **Strings in C++**
- **String Manipulation:**
  - `std::string str = "1234";` — Declare a string
  - `char ch = str[i];` — Access the i-th character
  - `size_t len = str.size();` — Get string length
  - `std::string sub = str.substr(start, length);` — Get substring

- **Modifications:**
  - `str.append("abc");` — Append to string
  - `str.insert(2, "sz");` — Insert at position
  - `str.replace(pos, len, "newStr");` — Replace substring
  - `str.erase(pos, length);` — Erase characters

- **Searching:**
  - `size_t found = str.find("ab");`
  - `if (found != std::string::npos) std::cout << "found";`

- **Reverse a String:**
  - `std::reverse(str.begin(), str.end());`

## 4. **Arrays**
- **Array Declarations:**
  - `int nums[10] = {0};` — Static array
  - `std::array<int, 10> arr = {0};` — `std::array` initialization
  - `std::vector<int> vec(std::begin(nums), std::end(nums));` — Convert array to vector

## 5. **Vectors**
- **Vector Initialization:**
  - `std::vector<int> v(size, 0);`
  - `std::vector<std::vector<int>> v(N, std::vector<int>(M, 0));` — 2D vector

- **Vector Operations:**
  - `v.push_back(e);` — Add element
  - `v.pop_back();` — Remove last element
  - `v.clear();` — Clear vector
  - `v.insert(v.begin(), var);` — Insert at beginning
  - `v.erase(v.begin() + 5);` — Remove element at index 5
  - `v.resize(new_size);` — Resize vector
  - `v.front();` — Get first element
  - `v.back();` — Get last element

- **Sorting:**
  - `std::sort(v.begin(), v.end());` — Sort vector

## 6. **Maps**
- **Declaration:**
  - `std::unordered_map<int, std::string> Map;`
  - `std::map<int, std::string> treeMap;` — Ordered map

- **Operations:**
  - `Map[1] = "one";` — Insert key-value pair
  - `std::string str = Map[1];` — Access value
  - `if (Map.find(1) != Map.end()) std::cout << Map[1];` — Check existence
  - `Map.erase(1);` — Remove key
  - `Map.size();` — Get size
  - `Map.empty();` — Check if empty

## 7. **Sets**
- **Declaration:**
  - `std::unordered_set<int> Set;`

- **Operations:**
  - `Set.insert(val);` — Insert value
  - `Set.erase(val);` — Remove value
  - `Set.find(1);` — Find value
  - `Set.size();` — Get size
  - `Set.empty();` — Check if empty

- **Ordered Set:**
  - `std::set<int>::iterator it = Set.upper_bound(val);`
  - `std::set<int>::iterator it = Set.lower_bound(val);`

## 8. **Priority Queue (Heap)**
- **Max Heap:**
  - `std::priority_queue<int> pq;`
- **Min Heap:**
  - `std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;`

- **Operations:**
  - `pq.push(val);` — Insert value
  - `pq.pop();` — Remove top element
  - `int top = pq.top();` — Get top element
  - `pq.size();` — Get size
  - `pq.empty();` — Check if empty

## 9. **Stack**
- **Operations:**
  - `std::stack<int> s;`
  - `s.push(1);` — Push value
  - `s.pop();` — Pop top element
  - `int top = s.top();` — Get top element
  - `s.empty();` — Check if empty
  - `s.size();` — Get size

## 10. **Queue**
- **Operations:**
  ```sh
  - `std::queue<int> q;`
  - `q.push(1);` — Push value
  - `q.pop();` — Remove front
  - `int front = q.front();` — Get front
  - `int back = q.back();` — Get back
  - `q.empty();` — Check if empty
  - `q.size();` — Get size

## 11. **Deque**
- **Operations:**
  - `std::deque<int> dq;`
  - `dq.push_back(1);`
  - `dq.push_front(-1);`
  - `dq.pop_back();`
  - `dq.pop_front();`
  - `dq.front();`
  - `dq.back();`
  - `dq.size();`

## 12. **Node Structures**
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

## 13. **Random Number Generation**
```sh
#include <cstdlib>
#include <ctime>
srand(static_cast<unsigned>(time(0)));
int randNum = rand() % 100 + 1;
```

## 13. **Mathematical Functions**
```sh
#include <cmath>
double pi = M_PI;
double root = std::sqrt(16);
double power = std::pow(2, 3);
double sine = std::sin(M_PI / 2);
double cosine = std::cos(M_PI / 3);
```
