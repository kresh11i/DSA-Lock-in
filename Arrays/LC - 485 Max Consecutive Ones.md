# Max Consecutive Ones

## 🔗 Problem Link

https://leetcode.com/problems/max-consecutive-ones/

## 🏷️ Tags

- Array

## 📚 Topics

- Array

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given a binary array `nums`, return the maximum number of consecutive `1`s in the array.

---

## ✨ Examples

### Example 1

```text
Input: nums = [1,1,0,1,1,1]

Output: 3
```

### Example 2

```text
Input: nums = [1,0,1,1,0,1]

Output: 2
```

---

## 🚀 Approach

### Pattern Used

**Array Traversal**

### Intuition

Traverse the array from left to right.

- If the current element is `1`, increase the current count.
- Update the maximum count whenever the current count becomes larger.
- If the current element is `0`, reset the current count to `0`.

At the end of the traversal, the maximum count will be the answer.

### Why This Approach Works

The variable `cnt` keeps track of the current consecutive sequence of `1`s.

Whenever a `0` is found, the sequence breaks, so `cnt` is reset.

The variable `max` stores the longest sequence found during the traversal.

### Algorithm

1. Initialize `cnt = 0` and `max = 0`.
2. Traverse the array.
3. If the current element is `1`, increment `cnt`.
4. Update `max` if `cnt` becomes larger.
5. If the current element is `0`, reset `cnt` to `0`.
6. Return `max`.

---

## 💻 Java Solution

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int max = 0;
        int cnt = 0;

        for (int i = 0; i < nums.length; i++) {

            if (nums[i] == 1) {

                cnt++;

                if (cnt > max) {
                    max = cnt;
                }

            } else {

                cnt = 0;

            }

        }

        return max;
    }
}
```

---

## ⭐ Main Logic

```java
cnt++;

if (cnt > max) {
    max = cnt;
}
```

### Why is this the Main Logic?

- `cnt` stores the current consecutive sequence of `1`s.
- Every time a `1` is found, increase the count.
- Compare it with `max`.
- If the current sequence is larger, update the maximum.

> **Interview Takeaway:**  
> Whenever a problem asks for the **longest consecutive sequence**, maintain a running count and update the maximum whenever needed.

---

## 🧪 Dry Run

### Input

```text
nums = [1,1,0,1,1,1]
```

| Index | Value | cnt | max |
|------:|:-----:|----:|----:|
|0|1|1|1|
|1|1|2|2|
|2|0|0|2|
|3|1|1|2|
|4|1|2|2|
|5|1|3|3|

### Final Output

```text
3
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

- `1 <= nums.length <= 10⁵`
- `nums[i]` is either `0` or `1`

---

## 💡 Key Points

- Traverse the array only once.
- Maintain the current consecutive count.
- Reset the count whenever `0` appears.
- Update the maximum count whenever needed.
- No extra data structure is required.

---

## ⚠️ Common Mistakes

- Forgetting to reset `cnt` after encountering `0`.
- Updating `max` outside the `1` condition.
- Returning `cnt` instead of `max`.
- Using nested loops unnecessarily.

---

## 📝 Revision Snapshot

**Problem Type:** Array Traversal

**Pattern Used:** Running Count

**Main Data Structure:** Array

**Main Logic:**

```text
If nums[i] == 1
    cnt++
    max = max(max, cnt)
Else
    cnt = 0
```

**Key Idea:**

Keep counting consecutive `1`s. Whenever a `0` appears, reset the count. Track the maximum count throughout the traversal.