# Dynamic Programming Cheatsheet

## Dynamic Programming Overview

- Dynamic Programming (DP) solves problems by breaking them into overlapping subproblems, solving each subproblem once, and storing results for reuse. This cheatsheet covers DP techniques in C++, with examples and tricks.

## DP Basics

### Key Concepts

- **Overlapping Subproblems**: Subproblems are solved multiple times in a recursive solution.
- **Optimal Substructure**: The optimal solution to the problem can be constructed from optimal solutions of subproblems.
- **Memoization (Top-Down)**: Store results of subproblems in a cache.
- **Tabulation (Bottom-Up)**: Build solutions iteratively using a table.

### Fibonacci Example (Memoization)

```cpp
#include <vector>
using namespace std;

long long fibonacciMemo(int n, vector<long long>& memo) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    memo[n] = fibonacciMemo(n-1, memo) + fibonacciMemo(n-2, memo);
    return memo[n];
}

long long fibonacci(int n) {
    vector<long long> memo(n+1, -1);
    return fibonacciMemo(n, memo);
}
```

- **Time Complexity**: O(n), compared to O(2^n) without memoization.
- **Space Complexity**: O(n) for the memoization table.

### Fibonacci Example (Tabulation)

```cpp
long long fibonacciTab(int n) {
    if (n <= 1) return n;
    vector<long long> dp(n+1);
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; ++i) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

- **Time Complexity**: O(n).
- **Space Complexity**: O(n), but can be optimized to O(1) by using two variables.

---

## Common DP Patterns

### 1D DP: Knapsack Problem

- **Problem**: Given weights and values of n items, select items to maximize value within a weight limit W.

```cpp
int knapsack(int W, const vector<int>& weights, const vector<int>& values, int n) {
    vector<vector<int>> dp(n+1, vector<int>(W+1, 0));

    for (int i = 1; i <= n; ++i) {
        for (int w = 0; w <= W; ++w) {
            if (weights[i-1] <= w) {
                dp[i][w] = max(values[i-1] + dp[i-1][w-weights[i-1]], dp[i-1][w]);
            } else {
                dp[i][w] = dp[i-1][w];
            }
        }
    }
    return dp[n][W];
}
```

- **Time Complexity**: O(n \* W).
- **Space Complexity**: O(n \* W), can be optimized to O(W) by using a 1D array.

### 2D DP: Longest Common Subsequence (LCS)

- **Problem**: Find the length of the longest common subsequence between two strings.

```cpp
int LCS(const string& s1, const string& s2) {
    int m = s1.length(), n = s2.length();
    vector<vector<int>> dp(m+1, vector<int>(n+1, 0));

    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (s1[i-1] == s2[j-1]) {
                dp[i][j] = dp[i-1][j-1] + 1;
            } else {
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    return dp[m][n];
}
```

- **Time Complexity**: O(m \* n).
- **Space Complexity**: O(m \* n), can be optimized to O(min(m, n)).

---

## Tricks and Tips

- **State Definition**:
  - Define the DP state clearly (e.g., `dp[i]` = max value for first i items).
  - Include all necessary variables (e.g., `dp[i][w]` for knapsack).
- **Space Optimization**:
  - For 1D DP, use two variables or a rolling array (e.g., Fibonacci).
  - For 2D DP, reduce to 1D if only previous rows are needed (e.g., knapsack).
- **Base Cases**:
  - Initialize base cases correctly (e.g., `dp[0][w] = 0` in knapsack).
  - Handle edge cases (e.g., empty strings in LCS).
- **Transition**:
  - Write the recurrence relation (e.g., `dp[i] = dp[i-1] + dp[i-2]` for Fibonacci).
  - Ensure transitions cover all possibilities (e.g., include/exclude item in knapsack).

**Explanation**:

- Clear state definition avoids confusion in DP formulation.
- Space optimization reduces memory usage, crucial for large inputs.
- Base cases and transitions ensure correctness of the DP solution.

---

## Example: Minimum Path Sum

- **Problem**: Find the minimum path sum from top-left to bottom-right in a grid, moving only right or down.

```cpp
#include <vector>

int minPathSum(vector<vector<int>>& grid) {
    int m = grid.size(), n = grid[0].size();
    vector<vector<int>> dp(m, vector<int>(n, 0));

    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; ++i) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; ++j) dp[0][j] = dp[0][j-1] + grid[0][j];

    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
        }
    }
    return dp[m-1][n-1];
}

int main() {
    vector<vector<int>> grid = {
        {1, 3, 1},
        {1, 5, 1},
        {4, 2, 1}
    };
    cout << "Minimum Path Sum: " << minPathSum(grid) << "\n";
    // Output: Minimum Path Sum: 7 (path: 1->3->1->1->1)
}
```

---

## Best Practices

- **Formulation**:
  - Identify overlapping subproblems and optimal substructure.
  - Start with a recursive solution, then optimize with DP.
  - Write the state transition equation before coding.
- **Optimization**:
  - Use tabulation for better space efficiency.
  - Reduce dimensions where possible (e.g., 2D to 1D).
  - Avoid unnecessary computations by initializing properly.
- **Debugging**:
  - Test with small inputs to verify DP table values.
  - Print the DP table for complex problems.
  - Check base cases and transitions for correctness.

**Explanation**:

- Proper formulation ensures the DP approach is applicable.
- Optimization reduces time and space complexity.
- Debugging with small cases helps catch errors early.

---

## Cheat Codes

- **Quick Tips**:
  - Use `vector` for DP tables; initialize with appropriate size.
  - For knapsack, iterate weights in reverse to avoid overwriting.
  - Combine DP with other techniques (e.g., DP + Greedy for optimization).
- **Interview Questions**:
  - Find the longest increasing subsequence.
  - Solve the 0/1 knapsack problem.
  - Compute the minimum edit distance between two strings.

**Explanation**:

- `vector` is safer than arrays for dynamic sizing.
- Reverse iteration in knapsack ensures items are used at most once.
- DP often pairs with other paradigms for complex problems.