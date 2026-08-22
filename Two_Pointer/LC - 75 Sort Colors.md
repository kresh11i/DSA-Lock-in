**File name:** `LC - 75 Sort Colors.md`
**📁 Folder:** `Two_Pointer`

# 🧩 LeetCode 75 - Sort Colors

## 🔗 Problem

Given an array containing only `0`, `1`, and `2`, sort the array in-place so that all `0`s come first, followed by `1`s, and then `2`s.

The solution should be done without using a separate sorting algorithm.

---

## 🏷️ Tags

* Array
* Two Pointer
* Sorting
* Dutch National Flag

---

## 📚 Topics

* Arrays
* Two Pointers
* In-place Sorting

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

Since the array contains only three values:

```text
0 → Red
1 → White
2 → Blue
```

I use three pointers:

```text
low  → position where the next 0 should go
mid  → current element being checked
high → position where the next 2 should go
```

The main idea is to divide the array into three sections:

```text
[ 0s | 1s | unknown | 2s ]
       low  mid     high
```

Whenever `mid` finds a `0`, I swap it with `low`.

If it finds a `1`, I simply move `mid`.

If it finds a `2`, I swap it with `high`.

This is the **Dutch National Flag** approach and sorts the array in one traversal.

---

## 🧠 Thought Process

### Step 1 : Initialize Three Pointers

```java
int low = 0;
int mid = 0;
int high = nums.length - 1;
```

Initially, the whole array is unknown.

```text
[ unknown unknown unknown unknown ]
  ↑                          ↑
 mid                        high
```

---

### Step 2 : When `nums[mid] == 0`

If the current element is `0`, it belongs at the beginning.

So I swap `nums[mid]` with `nums[low]`.

```java
int temp = nums[mid];
nums[mid] = nums[low];
nums[low] = temp;
```

Then both `low` and `mid` move forward:

```java
low++;
mid++;
```

This is because the element placed at `low` is already correctly positioned.

---

### Step 3 : When `nums[mid] == 1`

`1` already belongs in the middle section.

So no swapping is required.

Simply move:

```java
mid++;
```

---

### Step 4 : When `nums[mid] == 2`

`2` belongs at the end.

So I swap `nums[mid]` with `nums[high]`.

```java
int temp1 = nums[mid];
nums[mid] = nums[high];
nums[high] = temp1;
```

Then:

```java
high--;
```

Here, I **do not increment `mid`**.

The reason is that the element swapped from `high` into `mid` has not been checked yet. It could be `0`, `1`, or `2`, so I need to process it again.

---

## 🔍 Dry Run

Input:

```text
nums = [2,0,2,1,1,0]
```

Initial:

```text
low = 0
mid = 0
high = 5
```

### Step 1

```text
nums[mid] = 2
```

Swap with `high`:

```text
[0,0,2,1,1,2]
```

Move:

```text
high--
```

`mid` stays the same.

---

### Step 2

```text
nums[mid] = 0
```

Swap with `low`:

```text
[0,0,2,1,1,2]
```

Move:

```text
low++
mid++
```

---

### Step 3

```text
nums[mid] = 2
```

Swap with `high`:

```text
[0,0,1,1,2,2]
```

Move:

```text
high--
```

Again, `mid` stays because the new element at `mid` must be checked.

---

### Step 4

```text
nums[mid] = 1
```

Move:

```text
mid++
```

---

### Step 5

```text
nums[mid] = 1
```

Move:

```text
mid++
```

Now:

```text
mid > high
```

So the process ends.

### Final Output

```text
[0,0,1,1,2,2]
```

---

## 💻 Java Solution

```java
class Solution {
    public void sortColors(int[] nums) {
        int low = 0;
        int mid = 0;
        int high = nums.length - 1;
        while (mid <= high) {
            if (nums[mid] == 0) {
                int temp = nums[mid];
                nums[mid] = nums[low];
                nums[low] = temp;
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                mid++;
            } else {
                int temp1 = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp1;
                high--;
            }

        }

    }
}
```

---

## ⭐ Main Logic

```java
if (nums[mid] == 0) {
    int temp = nums[mid];
    nums[mid] = nums[low];
    nums[low] = temp;
    low++;
    mid++;
} else if (nums[mid] == 1) {
    mid++;
} else {
    int temp1 = nums[mid];
    nums[mid] = nums[high];
    nums[high] = temp1;
    high--;
}
```

### Why is this the Main Logic?

* `low` keeps track of where `0` should be placed.
* `mid` checks the current unknown element.
* `high` keeps track of where `2` should be placed.
* For `0`, swap with `low` and move both pointers.
* For `1`, only move `mid`.
* For `2`, swap with `high` and move only `high`.
* `mid` does not move after placing a `2` because the swapped element still needs to be checked.

> 💡 **Interview Takeaway:**
> When an array contains only three distinct values, think about the **Dutch National Flag / three-pointer** approach instead of normal sorting.

---

## 🎯 Key Pattern

```text
[ 0s | 1s | Unknown | 2s ]
       ↑       ↑       ↑
      low     mid     high
```

The goal is to continuously reduce the **unknown** section.

```text
0 → low++
1 → mid++
2 → high--
```

The special case is:

```text
2 → high--
```

without moving `mid`.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n)
```

The array is traversed only once.

### Space Complexity

```text
O(1)
```

Only three pointers and temporary variables are used. The sorting is performed in-place.

---

## 📌 Constraints

* `1 <= nums.length <= 300`
* `nums[i]` is either `0`, `1`, or `2`.

---

## 📌 Key Takeaways

* Use three pointers: `low`, `mid`, and `high`.
* `0` goes to the left, `1` stays in the middle, and `2` goes to the right.
* Do not increment `mid` after swapping a `2`.
* The array is sorted in-place.
* The Dutch National Flag approach gives `O(n)` time and `O(1)` space.
