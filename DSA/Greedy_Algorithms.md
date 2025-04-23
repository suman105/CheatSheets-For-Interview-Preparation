# Greedy Algorithms Cheatsheet

## Overview
- **Definition**: Greedy algorithms make locally optimal choices at each step to find a global optimum, often used for optimization problems.
- **Key Characteristics**:
  - Greedy Choice Property: A global optimum can be reached by selecting a local optimum.
  - Optimal Substructure: An optimal solution contains optimal solutions to subproblems.
- **When to Use**:
  - Problems where a greedy choice leads to an optimal solution (e.g., scheduling, graph algorithms).
- **Advantages**:
  - Simple and efficient (often O(n log n) or better).
- **Disadvantages**:
  - Not always optimal; requires proof of correctness.

## Common Greedy Problems and Solutions (C++)

### 1. Activity Selection Problem
- **Problem**: Given activities with start and finish times, select the maximum number of non-overlapping activities.
- **Greedy Strategy**: Sort by finish time and pick activities that don’t overlap.
- **Example**:
  - Input: `activities = [(1, 4), (3, 5), (0, 6), (5, 7)]`
  - Output: `[(1, 4), (5, 7)]`

#### Solution (C++)
```cpp
#include <vector>
#include <algorithm>
using namespace std;

std::vector<std::pair<int, int>> activitySelection(std::vector<std::pair<int, int>>& activities) {
    // Sort by finish time
    sort(activities.begin(), activities.end(), 
              [](const auto& a, const auto& b) { return a.second < b.second; });
    
    vector<pair<int, int>> selected;
    selected.push_back(activities[0]);
    int lastFinish = activities[0].second;
    
    for (size_t i = 1; i < activities.size(); ++i) {
        if (activities[i].first >= lastFinish) {
            selected.push_back(activities[i]);
            lastFinish = activities[i].second;
        }
    }
    return selected;
}

int main() {
    vector<pair<int, int>> activities = {{1, 4}, {3, 5}, {0, 6}, {5, 7}};
    auto result = activitySelection(activities);
    for (const auto& activity : result) {
        cout << "(" << activity.first << ", " << activity.second << ") ";
    }
    // Output: (1, 4) (5, 7)
    return 0;
}
```

### 2. Fractional Knapsack Problem
- **Problem**: Maximize total value in a knapsack of capacity W (fractional items allowed).
- **Greedy Strategy**: Sort by value-to-weight ratio (descending) and add items greedily.
- **Example**:
  - Input: `items = [(60, 10), (100, 20), (120, 30)]`, `W = 50`
  - Output: `240`

#### Solution (C++)
```cpp
#include <vector>
#include <algorithm>
using namespace std;

double fractionalKnapsack(int W, vector<pair<int, int>>& items) {
    // Store value-to-weight ratio with original items
    vector<pair<double, pair<int, int>>> ratio;
    for (const auto& item : items) {
        double r = static_cast<double>(item.first) / item.second;
        ratio.push_back({r, item});
    }
    // Sort by ratio in descending order
    sort(ratio.begin(), ratio.end(), greater<>());
    
    double totalValue = 0.0;
    int remainingW = W;
    
    for (const auto& r : ratio) {
        int value = r.second.first;
        int weight = r.second.second;
        if (remainingW >= weight) {
            totalValue += value;
            remainingW -= weight;
        } else {
            totalValue += remainingW * r.first;
            break;
        }
    }
    return totalValue;
}

int main() {
    vector<pair<int, int>> items = {{60, 10}, {100, 20}, {120, 30}};
    int W = 50;
    cout << fractionalKnapsack(W, items) << endl;  // Output: 240
    return 0;
}
```

### 3. Huffman Coding
- **Problem**: Compress a string by assigning variable-length codes based on character frequencies.
- **Greedy Strategy**: Build a Huffman Tree by combining nodes with the smallest frequencies.
- **Example**:
  - Input: `chars = ['a', 'b', 'c']`, `freq = [5, 9, 12]`
  - Output: Codes like `a:00`, `b:01`, `c:1`

#### Solution (C++)
```cpp
#include <queue>
#include <vector>
#include <string>
#include <iostream>
using namespace std;

struct Node {
    char ch;
    int freq;
    Node *left, *right;
    Node(char c, int f) : ch(c), freq(f), left(nullptr), right(nullptr) {}
};

struct Compare {
    bool operator()(Node* a, Node* b) {
        return a->freq > b->freq;
    }
};

void printCodes(Node* root, string code) {
    if (!root) return;
    if (root->ch != '$') {
        cout << root->ch << ": " << code << endl;
    }
    printCodes(root->left, code + "0");
    printCodes(root->right, code + "1");
}

void huffmanCoding(vector<char>& chars, vector<int>& freq) {
    priority_queue<Node*, vector<Node*>, Compare> pq;
    for (size_t i = 0; i < chars.size(); ++i) {
        pq.push(new Node(chars[i], freq[i]));
    }
    
    while (pq.size() > 1) {
        Node* left = pq.top(); pq.pop();
        Node* right = pq.top(); pq.pop();
        Node* parent = new Node('$', left->freq + right->freq);
        parent->left = left;
        parent->right = right;
        pq.push(parent);
    }
    
    printCodes(pq.top(), "");
}

int main() {
    vector<char> chars = {'a', 'b', 'c'};
    vector<int> freq = {5, 9, 12};
    huffmanCoding(chars, freq);
    // Output: c: 1, b: 01, a: 00
    return 0;
}
```

### 4. Minimum Spanning Tree (Kruskal's Algorithm)
- **Problem**: Find the minimum spanning tree (MST) of a graph.
- **Greedy Strategy**: Sort edges by weight, add them to MST if they don’t form a cycle (use Union-Find).
- **Example**:
  - Input: Edges `[(0, 1, 10), (0, 2, 6), (0, 3, 5), (1, 3, 15), (2, 3, 4)]`
  - Output: MST `[(2, 3, 4), (0, 3, 5), (0, 1, 10)]`

#### Solution (C++)
```cpp
#include <vector>
#include <algorithm>
using namespace std;

class DisjointSet {
    vector<int> parent, rank;
public:
    DisjointSet(int n) : parent(n), rank(n, 0) {
        for (int i = 0; i < n; ++i) parent[i] = i;
    }
    
    int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]);
        return parent[x];
    }
    
    bool unionSet(int x, int y) {
        int px = find(x), py = find(y);
        if (px == py) return false;
        if (rank[px] < rank[py]) swap(px, py);
        parent[py] = px;
        if (rank[px] == rank[py]) ++rank[px];
        return true;
    }
};

vector<tuple<int, int, int>> kruskal(int n, vector<tuple<int, int, int>>& edges) {
    sort(edges.begin(), edges.end(), 
              [](const auto& a, const auto& b) { return get<2>(a) < get<2>(b); });
    
    DisjointSet ds(n);
    vector<tuple<int, int, int>> mst;
    
    for (const auto& edge : edges) {
        int u = get<0>(edge), v = get<1>(edge), w = get<2>(edge);
        if (ds.unionSet(u, v)) {
            mst.push_back(edge);
        }
    }
    return mst;
}

int main() {
    vector<tuple<int, int, int>> edges = {{0, 1, 10}, {0, 2, 6}, {0, 3, 5}, {1, 3, 15}, {2, 3, 4}};
    auto mst = kruskal(4, edges);
    for (const auto& edge : mst) {
        cout << "(" << get<0>(edge) << ", " << get<1>(edge) << ", " << get<2>(edge) << ") ";
    }
    // Output: (2, 3, 4) (0, 3, 5) (0, 1, 10)
    return 0;
}
```

## Tricks and Tips
- **Sorting**: Use `std::sort` with custom comparators for efficiency (e.g., sort by finish time, ratio, or weight).
- **Data Structures**:
  - Use `std::priority_queue` for Huffman Coding.
  - Use Union-Find (Disjoint Set) for Kruskal’s algorithm.
- **Edge Cases**:
  - Handle empty inputs or single elements.
  - Check for negative weights/values in MST or knapsack problems.
- **Optimization**:
  - Avoid unnecessary copies with references (`const auto&`).
  - Use `reserve()` for vectors to prevent reallocations.

## Common Mistakes
- **Assuming Greedy Works**: Greedy fails for problems like 0/1 Knapsack (use DP instead).
- **Ignoring Cycles**: In Kruskal’s, failing to detect cycles leads to incorrect MSTs.
- **Sorting Errors**: Ensure correct comparator logic in `std::sort`.

## Practice Problems
- **Easy**:
  - Coin Change (minimum coins, if greedy applies).
  - Job Sequencing with Deadlines.
- **Medium**:
  - Minimum Number of Platforms for Train Schedules.
  - Fractional Knapsack.
- **Hard**:
  - Huffman Coding.
  - Minimum Cost to Connect All Cities (MST).

## Time Complexities
- **Activity Selection**: O(n log n) due to sorting.
- **Fractional Knapsack**: O(n log n) due to sorting.
- **Huffman Coding**: O(n log n) with priority queue.
- **Kruskal’s Algorithm**: O(E log E) for sorting edges.

## Resources
- Books: "Introduction to Algorithms" by Cormen.
- Online: LeetCode, HackerRank, GeeksforGeeks.