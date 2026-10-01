**📁 Folder:** `Arrays`

**File Name:** `LC - 189 Rotate Array.md`

# 🧩 Rotate Array

## 🔗 Problem

[LeetCode 189 — Rotate Array](https://leetcode.com/problems/rotate-array/)

---

## 🏷️ Tags

`Array` `Two Pointer` `In-Place` `Reverse`

## 📚 Topics

* Array manipulation
* In-place reversal
* Two pointers
* Rotation

## 📊 Difficulty

**Medium**

---

## 💡 Intuition

We need to rotate the array to the **right by `k` positions**.

For example:

```text
nums = [1, 2, 3, 4, 5, 6, 7]
k = 3
```

Expected:

```text
[5, 6, 7, 1, 2, 3, 4]
```

Instead of shifting elements one by one, we can use the **reverse technique**.

### The trick

For `k = 3`:

### Step 1 — Reverse the entire array

```text
[1, 2, 3, 4, 5, 6, 7]
              ↓
[7, 6, 5, 4, 3, 2, 1]
```

### Step 2 — Reverse the first `k` elements

```text
[7, 6, 5 | 4, 3, 2, 1]
      ↓
[5, 6, 7 | 4, 3, 2, 1]
```

### Step 3 — Reverse the remaining elements

```text
[5, 6, 7 | 4, 3, 2, 1]
             ↓
[5, 6, 7 | 1, 2, 3, 4]
```

Final answer:

```text
[5, 6, 7, 1, 2, 3, 4]
```

---

## 🧠 Thought Process

There are two important things to understand.

### 1. Why `k = k % nums.length`?

```java
k = k % nums.length;
```

If the array has `7` elements:

```text
k = 7
```

rotating by 7 positions gives the same array.

```text
k = 8
```

is the same as rotating by 1.

So:

```text
8 % 7 = 1
```

This avoids unnecessary rotations.

---

### 2. Why three reversals?

Suppose:

```text
[1 2 3 4 | 5 6 7]
```

We want:

```text
[5 6 7 | 1 2 3 4]
```

First reverse everything:

```text
[7 6 5 | 4 3 2 1]
```

Then reverse the first `k`:

```text
[5 6 7 | 4 3 2 1]
```

Then reverse the remaining part:

```text
[5 6 7 | 1 2 3 4]
```

That's exactly the required rotation.

---

## 🔍 Dry Run

### Input

```text
nums = [1, 2, 3, 4, 5, 6, 7]
k = 3
```

### Step 1

```java
k = k % nums.length;
```

```text
3 % 7 = 3
```

---

### Step 2 — Reverse entire array

```java
reverse(nums, 0, nums.length - 1);
```

Before:

```text
[1, 2, 3, 4, 5, 6, 7]
```

After:

```text
[7, 6, 5, 4, 3, 2, 1]
```

---

### Step 3 — Reverse first `k` elements

```java
reverse(nums, 0, k - 1);
```

Here:

```text
k - 1 = 2
```

So reverse indices `0 → 2`.

Before:

```text
[7, 6, 5, 4, 3, 2, 1]
```

After:

```text
[5, 6, 7, 4, 3, 2, 1]
```

---

### Step 4 — Reverse remaining elements

```java
reverse(nums, k, nums.length - 1);
```

That means:

```text
reverse(nums, 3, 6)
```

Before:

```text
[5, 6, 7, 4, 3, 2, 1]
```

After:

```text
[5, 6, 7, 1, 2, 3, 4]
```

✅ Final answer.

---

## ⭐ Main Logic

The entire algorithm is:

```java
k = k % nums.length;

reverse(nums, 0, nums.length - 1);
reverse(nums, 0, k - 1);
reverse(nums, k, nums.length - 1);
```

Think of it as:

```text
Reverse ALL
    ↓
Reverse first K
    ↓
Reverse remaining
    ↓
Rotated array
```

---

## 💻 Java Solution

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;

        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    public void reverse(int[] nums, int left, int right) {

        while (left < right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;

            left++;
            right--;
        }
    }
}
```

---

## 🎯 Key Pattern

### Array Rotation Using Reversal

Whenever you see:

> **Rotate an array to the right by `k`**

Think:

```text
k = k % n

Reverse entire array
Reverse first k
Reverse remaining n-k
```

---

## ⏱️ Complexity

### Time — `O(n)`

We reverse the array three times.

```text
O(n) + O(k) + O(n-k)
= O(n)
```

### Space — `O(1)`

The array is modified **in-place** and only a temporary variable is used for swapping.

---

## 📌 Key Takeaways

* `k % n` handles rotations larger than the array size.
* The solution uses **three reversals**.
* The helper `reverse()` uses the **two-pointer technique**.
* The array is modified in-place.
* No extra array is required.
* Pattern: **Reverse → Reverse → Reverse**.
