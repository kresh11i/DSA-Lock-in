# Check if Array Is Sorted and Rotated

## 🔗 Problem Link

https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/

## 🏷️ Tags

- Array
- Traversal
- Simulation

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given an integer array `nums`, return `true` if the array was originally sorted in non-decreasing order and then rotated some number of times. Otherwise, return `false`.

## ✨ Examples

### Example 1

```text
Input: nums = [3,4,5,1,2]
Output: true
```

### Example 2

```text
Input: nums = [2,1,3,4]
Output: false
```

### Example 3

```text
Input: nums = [1,2,3]
Output: true
```

## 🚀 Approach

The idea is to count how many times the sorted order breaks.

- Traverse the array from left to right.
- If the current element is smaller than the previous element, increase the count.
- After the loop, compare the last element with the first element.
- If the last element is greater than the first element, it means there is one more break in the circular order.
- If the total number of breaks is more than one, the array cannot be sorted and rotated.
- Otherwise, return `true`.

## 💻 Java Solution

```java
class Solution {
    public boolean check(int[] nums) {

        int cnt = 0;
        for(int i = 1 ;i<nums.length ; i++){
            if(nums[i] < nums[i-1]){
                cnt++;
            }

        }
        if(nums[nums.length-1] > nums[0]){
            cnt++;
        }
        return cnt <= 1;
    }
}
```

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The array is traversed only once.

### Space Complexity

**O(1)**

- No extra space is used.

## 📌 Constraints

- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`

## 💡 Key Points

- Count the number of order breaks.
- A valid sorted and rotated array can have at most one break.
- Don't forget to check the last and first elements.
- Traverse the array only once.
- No extra space is required.

## ⚠️ Common Mistakes

- Forgetting to compare the last and first elements.
- Using `>=` instead of `>`.
- Returning `true` without checking all breaks.
- Counting breaks incorrectly.

## 📝 Revision Snapshot

**Problem Type:** Array Traversal

**Pattern Used:** Count Order Breaks

**Main Data Structure:** Array

**Key Idea:** Count how many times the array becomes smaller than the previous element. If the total breaks are at most one (including the circular check), the array is sorted and rotated.