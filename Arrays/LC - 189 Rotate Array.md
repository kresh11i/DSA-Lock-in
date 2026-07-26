# Rotate Array

## 🔗 Problem Link

https://leetcode.com/problems/rotate-array/

## 🏷️ Tags

- Array
- Simulation

## 📚 Topics

- Array
- Math

## 📊 Difficulty

Medium

## 📖 Problem Statement

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

The rotation must modify the original array.

---

## ✨ Examples

### Example 1

```text
Input: nums = [1,2,3,4,5,6,7], k = 3

Output: [5,6,7,1,2,3,4]
```

### Example 2

```text
Input: nums = [-1,-100,3,99], k = 2

Output: [3,99,-1,-100]
```

---

## 🚀 Approach

### Pattern Used

**Array Index Mapping (Modulo Arithmetic)**

### Intuition

Instead of rotating the array one position at a time, directly calculate the new position of every element.

### Why This Approach Works

If an element is currently at index `i`, after rotating the array by `k` positions, its new index becomes:

```text
(i + k) % nums.length
```

The modulo (`%`) operator wraps the index back to the beginning whenever it exceeds the array size.

### Algorithm

1. Calculate the effective rotation using `k % nums.length`.
2. Create a temporary array of the same size.
3. Traverse the original array.
4. Calculate the new index of every element.
5. Store the element in the temporary array.
6. Copy the temporary array back to the original array.

---

## 💻 Java Solution

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        int temp [] = new int [ nums.length];

        for(int i = 0 ; i<nums.length ; i++){
            temp[(i+k)%nums.length] = nums[i];
        }

        for(int i = 0 ; i<nums.length; i++){
            nums[i] = temp[i];
        }
    }
}
```

---

## ⭐ Main Logic

```java
temp[(i + k) % nums.length] = nums[i];
```

### Why is this the Main Logic?

This single line performs the complete rotation.

- `(i + k)` moves the element `k` positions to the right.
- `% nums.length` wraps the index if it goes beyond the array length.
- The element is placed directly into its correct rotated position.

> **Interview Takeaway:**  
> Whenever an array rotates in a circular manner, think of **Modulo Arithmetic**.

---

## 🧪 Dry Run

### Input

```text
nums = [1,2,3,4,5,6,7]
k = 3
```

### Step 1

Calculate the effective rotation.

```text
k = 3 % 7 = 3
```

Create an empty temporary array.

```text
temp = [_,_,_,_,_,_,_]
```

### Step 2

| Current Index (i) | nums[i] | New Index `(i+k)%7` | temp Array |
|------------------:|:-------:|:-------------------:|:--------------------------:|
| 0 | 1 | 3 | [_,_,_,1,_,_,_] |
| 1 | 2 | 4 | [_,_,_,1,2,_,_] |
| 2 | 3 | 5 | [_,_,_,1,2,3,_] |
| 3 | 4 | 6 | [_,_,_,1,2,3,4] |
| 4 | 5 | 0 | [5,_,_,1,2,3,4] |
| 5 | 6 | 1 | [5,6,_,1,2,3,4] |
| 6 | 7 | 2 | [5,6,7,1,2,3,4] |

### Step 3

Copy the temporary array back.

```text
nums = [5,6,7,1,2,3,4]
```

### Final Output

```text
[5,6,7,1,2,3,4]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- One traversal to place the elements into the temporary array.
- One traversal to copy the elements back.
- Overall Time Complexity = **O(n)**.

### Space Complexity

**O(n)**

- An extra array of size `n` is used.

---

## 📌 Constraints

- `1 <= nums.length <= 10⁵`
- `-2³¹ <= nums[i] <= 2³¹ - 1`
- `0 <= k <= 10⁵`

---

## 💡 Key Points

- Calculate the effective rotation using `k % n`.
- Use modulo arithmetic for circular indexing.
- Every element gets a new position.
- Store rotated elements in a temporary array.
- Copy the temporary array back to the original array.
- Simple and easy-to-understand solution.

---

## ⚠️ Common Mistakes

- Forgetting to calculate `k % nums.length`.
- Forgetting to use modulo while calculating the new index.
- Not copying the temporary array back.
- Rotating the array one step at a time, resulting in a slower solution.

---

## 📝 Revision Snapshot

**Problem Type:** Array Manipulation

**Pattern Used:** Array Index Mapping (Modulo Arithmetic)

**Main Data Structure:** Array

**Main Formula:**

```text
New Index = (Current Index + k) % n
```

**Key Idea:**

Calculate the new position of every element using modulo arithmetic, store it in a temporary array, and finally copy the rotated array back.