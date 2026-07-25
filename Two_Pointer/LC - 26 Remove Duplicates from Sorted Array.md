# Remove Duplicates from Sorted Array

## 🔗 Problem Link

https://leetcode.com/problems/remove-duplicates-from-sorted-array/

## 🏷️ Tags

- Array
- Two Pointer
- In-Place

## 📚 Topics

- Array
- Two Pointers

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given a sorted integer array `nums`, remove the duplicate elements in-place such that each unique element appears only once. Return the number of unique elements.

The relative order of the elements should be maintained, and no extra array should be used.

## ✨ Examples

### Example 1

```text
Input: nums = [1,1,2]

Output: 2

Updated Array: [1,2,_]
```

### Example 2

```text
Input: nums = [0,0,1,1,1,2,2,3,3,4]

Output: 5

Updated Array: [0,1,2,3,4,_,_,_,_,_]
```

## 🚀 Approach

The idea is to use the **Two Pointer** technique.

- One pointer (`j`) is used to read every element in the array.
- Another pointer (`i`) is used to keep track of the position where the next unique element should be placed.
- Since the array is already sorted, duplicate elements will always be next to each other.
- If the current element is the same as the previous unique element, move only the read pointer.
- If it is a new unique element, move the write pointer, copy the value, and increase the count of unique elements.
- After traversing the array, return the total number of unique elements.

## 💻 Java Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0, j = 1, k = 1;
        while (j < nums.length) {
            if (nums[i] == nums[j]) {
                j++;
            } else if (nums[i] != nums[j]) {
                i++;
                nums[i] = nums[j];

                j++;
                k++;
            }
        }

        return k;
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

- `1 <= nums.length <= 3 × 10⁴`
- `-100 <= nums[i] <= 100`
- `nums` is sorted in non-decreasing order.

## 💡 Key Points

- The array is already sorted.
- Duplicate elements are adjacent.
- Use two pointers to avoid extra space.
- Copy only unique elements.
- Return the number of unique elements.

## ⚠️ Common Mistakes

- Forgetting that the array is already sorted.
- Returning the array length instead of the unique count.
- Incrementing the write pointer for duplicate elements.
- Using an extra array instead of modifying the original array.

## 📝 Revision Snapshot

**Problem Type:** Two Pointer

**Pattern Used:** Read Pointer & Write Pointer

**Main Data Structure:** Array

**Key Idea:** Traverse the sorted array using one pointer and copy only unique elements using another pointer. Since duplicates are adjacent, comparing consecutive elements is enough.