# Missing Number

## 🔗 Problem Link

https://leetcode.com/problems/missing-number/

## 🏷️ Tags

- Array
- Bit Manipulation
- XOR

## 📚 Topics

- Array
- Hash Table
- Math
- Binary Search
- Bit Manipulation
- Sorting

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number that is missing from the array.

---

## ✨ Examples

### Example 1

```text
Input: nums = [3,0,1]

Output: 2
```

### Example 2

```text
Input: nums = [0,1]

Output: 2
```

### Example 3

```text
Input: nums = [9,6,4,2,3,5,7,0,1]

Output: 8
```

---

## 🚀 Approach

### Pattern Used

**Bit Manipulation (XOR)**

### Intuition

XOR has a special property:

- A number XOR itself becomes `0`.
- A number XOR `0` remains the same.

If we XOR all numbers from `0` to `n` and also XOR every element in the array, every matching number gets cancelled. The only remaining value is the missing number.

### Why This Approach Works

Every number appears exactly twice:

- Once from the range `0...n`
- Once from the given array

The missing number appears only once, so it remains after all XOR operations.

### Algorithm

1. Initialize two XOR variables.
2. XOR all elements of the array.
3. XOR all numbers from `1` to `n`.
4. XOR both results.
5. The remaining value is the missing number.

---

## 💻 Java Solution

```java
class Solution {
    public int missingNumber(int[] nums) {

        int n = nums.length;

        int xor1 = 0, xor2 = 0;

        for (int i = 0; i < nums.length; i++) {

            xor2 = xor2 ^ nums[i];
            xor1 = xor1 ^ (i + 1);

        }

        return xor1 ^ xor2;
    }
}
```

---

## ⭐ Main Logic

```java
xor2 = xor2 ^ nums[i];
xor1 = xor1 ^ (i + 1);

return xor1 ^ xor2;
```

### Why is this the Main Logic?

- `xor2` stores the XOR of all elements in the array.
- `xor1` stores the XOR of numbers from `1` to `n`.
- XORing both values cancels every common number.
- The remaining value is the missing number.

> **Interview Takeaway:**  
> Whenever every element appears exactly twice except one, think about using **XOR**.

---

## 🧪 Dry Run

### Input

```text
nums = [3,0,1]
```

### Initial State

```text
xor1 = 0
xor2 = 0
```

| i | nums[i] | xor2 | i+1 | xor1 |
|---|---------|------|-----|------|
|0|3|3|1|1|
|1|0|3|2|3|
|2|1|2|3|0|

### Final Step

```text
Answer = xor1 ^ xor2
       = 0 ^ 2
       = 2
```

### Final Output

```text
2
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The array is traversed only once.

### Space Complexity

**O(1)**

- Only two integer variables are used.

---

## 📌 Constraints

- `n == nums.length`
- `1 <= n <= 10⁴`
- `0 <= nums[i] <= n`
- All numbers are unique.

---

## 💡 Key Points

- XOR of the same numbers becomes `0`.
- XOR with `0` gives the same number.
- No sorting is required.
- No extra array or HashMap is needed.
- One traversal is enough.
- Uses constant extra space.

---

## ⚠️ Common Mistakes

- Using `i` instead of `i + 1`.
- Forgetting to XOR the array elements.
- Confusing XOR (`^`) with exponentiation.
- Using addition instead of XOR.

---

## 📝 Revision Snapshot

**Problem Type:** Missing Element

**Pattern Used:** Bit Manipulation (XOR)

**Main Data Structure:** Integer

**Main Formula:**

```text
a ^ a = 0
a ^ 0 = a

Missing Number = XOR(1...n) ^ XOR(array)
```

**Key Idea:**

XOR all numbers from `1` to `n` and XOR all array elements. Every common number gets cancelled, leaving only the missing number.