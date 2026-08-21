Your code is **LeetCode 88 – Merge Sorted Array**, not LC 58.
**LC 58 is Length of Last Word.**

So based on the code you provided:

**File name:** `LC - 88 Merge Sorted Array.md`
**📁 Folder:** `Two_Pointer`

# 🧩 LeetCode 88 - Merge Sorted Array

## 🔗 Problem

Given two sorted integer arrays `nums1` and `nums2`, merge `nums2` into `nums1` so that `nums1` becomes one sorted array.

`nums1` has enough extra space at the end to store all elements from `nums2`.

---

## 🏷️ Tags

* Array
* Two Pointer
* Sorting
* In-place

---

## 📚 Topics

* Arrays
* Two Pointers
* In-place Array Manipulation

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

Since both arrays are already sorted, we don't need to sort them again.

The main idea is to start comparing the elements **from the end** of both arrays.

I use three pointers:

```text
i → last valid element of nums1
j → last element of nums2
k → last position available in nums1
```

I compare `nums1[i]` and `nums2[j]`.

The larger element is placed at `nums1[k]`.

Moving from the end is important because `nums1` already contains its valid elements at the beginning, and placing values from the back prevents overwriting them.

---

## 🧠 Thought Process

### Step 1 : Create Three Pointers

```java
int i = m - 1, j = n - 1, k = m + n - 1;
```

Here:

```text
i → points to the last actual element of nums1

j → points to the last element of nums2

k → points to the last position of nums1
```

Example:

```text
nums1 = [1,2,3,0,0,0]
nums2 = [2,5,6]

i = 2
j = 2
k = 5
```

---

### Step 2 : Compare From the Back

While both arrays still have elements:

```java
while(i>=0 && j>=0)
```

Compare:

```java
if(nums1[i] < nums2[j])
```

If `nums2[j]` is larger, place it at `nums1[k]`.

```java
nums1[k] = nums2[j];

j--;
k--;
```

Otherwise, place `nums1[i]`.

```java
nums1[k] = nums1[i];

i--;
k--;
```

Because the arrays are sorted, the largest remaining element will always be at either `i` or `j`.

---

### Step 3 : Copy Remaining Elements of nums2

After the main loop, there may still be elements left in `nums2`.

So:

```java
while(j>=0)
```

Copy the remaining elements:

```java
nums1[k] = nums2[j];

j--;
k--;
```

There is no need to copy the remaining elements of `nums1` because they are already in their correct positions.

---

## 🔍 Dry Run

Input:

```text
nums1 = [1,2,3,0,0,0]
m = 3

nums2 = [2,5,6]
n = 3
```

Initial pointers:

```text
i = 2
j = 2
k = 5
```

### Comparison 1

```text
nums1[i] = 3
nums2[j] = 6

6 is larger
```

Place `6`:

```text
[1,2,3,0,0,6]
```

Move:

```text
j--
k--
```

---

### Comparison 2

```text
nums1[i] = 3
nums2[j] = 5

5 is larger
```

Place `5`:

```text
[1,2,3,0,5,6]
```

---

### Comparison 3

```text
nums1[i] = 3
nums2[j] = 2

3 is larger
```

Place `3`:

```text
[1,2,3,3,5,6]
```

---

### Comparison 4

```text
nums1[i] = 2
nums2[j] = 2
```

Since the condition is:

```java
nums1[i] < nums2[j]
```

the `else` block executes.

Place `2`:

```text
[1,2,2,3,5,6]
```

---

### Remaining Element

Now `nums1` still has `1`, but `nums2` has no elements left.

The result is:

```text
[1,2,2,3,5,6]
```

---

## 💻 Java Solution

```java
class Solution {

    public void merge(int[] nums1, int m, int[] nums2, int n) {

        int i = m - 1, j = n - 1, k = m + n - 1;

        while(i>=0 && j>=0){

            if(nums1[i] < nums2[j]){

                nums1[k] = nums2[j];

                j--;

                k--;

            }else{

                nums1[k] = nums1[i];

                i--;

                k--;

            }
        }

        while(j>=0){

            nums1[k] = nums2[j];

            j--;

            k--;

        }
    }
}
```

---

## ⭐ Main Logic

```java
if(nums1[i] < nums2[j]){

    nums1[k] = nums2[j];

    j--;
    k--;

}else{

    nums1[k] = nums1[i];

    i--;
    k--;
}
```

### Why is this the Main Logic?

* Both arrays are already sorted.
* `i` and `j` point to the largest remaining elements.
* `k` points to the position where the largest element should go.
* The larger value between `nums1[i]` and `nums2[j]` is placed at `nums1[k]`.
* Moving backwards prevents overwriting the useful elements already present in `nums1`.

> 💡 **Interview Takeaway:**
> When merging two sorted arrays in-place, start from the end so that existing elements in the first array are not overwritten.

---

## 🎯 Key Pattern

```text
Two Sorted Arrays
        ↓
Compare From End
        ↓
Place Larger Element At Back
        ↓
Move Pointer
```

The important pointer relationship is:

```text
i → nums1 valid elements
j → nums2
k → final position
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(m + n)
```

Each element is processed at most once.

### Space Complexity

```text
O(1)
```

The merging is done directly inside `nums1` without using another array.

---

## 📌 Constraints

* `0 <= m, n <= 200`
* `1 <= m + n <= 200`
* `-10⁹ <= nums1[i], nums2[j] <= 10⁹`
* `nums1` contains `m` valid elements followed by `n` empty positions.

---

## 📌 Key Takeaways

* Both arrays are already sorted, so no additional sorting is needed.
* Use three pointers: `i`, `j`, and `k`.
* Start from the **back** to avoid overwriting `nums1`.
* Always place the larger element at `k`.
* Remaining elements of `nums2` must be copied after the main loop.
* The solution works in `O(m + n)` time and `O(1)` extra space.
