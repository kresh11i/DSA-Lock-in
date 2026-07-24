# Move Zeroes

## 🔗 Problem Link

https://leetcode.com/problems/move-zeroes/

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

Given an integer array `nums`, move all `0`s to the end of the array while maintaining the relative order of the non-zero elements. The operation must be performed in-place.

## ✨ Examples

### Example 1

```text
Input: nums = [0,1,0,3,12]

Output: [1,3,12,0,0]
```

### Example 2

```text
Input: nums = [0]

Output: [0]
```

## 🚀 Approach

The idea is to use the **Two Pointer** technique.

- One pointer (`j`) is used to read every element in the array.
- Another pointer (`i`) is used to write only the non-zero elements.
- If the current element is `0`, only the read pointer moves.
- If the current element is non-zero, copy it to the write pointer position and move both pointers.
- After all non-zero elements are placed at the beginning, fill the remaining positions with `0`.
- This keeps the relative order of all non-zero elements while modifying the array in-place.

## 💻 Java Solution

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int i = 0, j = 0;
        while(j < nums.length){
            if(nums[j] == 0){
                j++;
            }else{
                nums[i] = nums[j];
                i++;
                j++;
            }
        }
        for(int k = i; k < nums.length; k++){
            nums[k] = 0;
        }
    }
}
```

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The array is traversed once, and the remaining positions are filled with zeroes. Overall complexity is **O(n)**.

### Space Complexity

**O(1)**

- No extra data structure is used.

## 📌 Constraints

- `1 <= nums.length <= 10⁴`
- `-2³¹ <= nums[i] <= 2³¹ - 1`

## 💡 Key Points

- Use two pointers.
- One pointer reads every element.
- One pointer writes only non-zero elements.
- Fill the remaining positions with `0`.
- Maintain the relative order of non-zero elements.
- Solve the problem in-place.

## ⚠️ Common Mistakes

- Forgetting to fill the remaining positions with `0`.
- Using an extra array instead of modifying the original array.
- Incrementing the write pointer for zero values.
- Changing the order of non-zero elements.

## 📝 Revision Snapshot

**Problem Type:** Two Pointer

**Pattern Used:** Read Pointer & Write Pointer

**Main Data Structure:** Array

**Key Idea:** Read every element using one pointer, write only the non-zero elements using another pointer, and finally fill the remaining positions with zeroes.