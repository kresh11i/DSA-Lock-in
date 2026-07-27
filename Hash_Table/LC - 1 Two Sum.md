# Two Sum

## 🔗 Problem Link

https://leetcode.com/problems/two-sum/

## 🏷️ Tags

- Array
- Brute Force

## 📚 Topics

- Array
- Hash Table

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input has exactly one solution, and you may not use the same element twice.

The answer can be returned in any order.

---

## ✨ Examples

### Example 1

```text
Input: nums = [2,7,11,15], target = 9

Output: [0,1]
```

### Example 2

```text
Input: nums = [3,2,4], target = 6

Output: [1,2]
```

### Example 3

```text
Input: nums = [3,3], target = 6

Output: [0,1]
```

---

## 🚀 Approach

### Pattern Used

**Brute Force (Nested Loops)**

### Intuition

The simplest way is to check every possible pair in the array.

For each element, compare it with every remaining element. If their sum equals the target, store their indices and return the answer.

### Why This Approach Works

Since every possible pair is checked exactly once, the correct pair will always be found.

Although this method is not efficient, it is easy to understand and is usually the first solution that comes to mind.

### Algorithm

1. Traverse the array using the first loop.
2. Traverse the remaining elements using the second loop.
3. Add the two numbers.
4. If the sum equals the target, store both indices.
5. Return the answer.

---

## 💻 Java Solution

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        int[] arr = new int[2];

        for(int i = 0; i < nums.length; i++){

            for(int j = i + 1; j < nums.length; j++){

                if(nums[i] + nums[j] == target){
                    arr[0] = i;
                    arr[1] = j;
                }

            }
        }

        return arr;
    }
}
```

---

## ⭐ Main Logic

```java
if(nums[i] + nums[j] == target){
    arr[0] = i;
    arr[1] = j;
}
```

### Why is this the Main Logic?

This condition checks whether the current pair adds up to the target.

If the condition becomes true, both indices are stored as the answer.

> **Interview Takeaway:**  
> Brute Force is the easiest solution. It checks every possible pair, but it performs many unnecessary comparisons.

---

## 🧪 Dry Run

### Input

```text
nums = [2,7,11,15]
target = 9
```

### Step 1

Start with

```text
i = 0
```

Now compare it with every remaining element.

| i | j | nums[i] | nums[j] | Sum | Match |
|---|---|----------|----------|-----|-------|
|0|1|2|7|9|✅ Yes|

Store the indices.

```text
arr[0] = 0
arr[1] = 1
```

Return

```text
[0,1]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n²)**

- The outer loop runs `n` times.
- The inner loop checks the remaining elements.
- Every possible pair is checked.

### Space Complexity

**O(1)**

- Only the answer array is used.
- No extra data structure is required.

---

## 📌 Constraints

- `2 <= nums.length <= 10⁴`
- `-10⁹ <= nums[i] <= 10⁹`
- `-10⁹ <= target <= 10⁹`
- Exactly one valid answer exists.

---

## 💡 Key Points

- Check every possible pair.
- Use two nested loops.
- Return the indices, not the values.
- Easy to understand but not efficient.
- Good starting approach before optimization.

---

## ⚠️ Common Mistakes

- Starting the inner loop from `0` instead of `i + 1`.
- Using the same element twice.
- Returning the values instead of the indices.
- Forgetting to stop after finding the answer.

---

## 📝 Revision Snapshot

**Problem Type:** Pair Sum

**Pattern Used:** Brute Force (Nested Loops)

**Main Data Structure:** Array

**Main Logic:**

```text
Check every possible pair.
If nums[i] + nums[j] == target,
return the indices.
```

**Key Idea:**

Compare every pair of elements using two nested loops. If the sum equals the target, return their indices.