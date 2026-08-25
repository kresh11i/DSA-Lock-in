**File name:** `LC - 34 Find First and Last Position of Element in Sorted Array.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 34 - Find First and Last Position of Element in Sorted Array

## 🔗 Problem

Given a sorted array `nums` and a target value, find the **first and last position** of the target.

If the target does not exist, return:

```text
[-1,-1]
```

The important idea is to use **Binary Search twice**:

* First Binary Search → find the **first occurrence**
* Second Binary Search → find the **last occurrence**

---

## 🏷️ Tags

* Array
* Binary Search
* Lower Bound
* Upper Bound

---

## 📚 Topics

* Arrays
* Binary Search
* Searching in Sorted Array

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

Since the array is sorted, I can use Binary Search instead of checking every element.

The problem has two separate goals:

```text
First occurrence → search towards LEFT
Last occurrence  → search towards RIGHT
```

For the first occurrence, whenever I find the target, I store its index and continue searching on the left side.

For the last occurrence, whenever I find the target, I store its index and continue searching on the right side.

So I use two Binary Searches.

---

## 🧠 Thought Process

### Step 1 : Initialize the Answer

```java
int[] ans = new int[2];

ans[0] = -1;
ans[1] = -1;
```

Initially, both positions are `-1`.

If the target is never found, the answer remains:

```text
[-1,-1]
```

---

### Step 2 : Find the First Occurrence

I start a normal Binary Search:

```java
int low = 0, high = nums.length - 1;
```

When I find the target:

```java
if (target == nums[mid]) {
    ans[0] = mid;
    high = mid - 1;
}
```

The important part is:

```text
high = mid - 1
```

I don't stop after finding the target because there may be another occurrence further to the left.

Example:

```text
nums = [5,7,7,8,8,10]
target = 8
```

If I find:

```text
index = 4
```

I store:

```text
ans[0] = 4
```

but continue searching left.

Eventually I find:

```text
index = 3
```

So:

```text
first occurrence = 3
```

---

### Step 3 : Find the Last Occurrence

Now I perform another Binary Search.

I use separate pointers:

```java
int i = 0, j = nums.length - 1;
```

When I find the target:

```java
if (target == nums[mid]) {
    ans[1] = mid;
    i = mid + 1;
}
```

This time, I search to the **right**.

The important part is:

```text
i = mid + 1
```

There may be another occurrence after `mid`.

So I keep searching until I find the last occurrence.

---

## 🔍 Dry Run

Input:

```text
nums = [5,7,7,8,8,10]
target = 8
```

### First Occurrence

We want the first `8`.

```text
Index:  0 1 2 3 4 5
Array:  [5,7,7,8,8,10]
                  ↑
```

Suppose Binary Search finds index `4`.

```text
ans[0] = 4
```

But we continue left:

```text
high = 3
```

Now we find index `3`.

```text
ans[0] = 3
```

Continue searching left, but no earlier `8` exists.

So:

```text
First occurrence = 3
```

---

### Last Occurrence

Now search for the last `8`.

Suppose we find index `3`.

```text
ans[1] = 3
```

But we continue right:

```text
i = 4
```

Now index `4` also contains `8`.

```text
ans[1] = 4
```

Continue right, but there is no more `8`.

So:

```text
Last occurrence = 4
```

### Final Answer

```text
[3,4]
```

---

## 💻 Java Solution

```java
class Solution { 
    public int[] searchRange(int[] nums, int target) { 
        int low = 0, high = nums.length - 1; 
        int[] ans = new int[2]; 
        ans[0]= -1; 
        ans[1] = -1; 

        while (low <= high) { 
            int mid = (low + high) / 2; 

            if (target == nums[mid]) { 
                ans[0] = mid; 
                high = mid - 1; 
            } else if (target > nums[mid]) { 
                low = mid + 1; 
            } else { 
                high = mid - 1; 
            } 
        } 

        int i = 0, j = nums.length - 1; 

        while (i <= j) { 
            int mid = (i + j) / 2; 

            if (target == nums[mid]) { 
                ans[1] = mid; 
                i = mid + 1; 
            } else if (target > nums[mid]) { 
                i = mid + 1; 
            } else { 
                j = mid - 1; 
            } 
        } 
 
        return ans; 
    } 
}
```

---

## ⭐ Main Logic

### First Occurrence

```java
if (target == nums[mid]) { 
    ans[0] = mid; 
    high = mid - 1; 
}
```

When the target is found:

```text
Store answer
     ↓
Search LEFT
     ↓
Find an earlier occurrence
```

### Last Occurrence

```java
if (target == nums[mid]) { 
    ans[1] = mid; 
    i = mid + 1; 
}
```

When the target is found:

```text
Store answer
     ↓
Search RIGHT
     ↓
Find a later occurrence
```

### Why is this the Main Logic?

The only difference between the two Binary Searches is what happens **after finding the target**.

```text
First occurrence:
target found → high = mid - 1

Last occurrence:
target found → low = mid + 1
```

This lets us find the extreme positions of the target without scanning the entire array.

> 💡 **Interview Takeaway:**
> If you need the first or last occurrence of a value in a sorted array, Binary Search can be modified by continuing the search after finding the target.

---

## 🎯 Key Pattern

```text
Find First
    ↓
Target found
    ↓
Store index
    ↓
Move LEFT
    ↓
high = mid - 1
```

```text
Find Last
    ↓
Target found
    ↓
Store index
    ↓
Move RIGHT
    ↓
low = mid + 1
```

This is closely related to **Lower Bound** and **Upper Bound** Binary Search.

```text
First Position → first index where target occurs
Last Position  → last index where target occurs
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

Two Binary Searches are performed:

```text
O(log n) + O(log n)
= O(log n)
```

### Space Complexity

```text
O(1)
```

Only a few variables and the fixed-size answer array are used.

---

## 📌 Constraints

* `0 <= nums.length <= 10⁵`
* `-10⁹ <= nums[i] <= 10⁹`
* `nums` is sorted in non-decreasing order.
* `-10⁹ <= target <= 10⁹`

---

## 📌 Key Takeaways

* Use Binary Search because the array is sorted.
* For the **first occurrence**, move left after finding the target.
* For the **last occurrence**, move right after finding the target.
* Finding the target does not mean stopping the search.
* This is essentially finding the **leftmost and rightmost occurrence**.
* Two Binary Searches still give an overall `O(log n)` time complexity.
