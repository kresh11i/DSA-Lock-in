# Next Permutation

## 🔗 Problem Link

https://leetcode.com/problems/next-permutation/

## 🏷️ Tags

- Array
- Two Pointers

## 📚 Topics

- Array
- Two Pointers

## 📊 Difficulty

Medium

## 📖 Problem Statement

A permutation of an array is an arrangement of its elements.

Given an array of integers `nums`, rearrange it into the **next lexicographically greater permutation**.

If such an arrangement is not possible, rearrange it into the **lowest possible order (ascending order)**.

The replacement must be **in-place** and use only **constant extra memory**.

---

## ✨ Examples

### Example 1

```text
Input: nums = [1,2,3]

Output: [1,3,2]
```

### Example 2

```text
Input: nums = [3,2,1]

Output: [1,2,3]
```

### Example 3

```text
Input: nums = [1,1,5]

Output: [1,5,1]
```

---

## 🚀 Approach

### Pattern Used

**Two Pointers + Array Traversal + Reverse**

### Intuition

To get the next permutation, we first need to find the first position from the right where the order starts increasing.

This position is called the **pivot**.

- If no pivot exists, the array is already the largest permutation.
- Otherwise, swap the pivot with the smallest greater element on its right.
- Finally, reverse the remaining suffix to obtain the smallest possible arrangement after the pivot.

---

### Why This Approach Works

The suffix after the pivot is always in **descending order**.

So,

- The first element greater than the pivot while traversing from right to left is automatically the **least greater element**.
- After swapping, the suffix is still in descending order.
- Reversing it converts it into ascending order, giving the next lexicographical permutation.

---

### Algorithm

1. Traverse the array from **right to left** using `i--`.
2. Find the **break point (pivot)** where `nums[i] < nums[i + 1]`.
3. Initialize `pivot = -1`.
4. If the pivot is still `-1`, reverse the entire array using two pointers and return.
5. Otherwise, traverse from the end of the array towards the pivot and find the **first element greater than the pivot**.
6. Swap that element with the pivot.
7. Reverse all the remaining elements after the pivot using two pointers.

---

## 💻 Java Solution

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;
        int pivot = -1;

        for (int i = n - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                pivot = i;
                break;
            }
        }

        if (pivot == -1) {
            int L = 0, R = n - 1;
            while (L < R) {
                int temp = nums[L];
                nums[L] = nums[R];
                nums[R] = temp;
                L++;
                R--;
            }
            return;
        }

        for (int i = n - 1; i >= pivot; i--) {
            if (nums[i] > nums[pivot]) {
                int temp2 = nums[i];
                nums[i] = nums[pivot];
                nums[pivot] = temp2;
                break;
            }
        }

        int left = pivot + 1;
        int right = n - 1;

        while (left < right) {
            int temp1 = nums[left];
            nums[left] = nums[right];
            nums[right] = temp1;
            left++;
            right--;
        }
    }
}
```

---

## ⭐ Main Logic

### Step 1 - Find the Pivot

```java
if (nums[i] < nums[i + 1]) {
    pivot = i;
    break;
}
```

Find the first element from the right that is smaller than its next element.

---

### Step 2 - Find the Least Greater Element

```java
if (nums[i] > nums[pivot]) {
    swap(nums[i], nums[pivot]);
}
```

Traverse from right to left.

The **first element greater than the pivot** is automatically the **least greater element** because the suffix is already sorted in descending order.

---

### Step 3 - Reverse the Suffix

```java
left = pivot + 1;
right = n - 1;

while(left < right){
    swap(nums[left], nums[right]);
}
```

Reverse the remaining suffix so it becomes the smallest possible order.

> **Interview Takeaway:**  
> Whenever a question asks for the **next lexicographical arrangement**, think of the sequence:
>
> **Find Pivot → Swap → Reverse**

---

## 🧪 Dry Run

### Input

```text
nums = [1,2,3]
```

### Step 1

Find the pivot.

```text
1 2 3
  ↑

pivot = 1
```

---

### Step 2

Find the first element greater than `2`.

```text
3
```

Swap.

```text
1 3 2
```

---

### Step 3

Reverse everything after the pivot.

```text
Suffix = [2]

Already sorted.
```

### Final Output

```text
[1,3,2]
```

---

### Another Example

```text
nums = [3,2,1]
```

No pivot is found.

Reverse the entire array.

```text
[1,2,3]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- Find pivot → O(n)
- Find least greater element → O(n)
- Reverse suffix → O(n)

Overall Time Complexity = **O(n)**.

### Space Complexity

**O(1)**

- The array is modified in-place.

---

## 📌 Constraints

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 100`

---

## 💡 Key Points

- Traverse from right to left.
- Find the pivot (`nums[i] < nums[i+1]`).
- If no pivot exists, reverse the entire array.
- Swap with the least greater element.
- Reverse the suffix.
- In-place solution with constant space.

---

## ⚠️ Common Mistakes

- Traversing from left to right.
- Forgetting to reverse the entire array when no pivot exists.
- Swapping with the wrong element instead of the least greater element.
- Forgetting to reverse the suffix after swapping.
- Starting the reverse from the pivot instead of `pivot + 1`.

---

## 📝 Revision Snapshot

**Problem Type:** Next Lexicographical Permutation

**Pattern Used:** Two Pointers + Array Traversal + Reverse

**Main Data Structure:** Array

**Main Flow**

```text
Traverse from Right
        │
        ▼
Find Pivot
        │
        ▼
Pivot Found?
      /     \
    No       Yes
    │         │
Reverse   Find Least Greater
Entire       Element
Array         │
              ▼
           Swap
              │
              ▼
      Reverse Suffix
```

**Key Idea**

```text
Find Pivot
      ↓
Swap with Least Greater Element
      ↓
Reverse Remaining Suffix
```