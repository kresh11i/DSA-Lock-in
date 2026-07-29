# Rearrange Array Elements by Sign

## 🔗 Problem Link

https://leetcode.com/problems/rearrange-array-elements-by-sign/

## 🏷️ Tags

- Array

## 📚 Topics

- Array
- Two Pointers
- Simulation

## 📊 Difficulty

Medium

## 📖 Problem Statement

You are given an integer array `nums` of even length containing an equal number of positive and negative integers.

Rearrange the array such that:

- Positive and negative numbers appear alternately.
- The array starts with a positive number.
- The relative order of positive numbers and negative numbers remains the same.

Return the rearranged array.

---

## ✨ Examples

### Example 1

```text
Input: nums = [3,1,-2,-5,2,-4]

Output: [3,-2,1,-5,2,-4]
```

### Example 2

```text
Input: nums = [-1,1]

Output: [1,-1]
```

---

## 🚀 Approach

### Pattern Used

**Two Pointers (Index Placement)**

### Intuition

Since the array length is always **even**, there will always be an equal number of positive and negative numbers.

We create a new answer array.

- Positive numbers are placed at **even indices** (`0, 2, 4, ...`).
- Negative numbers are placed at **odd indices** (`1, 3, 5, ...`).

To keep track of these positions, we use two pointers:

- `positiveIndex`
- `negativeIndex`

After placing a number, the corresponding pointer is increased by **2**, so it always points to the next valid even or odd index.

This also preserves the original order of positive and negative numbers.

---

### Why This Approach Works

- Every positive number is stored only in an even index.
- Every negative number is stored only in an odd index.
- Since the pointers move by **2**, they always stay on their correct positions.
- Traversing the array only once keeps the solution efficient.

---

### Algorithm

1. Create an answer array of the same size.
2. Initialize `positiveIndex = 0`.
3. Initialize `negativeIndex = 1`.
4. Traverse the original array.
5. If the current number is positive, place it at `positiveIndex` and increment it by `2`.
6. Otherwise, place it at `negativeIndex` and increment it by `2`.
7. Return the answer array.

---

## 💻 Java Solution

```java
class Solution {
    public int[] rearrangeArray(int[] nums) {

        int i = 0;
        int positiveIndex = 0;
        int negativeIndex = 1;
        int[] ans = new int[nums.length];

        while (i < nums.length) {

            if (nums[i] > 0) {
                ans[positiveIndex] = nums[i];
                positiveIndex += 2;
                i++;
            } else {
                ans[negativeIndex] = nums[i];
                i++;
                negativeIndex += 2;
            }
        }

        return ans;
    }
}
```

---

## ⭐ Main Logic

```java
if (nums[i] > 0) {
    ans[positiveIndex] = nums[i];
    positiveIndex += 2;
} else {
    ans[negativeIndex] = nums[i];
    negativeIndex += 2;
}
```

### Why is this the Main Logic?

This block decides where each number should be placed.

- Positive numbers always go to even indices.
- Negative numbers always go to odd indices.
- Increasing the index by `2` ensures that the next positive or negative number is placed in the correct position.

> **Interview Takeaway:**  
> When elements have fixed positions (even index, odd index, etc.), maintain separate pointers for each position.

---

## 🧪 Dry Run

### Input

```text
nums = [3,1,-2,-5,2,-4]
```

Initially,

```text
positiveIndex = 0
negativeIndex = 1

ans = [_,_,_,_,_,_]
```

| Current Number | Action | Answer Array |
|---------------:|--------|--------------|
|3|Place at index 0|[3,_,_,_,_,_]|
|1|Place at index 2|[3,_,1,_,_,_]|
|-2|Place at index 1|[3,-2,1,_,_,_]|
|-5|Place at index 3|[3,-2,1,-5,_,_]|
|2|Place at index 4|[3,-2,1,-5,2,_]|
|-4|Place at index 5|[3,-2,1,-5,2,-4]|

### Final Output

```text
[3,-2,1,-5,2,-4]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The array is traversed only once.

### Space Complexity

**O(n)**

- An extra answer array is used.

---

## 📌 Constraints

- `2 <= nums.length <= 2 × 10⁵`
- `nums.length` is even.
- Half of the integers are positive.
- Half of the integers are negative.

---

## 💡 Key Points

- Array length is always even.
- Positive numbers always go to even indices.
- Negative numbers always go to odd indices.
- Increase both pointers by `2`.
- The original order of positive and negative numbers is preserved.
- Traverse the array only once.

---

## ⚠️ Common Mistakes

- Incrementing the indices by `1` instead of `2`.
- Starting `negativeIndex` from `0` instead of `1`.
- Forgetting to preserve the original order.
- Using the same pointer for both positive and negative numbers.

---

## 📝 Revision Snapshot

**Problem Type:** Rearranging Array

**Pattern Used:** Two Pointers (Index Placement)

**Main Data Structure:** Array

**Main Logic:**

```text
Positive Number ➜ Even Index (0,2,4...)

Negative Number ➜ Odd Index (1,3,5...)

positiveIndex += 2
negativeIndex += 2
```

**Key Idea:**

Use two separate pointers to track the next available even and odd positions in the answer array. Place positive numbers at even indices and negative numbers at odd indices while preserving their original order.