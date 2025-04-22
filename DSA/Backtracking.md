# Backtracking Cheatsheet

## Backtracking Overview

- Backtracking is a recursive technique that systematically explores all possible solutions by building candidates incrementally and abandoning (backtracking) those that violate constraints. It’s ideal for combinatorial problems like permutations, combinations, and constraint satisfaction (e.g., N-Queens, Sudoku).

### How Backtracking Works

- **Core Idea**: Backtracking builds a solution step-by-step, trying all possible choices at each step. If a choice leads to an invalid solution, it undoes the choice (backtracks) and tries the next option.
- **Steps**:
  1. **Choose**: Make a choice (e.g., place a queen in a column, include an element in a subset).
  2. **Explore**: Recursively solve the remaining subproblem with the current choice.
  3. **Unchoose**: If the choice leads to an invalid solution, undo it and try another option.
- **Key Components**:
  - **State**: The current partial solution (e.g., chessboard in N-Queens).
  - **Constraints**: Rules to validate choices (e.g., queens cannot attack each other).
  - **Base Case**: When a solution is complete (e.g., all queens placed).
  - **Choices**: Options at each step (e.g., columns for a queen).
- **Process**:
  - Start with an empty solution.
  - At each step, try a choice and check constraints.
  - If valid, proceed recursively; if invalid, backtrack and try the next choice.
  - Continue until a solution is found or all possibilities are exhausted.
- **Example**: In N-Queens, place a queen in each row, checking if it’s safe (no attacks). If a row has no safe column, backtrack to the previous row and adjust.

## Backtracking Basics

### N-Queens Problem

- **Problem**: Place N queens on an NxN chessboard such that no two queens attack each other (same row, column, or diagonal).

```cpp
#include <vector>
using namespace std;

class NQueens {
    vector<vector<int>> board;
    int N;

    bool isSafe(int row, int col) {
        // Check column
        for (int i = 0; i < row; ++i) {
            if (board[i][col]) return false;
        }
        // Check upper-left diagonal
        for (int i = row, j = col; i >= 0 && j >= 0; --i, --j) {
            if (board[i][j]) return false;
        }
        // Check upper-right diagonal
        for (int i = row, j = col; i >= 0 && j < N; --i, ++j) {
            if (board[i][j]) return false;
        }
        return true;
    }

    bool solve(int row) {
        if (row == N) {
            return true; // All queens placed
        }

        for (int col = 0; col < N; ++col) {
            if (isSafe(row, col)) {
                board[row][col] = 1; // Choose
                if (solve(row + 1)) return true; // Explore
                board[row][col] = 0; // Unchoose (backtrack)
            }
        }
        return false;
    }

public:
    NQueens(int n) : N(n) {
        board.assign(N, vector<int>(N, 0));
    }

    void solve() {
        if (solve(0)) {
            for (const auto& row : board) {
                for (int val : row) {
                    cout << (val ? "Q " : ". ");
                }
                cout << "\n";
            }
        } else {
            cout << "No solution exists\n";
        }
    }
};

int main() {
    NQueens nq(4);
    nq.solve();
    // Output (one possible solution):
    // . Q . .
    // . . . Q
    // Q . . .
    // . . Q .
}
```

- **Time Complexity**: O(N!), as it tries all permutations, but pruning reduces actual attempts.
- **Space Complexity**: O(N²) for the board, O(N) for recursion stack.

---

## Common Backtracking Problems

### Subset Sum

- **Problem**: Find all subsets of an array that sum to a target value.

```cpp
#include <vector>
using namespace std;

void subsetSum(const vector<int>& nums, int target, int idx, vector<int>& current, int sum) {
    if (sum == target) {
        cout << "{ ";
        for (int x : current) cout << x << " ";
        cout << "}\n";
        return;
    }
    if (sum > target || idx == nums.size()) return; // Prune

    current.push_back(nums[idx]); // Choose
    subsetSum(nums, target, idx + 1, current, sum + nums[idx]); // Explore
    current.pop_back(); // Unchoose
    subsetSum(nums, target, idx + 1, current, sum); // Try without current element
}

int main() {
    vector<int> nums = {3, 1, 2, 4};
    int target = 5;
    vector<int> current;
    subsetSum(nums, target, 0, current, 0);
    // Output:
    // { 3 2 }
    // { 1 4 }
}
```

- **Time Complexity**: O(2^n), as it tries all subsets.
- **Space Complexity**: O(n) for recursion stack.

### Permutations

- **Problem**: Generate all permutations of an array.

```cpp
#include <vector>
using namespace std;

void permute(vector<int>& nums, int idx, vector<vector<int>>& result) {
    if (idx == nums.size()) {
        result.push_back(nums);
        return;
    }

    for (int i = idx; i < nums.size(); ++i) {
        swap(nums[idx], nums[i]); // Choose
        permute(nums, idx + 1, result); // Explore
        swap(nums[idx], nums[i]); // Unchoose
    }
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> result;
    permute(nums, 0, result);
    for (const auto& perm : result) {
        cout << "{ ";
        for (int x : perm) cout << x << " ";
        cout << "}\n";
    }
    // Output:
    // { 1 2 3 }
    // { 1 3 2 }
    // { 2 1 3 }
    // { 2 3 1 }
    // { 3 2 1 }
    // { 3 1 2 }
}
```

- **Time Complexity**: O(n!), as it generates all permutations.
- **Space Complexity**: O(n) for recursion stack.

### Sudoku Solver

- **Problem**: Solve a 9x9 Sudoku board.

```cpp
#include <vector>
using namespace std;

class SudokuSolver {
    vector<vector<char>>& board;

    bool isValid(int row, int col, char num) {
        // Check row
        for (int j = 0; j < 9; ++j) {
            if (board[row][j] == num) return false;
        }
        // Check column
        for (int i = 0; i < 9; ++i) {
            if (board[i][col] == num) return false;
        }
        // Check 3x3 box
        int startRow = row - row % 3, startCol = col - col % 3;
        for (int i = 0; i < 3; ++i) {
            for (int j = 0; j < 3; ++j) {
                if (board[startRow + i][startCol + j] == num) return false;
            }
        }
        return true;
    }

    bool solve(int row, int col) {
        if (row == 9) return true; // Board filled
        if (col == 9) return solve(row + 1, 0); // Move to next row

        if (board[row][col] != '.') return solve(row, col + 1); // Skip filled cells

        for (char num = '1'; num <= '9'; ++num) {
            if (isValid(row, col, num)) {
                board[row][col] = num; // Choose
                if (solve(row, col + 1)) return true; // Explore
                board[row][col] = '.'; // Unchoose
            }
        }
        return false;
    }

public:
    SudokuSolver(vector<vector<char>>& b) : board(b) {}

    void solve() {
        if (solve(0, 0)) {
            for (const auto& row : board) {
                for (char val : row) {
                    cout << val << " ";
                }
                cout << "\n";
            }
        } else {
            cout << "No solution exists\n";
        }
    }
};
```

- **Time Complexity**: O(9^(n\*n)), where n is the board size (9 for standard Sudoku).
- **Space Complexity**: O(n²) for recursion stack.

---

## Tricks and Tips

- **Pruning**:
  - Add constraints to reduce search space (e.g., `sum > target` in subset sum stops exploration).
  - Use early termination (e.g., `isSafe` in N-Queens avoids invalid placements).
  - Sort input to prune faster (e.g., in subset sum, sort numbers to try larger ones first).
- **State Management**:
  - Pass state by reference to avoid copying (e.g., `current` in subset sum).
  - Undo changes explicitly (e.g., `pop_back` in subset sum, `swap` in permutations).
  - Use a visited array to avoid duplicates in problems like permutations with duplicates.
- **Optimization**:
  - Combine backtracking with DP to memoize results (e.g., subset sum with memoization).
  - Use bitmasks for state tracking (e.g., track used positions in Sudoku).
  - Precompute constraints (e.g., precompute valid rows/columns in Sudoku).

**Explanation**:

- Pruning significantly reduces the number of recursive calls.
- Efficient state management ensures correctness and performance.
- Combining with DP can make backtracking feasible for larger inputs.

---

## Best Practices

- **Implementation**:
  - Define a clear base case (e.g., `row == N` in N-Queens).
  - Ensure all choices are explored (e.g., loop over columns in N-Queens).
  - Undo choices properly to maintain state (e.g., `board[row][col] = 0` in N-Queens).
- **Optimization**:
  - Use constraints to prune invalid paths early.
  - Avoid deep recursion by limiting input size where possible.
  - Test with small inputs to verify all solutions are found.
- **Debugging**:
  - Print the current state at each step to trace recursion.
  - Check for stack overflow with large inputs.
  - Verify undo operations restore the original state.

**Explanation**:

- Clear base cases prevent infinite recursion.
- Pruning and optimization make backtracking practical for larger problems.
- Debugging ensures all solutions are generated correctly.

---

## Cheat Codes

- **Quick Tips**:
  - Use a helper function to encapsulate recursive logic.
  - Pass results by reference to collect all solutions.
  - Use bitmasks for state tracking in complex problems (e.g., Sudoku).
- **Interview Questions**:
  - Solve the N-Queens problem.
  - Generate all permutations of an array.
  - Solve a Sudoku board using backtracking.

**Explanation**:

- Helper functions keep the main function clean.
- Bitmasks can replace arrays for state tracking, saving space.
- Backtracking is a common interview topic for combinatorial problems.