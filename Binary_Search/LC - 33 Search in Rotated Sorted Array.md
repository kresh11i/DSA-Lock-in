**File name:** `LC - 33 Search in Rotated Sorted Array.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 33 - Search in Rotated Sorted Array

## 🔗 Problem

Given a sorted array that has been rotated at an unknown position, search for a given `target` and return its index.

If the target does not exist, return `-1`.

The important idea is that even after rotation, **at least one half of the array will always be sorted**.

---

## 🏷️ Tags

* Array
* Binary Search
* Rotated Array

---

## 📚 Topics

* Arrays
* Binary Search
* Sorted Rotated Array

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

Normally, Binary Search works because the entire array is sorted.

Here, the array has been rotated:

```text
[0,1,2,4,5,6,7]

        ↓ rotate

[4,5,6,7,0,1,2]
```

So the entire array is no longer sorted.

But there is an important observation:

> **At least one half of the current search range is always sorted.**

For every iteration, I check which half is sorted.

```text
nums[low] <= nums[mid]
```

If this is true, the **left half is sorted**.

Otherwise, the **right half is sorted**.

Once I know the sorted half, I check whether the target lies inside that range.

* If yes → search that half.
* If no → search the other half.

This allows us to keep the `O(log n)` Binary Search complexity.

---

## 🧠 Thought Process

### Step 1 : Initialize Binary Search

```java
int low = 0, high = nums.length - 1;
```

The search range initially contains the entire array.

Then calculate:

```java
int mid = (low + high) / 2;
```

If:

```java
target == nums[mid]
```

the target is found immediately.

---

### Step 2 : Identify the Sorted Half

The most important condition is:

```java
if (nums[low] <= nums[mid])
```

If this is true, the left half is sorted.

For example:

```text
[4,5,6,7,0,1,2]
 ↑     ↑
low   mid
```

Here:

```text
nums[low] = 4
nums[mid] = 7

4 <= 7 ✔
```

So:

```text
[4,5,6,7]
```

is the sorted half.

---

### Step 3 : Check Whether Target is Inside the Sorted Half

If the left half is sorted, I check:

```java
if (nums[low] <= target && target <= nums[mid])
```

If true, the target must be somewhere in the left half.

So:

```java
high = mid - 1;
```

Otherwise, the target cannot be in the sorted left half, so I search the right half:

```java
low = mid + 1;
```

---

### Step 4 : When the Right Half is Sorted

If:

```java
nums[low] > nums[mid]
```

then the right half is sorted.

For example:

```text
[6,7,0,1,2,4,5]
 ↑     ↑       ↑
low   mid     high
```

Here:

```text
nums[low] = 6
nums[mid] = 1

6 > 1
```

So the right half:

```text
[1,2,4,5]
```

is sorted.

Now check whether the target lies inside it:

```java
if (nums[mid] <= target && target <= nums[high])
```

If yes:

```java
low = mid + 1;
```

Otherwise:

```java
high = mid - 1;
```

---

## 🔍 Dry Run

Input:

```text
nums = [4,5,6,7,0,1,2]
target = 0
```

### Iteration 1

```text
low = 0
high = 6

mid = 3
nums[mid] = 7
```

Target is not `7`.

Check sorted half:

```text
nums[low] <= nums[mid]

4 <= 7 ✔
```

So the left half is sorted:

```text
[4,5,6,7]
```

Check:

```text
4 <= 0 <= 7
```

False.

So target must be in the right half:

```text
low = mid + 1
low = 4
```

---

### Iteration 2

```text
low = 4
high = 6

mid = 5
nums[mid] = 1
```

Target is not `1`.

Check:

```text
nums[low] <= nums[mid]

0 <= 1 ✔
```

Left half is sorted:

```text
[0,1]
```

Check:

```text
0 <= 0 <= 1 ✔
```

So search left:

```text
high = mid - 1
high = 4
```

---

### Iteration 3

```text
low = 4
high = 4

mid = 4
nums[mid] = 0
```

Target found.

```text
return 4
```

### Final Answer

```text
4
```

---

## 💻 Java Solution

```java
class Solution { 
    public int search(int[] nums, int target) { 
        int low = 0, high = nums.length - 1; 
 
        while (low <= high) { 
            int mid = (low + high) / 2; 

            if (target == nums[mid]) { 
                return mid; 
            } 

            if (nums[low] <= nums[mid]) { 
 
                if (nums[low] <= target && target <= nums[mid]) { 
                    high = mid - 1; 
                } else { 
                    low = mid + 1; 
                } 
            } else { 
                if (nums[mid] <= target && target <= nums[high]) { 
                    low = mid + 1; 
                } else { 
                    high = mid - 1; 
                } 
            } 
        } 

        return -1; 
    } 
}
```

---

## ⭐ Main Logic

```java
if (nums[low] <= nums[mid]) {

    // Left half is sorted

    if (nums[low] <= target && target <= nums[mid]) {
        high = mid - 1;
    } else {
        low = mid + 1;
    }

} else {

    // Right half is sorted

    if (nums[mid] <= target && target <= nums[high]) {
        low = mid + 1;
    } else {
        high = mid - 1;
    }
}
```

### Why is this the Main Logic?

The entire trick is to first find **which half is sorted**.

```text
nums[low] <= nums[mid]
        ↓
Left half sorted
```

Otherwise:

```text
Right half sorted
```

Then I check whether the target belongs to that sorted half.

```text
Target inside sorted half
        ↓
Search that half

Target outside sorted half
        ↓
Search other half
```

> 💡 **Interview Takeaway:**
> In a rotated sorted array, don't try to find the rotation point first. At every Binary Search step, identify the sorted half and decide where the target can exist.

---

## 🎯 Key Pattern

```text
Rotated Sorted Array
        ↓
Find Mid
        ↓
Is Left Half Sorted?
      /       \
    YES        NO
     ↓          ↓
Check Target   Right Half Sorted
     ↓          ↓
Choose Search Half
        ↓
      Repeat
```

The two important conditions are:

```text
Left Sorted:

nums[low] <= nums[mid]
```

and:

```text
Target in Left:

nums[low] <= target <= nums[mid]
```

For the right side:

```text
Target in Right:

nums[mid] <= target <= nums[high]
```

---

## 🧪 Another Example

```text
nums = [6,7,0,1,2,4,5]
target = 4
```

The right half is sorted:

```text
[1,2,4,5]
```

Since:

```text
1 <= 4 <= 5
```

we search the right half.

Eventually:

```text
target = 4
```

is found at:

```text
index = 5
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

Each iteration eliminates approximately half of the remaining search space.

### Space Complexity

```text
O(1)
```

Only `low`, `high`, and `mid` are used.

---

## 📌 Constraints

* `1 <= nums.length <= 5000`
* `-10⁴ <= nums[i] <= 10⁴`
* All values of `nums` are unique.
* `nums` is sorted and then rotated at an unknown position.
* `-10⁴ <= target <= 10⁴`

---

## 📌 Key Takeaways

* A rotated sorted array always has at least one sorted half.
* First identify which half is sorted.
* Check whether the target lies inside the sorted half.
* If it does, search that half; otherwise search the other half.
* Do not search for the rotation point separately.
* The modified Binary Search still works in `O(log n)` time.
* Space complexity remains `O(1)`.
