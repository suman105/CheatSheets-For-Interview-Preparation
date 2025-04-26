# Time Complexity, Space Complexity, and Asymptotic Analysis

## Overview
- **Definition**: Asymptotic analysis evaluates algorithm performance in terms of time and space requirements as input size grows, using notations like Big-O, Omega, and Theta.
- **Key Characteristics**:
  - **Time Complexity**: Measures computational time as a function of input size.
  - **Space Complexity**: Measures memory usage as a function of input size.
  - **Asymptotic Notations**: Describe limiting behavior (upper, lower, tight bounds).
- **When to Use**:
  - To compare algorithm efficiency (e.g., sorting algorithms).
  - To predict scalability for large inputs.
- **Advantages**:
  - Simplifies performance analysis by focusing on growth rates.
  - Identifies bottlenecks for optimization.
- **Disadvantages**:
  - Ignores constants and lower-order terms, relevant for small inputs.
  - Often assumes worst-case, which may not always occur.

## Asymptotic Notations
- **Big-O (O)**: Upper bound, worst-case scenario.
  - Example: O(n²) means time grows at most quadratically.
- **Big-Omega (Ω)**: Lower bound, best-case scenario.
  - Example: Ω(n) means at least linear time.
- **Big-Theta (Θ)**: Tight bound, both upper and lower.
  - Example: Θ(n log n) means exactly proportional to n log n.
- **Little-o (o)**: Strict upper bound, excludes equality.
- **Little-omega (ω)**: Strict lower bound, excludes equality.

## Common Time Complexities
| Complexity | Name               | Example Algorithms                     |
|------------|--------------------|----------------------------------------|
| O(1)       | Constant           | Array access, hash table lookup        |
| O(log n)   | Logarithmic        | Binary search, balanced BST operations |
| O(n)       | Linear             | Linear search, array traversal         |
| O(n log n) | Linearithmic       | Merge sort, quicksort (average)        |
| O(n²)      | Quadratic          | Bubble sort, nested loops              |
| O(2ⁿ)      | Exponential        | Recursive Fibonacci, subset sum        |
| O(n!)      | Factorial          | Traveling Salesman (brute force)       |

## Common Space Complexities
| Complexity | Example Scenarios                     |
|------------|---------------------------------------|
| O(1)       | In-place algorithms (e.g., swap)      |
| O(n)       | Arrays, recursion stack for DFS       |
| O(n²)      | Adjacency matrix for graphs           |
| O(log n)   | Recursion stack in binary search      |
| O(n log n) | Merge sort (auxiliary array)          |

## Examples and Analysis (C++)

### 1. Linear Search
- **Problem**: Find an element in an unsorted array.

#### Solution (C++)
```cpp
#include <vector>
using namespace std;

int linearSearch(vector<int>& arr, int target) {
    // Iterate through each element
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == target) return i;
    }
    return -1;
}

int main() {
    vector<int> arr = {5, 2, 9, 1, 7};
    int target = 9;
    cout << linearSearch(arr, target) << endl; // Output: 2
    return 0;
}
```

#### Time Complexity Analysis
- **Step 1**: Identify the main operation. The algorithm iterates through the array, checking each element against the target.
- **Step 2**: Count iterations. The `for` loop runs from `i = 0` to `i < arr.size()`, which is `n` iterations, where `n` is the array size.
- **Step 3**: Analyze operations per iteration. Each iteration performs a constant-time comparison (`arr[i] == target`).
- **Step 4**: Calculate total time. Since there are `n` iterations, each taking O(1) time, the total time is `n * O(1) = O(n)`.
- **Step 5**: Consider cases. In the worst case (target not found or at the end), all `n` elements are checked, so the time complexity is O(n).

#### Space Complexity Analysis
- **Step 1**: Identify variables. The algorithm uses:
  - `i`: An integer for the loop counter.
  - `target`: An integer (input parameter).
  - `arr`: The input array (not counted as extra space).
- **Step 2**: Assess memory usage. Only `i` and `target` are extra variables, each taking constant space (O(1)).
- **Step 3**: Check for dynamic allocations. No arrays, recursion, or other data structures are created.
- **Step 4**: Total space. Since only a fixed number of variables are used regardless of input size, the space complexity is O(1).

### 2. Binary Search
- **Problem**: Find an element in a sorted array.

#### Solution (C++)
```cpp
#include <vector>
using namespace std;

int binarySearch(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    // Repeatedly divide search space
    while (left <= right) {
        int mid = left + (right - left) / 2; // Avoid overflow
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    int target = 3;
    cout << binarySearch(arr, target) << endl; // Output: 2
    return 0;
}
```

#### Time Complexity Analysis
- **Step 1**: Identify the main operation. The algorithm divides the search space in half each iteration.
- **Step 2**: Count iterations. Each iteration halves the search range (`right - left`). If the initial range is `n`, the number of iterations is the number of times `n` can be divided by 2 until it reaches 1, which is `log₂(n)`.
- **Step 3**: Analyze operations per iteration. Each iteration performs:
  - A constant-time calculation for `mid`.
  - A constant-time comparison (`arr[mid] == target`).
  - A constant-time update (`left` or `right`).
- **Step 4**: Calculate total time. With `log n` iterations, each taking O(1) time, the total time is `log n * O(1) = O(log n)`.
- **Step 5**: Consider cases. The worst case (target not found) still takes `log n` iterations, so the time complexity is O(log n).

#### Space Complexity Analysis
- **Step 1**: Identify variables. The algorithm uses:
  - `left`, `right`, `mid`: Integers for pointers.
  - `target`: An integer (input parameter).
  - `arr`: The input array (not counted).
- **Step 2**: Assess memory usage. All variables (`left`, `right`, `mid`, `target`) take constant space (O(1)).
- **Step 3**: Check for dynamic allocations. This iterative version has no recursion or extra arrays.
- **Step 4**: Total space. Since only a fixed number of variables are used, the space complexity is O(1).
- **Note**: A recursive binary search would use O(log n) space due to the call stack, but this iterative version avoids that.

### 3. Merge Sort
- **Problem**: Sort an array.

#### Solution (C++)
```cpp
#include <vector>
using namespace std;

void merge(vector<int>& arr, int left, int mid, int right) {
    vector<int> temp(right - left + 1);
    int i = left, j = mid + 1, k = 0;
    // Merge two sorted halves
    while (i <= mid && j <= right) {
        temp[k++] = (arr[i] <= arr[j]) ? arr[i++] : arr[j++];
    }
    while (i <= mid) temp[k++] = arr[i++];
    while (j <= right) temp[k++] = arr[j++];
    for (i = left, k = 0; i <= right; ++i, ++k) arr[i] = temp[k];
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        // Recursively sort halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

int main() {
    vector<int> arr = {5, 2, 9, 1, 7};
    mergeSort(arr, 0, arr.size() - 1);
    for (int x : arr) cout << x << " "; // Output: 1 2 5 7 9
    return 0;
}
```

#### Time Complexity Analysis
- **Step 1**: Break down the algorithm. Merge sort divides the array into two halves recursively and merges them.
- **Step 2**: Set up the recurrence. The time complexity `T(n)` is:
  - Divide: Split into two halves, O(1) for calculating `mid`.
  - Conquer: Two recursive calls, each on `n/2` elements, so `2T(n/2)`.
  - Merge: Linear time to merge `n` elements, O(n).
  - Recurrence: `T(n) = 2T(n/2) + O(n)`.
- **Step 3**: Solve the recurrence. Using the Master Theorem:
  - Form: `T(n) = aT(n/b) + f(n)`, where `a = 2`, `b = 2`, `f(n) = O(n)`.
  - Compare: `f(n) = O(n) = O(n^{log_b a}) = O(n^{log_2 2}) = O(n)`.
  - Case 2 applies: `T(n) = O(n log n)`.
- **Step 4**: Verify merge step. The `merge` function processes `right - left + 1` elements (up to `n`), with O(n) comparisons and copies.
- **Step 5**: Total time. The recurrence confirms O(n log n) for all cases (best, average, worst).

#### Space Complexity Analysis
- **Step 1**: Identify memory usage. The algorithm uses:
  - `temp` array in `merge`: Size `right - left + 1`, up to `n` at the top level.
  - Recursion stack: `mergeSort` calls itself `log n` times (depth of recursion tree).
  - Variables: `i`, `j`, `k`, `mid`, etc., all O(1).
- **Step 2**: Analyze `temp` array. The largest `temp` array is O(n) when merging the full array.
- **Step 3**: Analyze recursion stack. The recursion depth is `log n` (since the array is halved each time), but each call uses O(1) extra variables, so stack space is O(log n).
- **Step 4**: Total space. The dominant factor is the `temp` array (O(n)). The recursion stack (O(log n)) is smaller, so the total auxiliary space is O(n).
- **Note**: The input array `arr` is modified in-place but not counted as extra space.

### 4. Matrix Multiplication
- **Problem**: Multiply two n×n matrices.

#### Solution (C++)
```cpp
#include <vector>
using namespace std;

vector<vector<int>> matrixMultiply(vector<vector<int>>& A, vector<vector<int>>& B) {
    int n = A.size();
    vector<vector<int>> result(n, vector<int>(n, 0));
    // Triple loop for matrix multiplication
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            for (int k = 0; k < n; ++k) {
                result[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    return result;
}

int main() {
    vector<vector<int>> A = {{1, 2}, {3, 4}};
    vector<vector<int>> B = {{5, 6}, {7, 8}};
    auto result = matrixMultiply(A, B);
    for (const auto& row : result) {
        for (int x : row) cout << x << " ";
        cout << endl;
    }
    // Output: 19 22
    //         43 50
    return 0;
}
```

#### Time Complexity Analysis
- **Step 1**: Identify the main operation. The algorithm uses three nested loops to compute each element of the result matrix.
- **Step 2**: Count iterations:
  - Outer loop (`i`): Runs `n` times.
  - Middle loop (`j`): Runs `n` times for each `i`.
  - Inner loop (`k`): Runs `n` times for each `i`, `j` pair.
- **Step 3**: Analyze operations per iteration. The inner loop performs a constant-time operation (`result[i][j] += A[i][k] * B[k][j]`).
- **Step 4**: Calculate total time. Total iterations = `n * n * n = n³`. Each iteration is O(1), so total time is `n³ * O(1) = O(n³)`.
- **Step 5**: Consider cases. The loops always run fully, so O(n³) applies to all cases.

#### Space Complexity Analysis
- **Step 1**: Identify memory usage. The algorithm uses:
  - `result`: An n×n matrix to store the output.
  - Variables: `i`, `j`, `k`, all O(1).
  - Input matrices `A` and `B`: Not counted as extra space.
- **Step 2**: Analyze `result`. The `result` matrix has `n * n = n²` elements, so it takes O(n²) space.
- **Step 3**: Check for other allocations. No recursion or additional arrays are used.
- **Step 4**: Total space. The `result` matrix dominates, giving O(n²) auxiliary space.

## Tricks and Tips
- **Simplify Analysis**:
  - Focus on the dominant term (e.g., O(n² + n) simplifies to O(n²)).
  - Count loops: Single loop = O(n), nested loops = O(n²).
- **Amortized Analysis**:
  - Dynamic array resizing: O(n) per resize but O(1) amortized per insertion.
- **Master Theorem**:
  - For recurrences `T(n) = aT(n/b) + f(n)`, apply Master Theorem.
    - Example: Merge sort `T(n) = 2T(n/2) + O(n)` → O(n log n).
- **Space Optimization**:
  - Use in-place algorithms (e.g., quicksort) to reduce space to O(log n) or O(1).
  - Reuse variables or arrays to minimize allocations.
- **Edge Cases**:
  - Empty inputs: O(1) time, O(1) space.
  - Arithmetic overflow: Use safe calculations (e.g., `mid = left + (right - left) / 2`).

## Common Mistakes
- **Ignoring Constants**: Treating O(2n) as different from O(n) – they’re equivalent.
- **Confusing Notations**: Using O(n) for best-case when Ω(n) is needed.
- **Missing Stack Space**: Forgetting recursion stack (e.g., O(log n) for recursive binary search).
- **Worst vs. Average**: Quicksort is O(n²) worst-case but O(n log n) average.
- **Auxiliary Space**: Overlooking temporary arrays (e.g., merge sort’s O(n)).