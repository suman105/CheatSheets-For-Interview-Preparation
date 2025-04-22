# Bit Manipulation Cheatsheet

## Bit Manipulation Overview

- Bit Manipulation uses bitwise operators to solve problems efficiently at the bit level. It’s often faster than arithmetic operations and is widely used in low-level programming, competitive programming, and interviews. This cheatsheet covers techniques in C++.

## Bitwise Operators

### Basics

- **AND (**`&`**)**: Sets bit to 1 if both bits are 1.
- **OR (**`|`**)**: Sets bit to 1 if either bit is 1.
- **XOR (**`^`**)**: Sets bit to 1 if bits are different.
- **NOT (**`~`**)**: Flips all bits.
- **Left Shift (**`<<`**)**: Shifts bits left, fills with 0.
- **Right Shift (**`>>`**)**: Shifts bits right, fills with sign bit (for signed integers).

```cpp
int main() {
    int a = 5;  // 0101
    int b = 3;  // 0011

    cout << (a & b) << "\n";  // 1 (0001)
    cout << (a | b) << "\n";  // 7 (0111)
    cout << (a ^ b) << "\n";  // 6 (0110)
    cout << (~a) << "\n";     // -6 (inverts bits)
    cout << (a << 1) << "\n"; // 10 (1010)
    cout << (a >> 1) << "\n"; // 2 (0010)
}
```

---

## Common Bit Manipulation Techniques

### Check if a Number is Even or Odd

```cpp
bool isEven(int n) {
    return (n & 1) == 0;
}
```

- **Explanation**: LSB (least significant bit) is 1 for odd numbers, 0 for even. `n & 1` checks the LSB.

### Set, Clear, Toggle, and Check Bits

```cpp
// Set bit at position pos
int setBit(int n, int pos) {
    return n | (1 << pos);
}

// Clear bit at position pos
int clearBit(int n, int pos) {
    return n & ~(1 << pos);
}

// Toggle bit at position pos
int toggleBit(int n, int pos) {
    return n ^ (1 << pos);
}

// Check if bit at position pos is set
bool isBitSet(int n, int pos) {
    return (n & (1 << pos)) != 0;
}
```

- **Use Case**: Manipulate specific bits in flags or masks.

### Count Set Bits

- **Brian Kernighan’s Algorithm**:

```cpp
int countSetBits(int n) {
    int count = 0;
    while (n) {
        n &= (n - 1); // Clear the least significant set bit
        count++;
    }
    return count;
}
```

- **Time Complexity**: O(number of set bits).
- **Use Case**: Count 1s in a binary number.

### Find Single Number

- **Problem**: Find the number that appears once in an array where every other number appears twice.

```cpp
int singleNumber(const vector<int>& nums) {
    int result = 0;
    for (int num : nums) {
        result ^= num;
    }
    return result;
}
```

- **Explanation**: `a ^ a = 0`, so pairs cancel out; `a ^ 0 = a`, so the single number remains.

---

## More Bit Manipulation Tricks

- **Swap Two Numbers Without Temp Variable**:

```cpp
void swap(int& a, int& b) {
    a ^= b;
    b ^= a;
    a ^= b;
}
```

- **Explanation**: XOR-based swap uses the property `a ^ a = 0` and `a ^ 0 = a`.

- **Check if a Number is a Power of 2**:

```cpp
bool isPowerOf2(int n) {
    return n && !(n & (n - 1));
}
```

- **Explanation**: A power of 2 has exactly one set bit (e.g., 8 = 1000). `n & (n-1)` clears the rightmost set bit; if the result is 0, only one bit was set.

- **Get the Rightmost Set Bit**:

```cpp
int rightmostSetBit(int n) {
    return n & -n;
}
```

- **Explanation**: `n & -n` isolates the rightmost 1 (e.g., for 12 = 1100, it returns 4 = 0100). This works because `-n` is the two’s complement of n, flipping bits after the rightmost 1.

- **Check if a Number is a Power of 4**:

```cpp
bool isPowerOf4(int n) {
    return n > 0 && (n & (n - 1)) == 0 && (countSetBits(n - 1) % 2) == 0;
}
```

- **Explanation**:

  - `n & (n-1) == 0` ensures n is a power of 2.
  - For powers of 4 (e.g., 4 = 100, 16 = 10000), the set bit is at an even position (0-based: 2, 4, ...).
  - `countSetBits(n-1)` counts bits up to the set bit; if even, the position is even.

- **Reverse Bits of a Number**:

```cpp
unsigned int reverseBits(unsigned int n) {
    unsigned int result = 0;
    for (int i = 0; i < 32; ++i) {
        result <<= 1;
        result |= (n & 1);
        n >>= 1;
    }
    return result;
}
```

- **Explanation**: Iterate through each bit of n, build the result by shifting and adding the least significant bit of n, then shift n right.

- **Find the Only Number Appearing Odd Times**:

- **Problem**: In an array where all numbers appear an even number of times except one, find the number appearing an odd number of times.

```cpp
int findOddOccurring(const vector<int>& nums) {
    int result = 0;
    for (int num : nums) {
        result ^= num;
    }
    return result;
}
```

- **Explanation**: XOR cancels pairs (even occurrences), leaving the number with odd occurrences.

- **Check if Two Numbers Have Opposite Signs**:

```cpp
bool haveOppositeSigns(int a, int b) {
    return (a ^ b) < 0;
}
```

- **Explanation**: The sign bit (MSB) is 1 for negative numbers, 0 for positive. If a and b have opposite signs, their XOR will have a 1 in the MSB, making the result negative.

- **Add Two Numbers Without Arithmetic Operators**:

```cpp
int add(int a, int b) {
    while (b != 0) {
        int carry = a & b;
        a = a ^ b;
        b = carry << 1;
    }
    return a;
}
```

- **Explanation**:

  - `a ^ b` computes the sum without carry.
  - `a & b` computes the carry, shifted left by 1.
  - Repeat until no carry remains.

- **Multiply by 9 Using Bit Operations**:

```cpp
int multiplyBy9(int n) {
    return (n << 3) + n; // n * 8 + n = n * 9
}
```

- **Explanation**: Left shift by 3 multiplies by 8, then add n to get 9n.

- **Divide by 2 (Floor Division)**:

```cpp
int divideBy2(int n) {
    return n >> 1;
}
```

- **Explanation**: Right shift by 1 divides by 2, rounding down (e.g., 5 &gt;&gt; 1 = 2).

- **Find the Most Significant Set Bit (MSB)**:

```cpp
int findMSB(int n) {
    if (n == 0) return 0;
    int msb = 0;
    while (n != 0) {
        n >>= 1;
        msb++;
    }
    return 1 << (msb - 1);
}
```

- **Explanation**: Keep shifting right until n becomes 0, counting shifts to find the position of the MSB, then shift 1 to that position.

---

## Example: Subset Generation

- **Problem**: Generate all subsets of a set using bit manipulation.

```cpp
#include <vector>

vector<vector<int>> generateSubsets(const vector<int>& nums) {
    int n = nums.size();
    int total = 1 << n; // 2^n subsets
    vector<vector<int>> subsets;

    for (int mask = 0; mask < total; ++mask) {
        vector<int> subset;
        for (int i = 0; i < n; ++i) {
            if (mask & (1 << i)) {
                subset.push_back(nums[i]);
            }
        }
        subsets.push_back(subset);
    }
    return subsets;
}

int main() {
    vector<int> nums = {1, 2, 3};
    auto subsets = generateSubsets(nums);
    for (const auto& subset : subsets) {
        cout << "{ ";
        for (int x : subset) cout << x << " ";
        cout << "}\n";
    }
    // Output:
    // { }
    // { 1 }
    // { 2 }
    // { 1 2 }
    // { 3 }
    // { 1 3 }
    // { 2 3 }
    // { 1 2 3 }
}
```

---

## Best Practices

- **Implementation**:
  - Use unsigned integers for bit operations to avoid sign issues.
  - Comment bit manipulations for clarity (e.g., `n & 1 // check LSB`).
  - Test with edge cases (e.g., 0, INT_MAX, negative numbers).
- **Optimization**:
  - Use Brian Kernighan’s algorithm for counting set bits; faster than checking each bit.
  - Combine bit operations to reduce steps (e.g., `n & -n` to get the rightmost set bit).
  - Avoid unnecessary shifts; precompute masks if reused.
- **Debugging**:
  - Print binary representation to verify operations.
  - Use small numbers to test bit manipulations.
  - Check for overflow in shifts (e.g., shifting beyond 31 bits for int).

**Explanation**:

- Unsigned integers prevent unexpected behavior with sign bits.
- Optimization reduces the number of operations, crucial for performance.
- Debugging with binary output helps visualize bit changes.

---

## Cheat Codes

- **Quick Tips**:
  - `n & -n` gives the rightmost set bit.
  - `n & (n-1)` removes the rightmost set bit.
  - Use XOR to find unique elements or toggle bits.
  - `(n & (1 << k)) != 0` checks if the k-th bit is set.
  - `n | (1 << k)` sets the k-th bit.
- **Interview Questions**:
  - Find the single number in an array (XOR).
  - Check if a number is a power of 2 or 4.
  - Reverse bits of a number.
  - Add two numbers without arithmetic operators.

**Explanation**:

- Bit tricks provide O(1) solutions for many problems.
- XOR properties are powerful for problems involving pairs or uniqueness.
- Bit manipulation is a frequent interview topic for optimization problems.