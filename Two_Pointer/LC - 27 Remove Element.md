# Remove Element

## 🔗 Problem Link

https://leetcode.com/problems/remove-element/

## 🏷️ Tags

- Array
- Two Pointer

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in-place. Return the number of remaining elements. The order of the remaining elements does not matter.

## ✨ Examples

### Example 1

```text
Input: nums = [3,2,2,3], val = 3

Output: 2

Updated Array: [2,2]
```

### Example 2

```text
Input: nums = [0,1,2,2,3,0,4,2], val = 2

Output: 5

Updated Array: [0,1,4,0,3]
```

## 🚀 Approach

I used the **Two Pointer** approach.

- One pointer (`j`) is used to **read** every element in the array.
- Another pointer (`i`) is used to **write** only the elements that are not equal to `val`.
- If the current element is equal to `val`, the read pointer simply moves to the next element.
- Otherwise, the current element is copied to the write pointer position, and both pointers move forward.
- After traversing the entire array, `i` represents the number of remaining elements.

## 💻 Java Solution

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0, j = 0;

        while (j < nums.length) {
            if (nums[j] == val) {
                j++;
            } else {
                nums[i] = nums[j];
                i++;
                j++;
            }
        }

        return i;
    }
}
```

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The read pointer visits each element exactly once.

### Space Complexity

**O(1)**

- No extra data structure is used.

## 📌 Constraints

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

## 💡 Key Points

- Use two pointers.
- One pointer reads every element.
- One pointer writes only valid elements.
- Modify the array in-place.
- Return the write pointer as the answer.

## ⚠️ Common Mistakes

- Returning `j` instead of `i`.
- Moving the write pointer when the value is equal to `val`.
- Forgetting to return the count of remaining elements.
- Using an extra array when it is not required.