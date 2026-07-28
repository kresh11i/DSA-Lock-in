# Single Number

## 🔗 Problem Link

https://leetcode.com/problems/single-number/

## 🏷️ Tags

- Array
- Bit Manipulation
- XOR

## 📚 Topics

- Array
- Bit Manipulation

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single element.

Your solution must have a linear runtime complexity and use only constant extra space.

---

## ✨ Examples

### Example 1

```text
Input: nums = [2,2,1]

Output: 1
```

### Example 2

```text
Input: nums = [4,1,2,1,2]

Output: 4
```

### Example 3

```text
Input: nums = [1]

Output: 1
```

---

## 🚀 Approach

### Pattern Used

**Bit Manipulation (XOR)**

### Intuition

Every number appears exactly twice except one.

Using the XOR (`^`) operator, identical numbers cancel each other.

After XORing all the elements, only the unique element remains.

### Why This Approach Works

XOR has two important properties:

- `a ^ a = 0`
- `a ^ 0 = a`

When all elements are XORed together:

- Duplicate numbers become `0`.
- Only the number that appears once remains.

### Algorithm

1. Initialize `xor = 0`.
2. Traverse the array.
3. XOR every element with `xor`.
4. Return the final value of `xor`.

---

## 💻 Java Solution

```java
class Solution {
    public int singleNumber(int[] nums) {

        int xor = 0;

        for(int i = 0; i < nums.length; i++){

            xor = xor ^ nums[i];

        }

        return xor;
    }
}
```

---

## ⭐ Main Logic

```java
xor = xor ^ nums[i];
```

### Why is this the Main Logic?

Each element is XORed with the current result.

- Duplicate elements cancel each other.
- Only the unique element remains after the loop finishes.

> **Interview Takeaway:**  
> Whenever every element appears twice except one, think of using **XOR**.

---

## 🧪 Dry Run

### Input

```text
nums = [4,1,2,1,2]
```

### Initial State

```text
xor = 0
```

| Step | Current Number | XOR Calculation | xor |
|------|----------------|-----------------|-----|
|1|4|0 ^ 4|4|
|2|1|4 ^ 1|5|
|3|2|5 ^ 2|7|
|4|1|7 ^ 1|6|
|5|2|6 ^ 2|4|

### Final Output

```text
4
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The array is traversed only once.

### Space Complexity

**O(1)**

- Only one integer variable is used.

---

## 📌 Constraints

- `1 <= nums.length <= 3 × 10⁴`
- `-3 × 10⁴ <= nums[i] <= 3 × 10⁴`
- Every element appears twice except one.

---

## 💡 Key Points

- XOR of the same numbers is `0`.
- XOR with `0` gives the same number.
- Traverse the array only once.
- No extra array or HashMap is required.
- Constant extra space.
- Very common Bit Manipulation interview problem.

---

## ⚠️ Common Mistakes

- Confusing XOR (`^`) with exponentiation.
- Using addition instead of XOR.
- Sorting the array unnecessarily.
- Using a HashMap when constant space is required.

---

## 📝 Revision Snapshot

**Problem Type:** Unique Element

**Pattern Used:** Bit Manipulation (XOR)

**Main Data Structure:** Integer

**Main Formula:**

```text
a ^ a = 0
a ^ 0 = a
```

**Main Logic:**

```text
xor = xor ^ nums[i]
```

**Key Idea:**

XOR every element in the array. Duplicate elements cancel each other, leaving only the number that appears once.