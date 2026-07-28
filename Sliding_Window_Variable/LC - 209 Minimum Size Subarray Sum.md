# Minimum Size Subarray Sum

## 🔗 Problem Link

https://leetcode.com/problems/minimum-size-subarray-sum/

## 🏷️ Tags

- Array
- Sliding Window

## 📚 Topics

- Array
- Binary Search
- Sliding Window
- Prefix Sum

## 📊 Difficulty

Medium

## 📖 Problem Statement

Given an array of positive integers `nums` and a positive integer `target`, return the **minimum length** of a subarray whose sum is **greater than or equal to** `target`.

If there is no such subarray, return `0`.

---

## ✨ Examples

### Example 1

```text
Input: target = 7, nums = [2,3,1,2,4,3]

Output: 2
```

### Example 2

```text
Input: target = 4, nums = [1,4,4]

Output: 1
```

### Example 3

```text
Input: target = 11, nums = [1,1,1,1,1,1,1,1]

Output: 0
```

---

## 🚀 Approach

### Pattern Used

**Variable Sliding Window**

### What is Variable Sliding Window?

Variable Sliding Window is a technique used to solve problems involving **continuous subarrays**.

Instead of checking every possible subarray, we maintain a **window** using two pointers.

- **Left Pointer** → Start of the current window.
- **Right Pointer** → End of the current window.

The window size is **not fixed**.

It keeps increasing and decreasing based on the problem's condition.

There are only **two operations**.

### 1. Expand the Window ➜

Move the **right pointer** to include more elements.

We expand the window when the current sum is **less than the target**.

```text
Current Sum < Target
```

Since the sum is not enough, we include another element.

```java
right++;
sum += nums[right];
```

---

### 2. Shrink the Window ⬅

Move the **left pointer** to remove elements.

We shrink the window when the current sum is **greater than or equal to the target**.

```text
Current Sum >= Target
```

Since we already have a valid subarray, we try removing elements from the left to see whether we can get a **smaller valid subarray**.

```java
sum -= nums[left];
left++;
```

---

### Sliding Window Flow

```text
Current Sum < Target
        │
        ▼
Expand Right ➜

Current Sum >= Target
        │
        ▼
Update Minimum Length
Shrink Left ⬅
```

---

### Intuition

We need the **smallest subarray** whose sum is at least the target.

So,

- Keep expanding the window until the sum becomes large enough.
- Once the condition is satisfied, record the current window length.
- Then keep shrinking the window from the left as long as the condition is still true.
- This helps us find the minimum possible window.

---

### Why This Approach Works

Since every element in the array is **positive**,

- Expanding the window always increases the sum.
- Shrinking the window always decreases the sum.

Because of this property, we never need to move the pointers backwards.

Each element enters the window once and leaves the window once, making the solution efficient.

---

### Algorithm

1. Initialize `left`, `right`, `sum` and `minLength`.
2. Expand the window by moving the right pointer.
3. Keep adding elements to the sum.
4. Once `sum >= target`, update the minimum length.
5. Shrink the window from the left.
6. Continue until the right pointer reaches the end.
7. Return `0` if no valid subarray exists.

---

## 💻 Java Solution

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {

        int left = 0;
        int right = 0;
        int sum = nums[0];
        int maxLen = Integer.MAX_VALUE;
        int n = nums.length;

        while (right < n) {

            while (left <= right && sum >= target) {

                maxLen = Math.min(maxLen, right - left + 1);
                sum -= nums[left];

                left++;
            }

            right++;

            if (right < n) {
                sum += nums[right];
            }
        }

        return maxLen == Integer.MAX_VALUE ? 0 : maxLen;
    }
}
```

---

## ⭐ Main Logic

```java
while (left <= right && sum >= target) {

    maxLen = Math.min(maxLen, right - left + 1);

    sum -= nums[left];
    left++;
}
```

### Why is this the Main Logic?

This loop is the heart of the Sliding Window algorithm.

- The window has already reached the target.
- First, update the minimum length.
- Then remove elements from the left.
- Continue shrinking until the window is no longer valid.

> **Interview Takeaway:**  
> In Variable Sliding Window problems, **whenever the window satisfies the condition, update the answer first and then shrink the window.**

---

## 🧪 Dry Run

### Input

```text
target = 7

nums = [2,3,1,2,4,3]
```

| Left | Right | Window | Sum | Action | Minimum Length |
|-----:|------:|--------|----:|--------|---------------:|
|0|0|[2]|2|Expand|∞|
|0|1|[2,3]|5|Expand|∞|
|0|2|[2,3,1]|6|Expand|∞|
|0|3|[2,3,1,2]|8|Update & Shrink|4|
|1|3|[3,1,2]|6|Expand|4|
|1|4|[3,1,2,4]|10|Update & Shrink|4|
|2|4|[1,2,4]|7|Update & Shrink|3|
|3|4|[2,4]|6|Expand|3|
|3|5|[2,4,3]|9|Update & Shrink|3|
|4|5|[4,3]|7|Update & Shrink|2|
|5|5|[3]|3|Stop|2|

### Final Output

```text
2
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- Each element enters the window once and leaves the window once.

### Space Complexity

**O(1)**

- Only a few integer variables are used.

---

## 📌 Constraints

- `1 <= target <= 10⁹`
- `1 <= nums.length <= 10⁵`
- `1 <= nums[i] <= 10⁴`

---

## 💡 Key Points

- Use **Variable Sliding Window**.
- Expand while the sum is less than the target.
- Shrink while the sum is greater than or equal to the target.
- Update the answer before shrinking.
- Works because all elements are positive.
- Both pointers move only forward.

---

## ⚠️ Common Mistakes

- Shrinking before updating the answer.
- Forgetting to subtract `nums[left]`.
- Moving the right pointer before processing the current window.
- Using Sliding Window when the array contains negative numbers.
- Returning `Integer.MAX_VALUE` instead of `0` when no valid subarray exists.

---

## 📝 Revision Snapshot

**Problem Type:** Minimum Length Subarray

**Pattern Used:** Variable Sliding Window

**Main Data Structure:** Array

**Main Condition:**

```text
If Sum < Target
    Expand Right ➜

If Sum >= Target
    Update Answer
    Shrink Left ⬅
```

**Key Idea:**

Maintain a variable-sized window. Expand until the target is reached, then shrink it to find the smallest valid subarray.