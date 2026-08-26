**File name:** `LC - 153 Find Minimum in Rotated Sorted Array.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 153 - Find Minimum in Rotated Sorted Array

## 🔗 Problem

Given a sorted array that has been rotated at an unknown position, find and return the **minimum element**.

The array contains **unique elements**.

---

## 🏷️ Tags

* Array
* Binary Search
* Rotated Array

---

## 📚 Topics

* Arrays
* Binary Search
* Rotated Sorted Array

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

The array was originally sorted, but then it was rotated.

For example:

```text
[1,2,3,4,5,6,7]

After rotation:

[4,5,6,7,1,2,3]
```

The minimum element is the point where the rotation happened.

Instead of checking every element, I use **Binary Search**.

At every step, I check whether the current search range is already sorted:

```java
if(nums[low] <= nums[high])
```

If it is sorted, then `nums[low]` is the smallest element in that range.

Otherwise, I check which half is sorted using:

```java
if(nums[low] <= nums[mid])
```

If the left half is sorted, I know `nums[low]` is a possible minimum and move to the right half.

Otherwise, the rotation point is in the left half, so I move `high` to `mid - 1`.

I keep updating `ans` with the smallest value found.

---

## 🧠 Thought Process

### Step 1 : Initialize Binary Search

```java
int low = 0, high = nums.length - 1;
int ans = Integer.MAX_VALUE;
```

`low` and `high` represent the current search range.

`ans` stores the minimum value found so far.

---

### Step 2 : Check if the Current Range is Already Sorted

Before checking `mid`, I check:

```java
if(nums[low] <= nums[high]){
    ans = Math.min(nums[low],ans);
}
```

If:

```text
nums[low] <= nums[high]
```

then the current range is completely sorted.

Example:

```text
[1,2,3,4,5]
 ↑       ↑
low     high
```

Since the range is sorted, the smallest value is directly:

```text
nums[low]
```

So I update:

```java
ans = Math.min(nums[low], ans);
```

---

### Step 3 : Check Which Half is Sorted

Now I check:

```java
if (nums[low] <= nums[mid])
```

If this is true, the left half is sorted.

Example:

```text
[4,5,6,7,1,2,3]
 ↑       ↑
low     mid
```

Here:

```text
4 <= 7
```

so:

```text
[4,5,6,7]
```

is sorted.

The smallest value of this sorted half is `nums[low]`, so I consider it as a possible answer.

```java
ans = Math.min(nums[low] , ans);
```

Then I move:

```java
low = mid + 1;
```

because the minimum can be in the other half.

I also check `nums[mid]` against `ans` because it can itself be the minimum candidate:

```java
if(nums[mid]< ans){
    ans = Math.min(nums[mid] , ans);
}
```

---

### Step 4 : When the Left Half is Not Sorted

If:

```java
nums[low] > nums[mid]
```

then the left half contains the rotation point.

So `nums[mid]` becomes a possible minimum:

```java
ans = Math.min(nums[mid] , ans);
```

Then I move:

```java
high = mid-1;
```

This keeps the part where the smaller element can exist.

---

## 🔍 Dry Run

Input:

```text
nums = [4,5,6,7,0,1,2]
```

### Iteration 1

```text
low = 0
high = 6
mid = 3

nums[low] = 4
nums[mid] = 7
nums[high] = 2
```

The complete range is not sorted because:

```text
4 > 2
```

Check:

```text
4 <= 7 ✔
```

So the left half is sorted.

Possible minimum:

```text
4
```

Move:

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

nums = [0,1,2]
```

Now:

```text
nums[low] <= nums[high]

0 <= 2 ✔
```

The range is already sorted.

Therefore:

```text
nums[low] = 0
```

is the minimum.

```text
ans = 0
```

The remaining search eventually finishes with:

```text
0
```

### Final Answer

```text
0
```

---

## 💻 Java Solution

```java
class Solution {
    public int findMin(int[] nums) {
        int low = 0, high = nums.length - 1;
        int ans = Integer.MAX_VALUE;
        while (low <= high) {
            int mid = (low + high) / 2;
            if(nums[low]<=nums[high]){
                ans = Math.min(nums[low],ans);
            }
            if (nums[low] <= nums[mid]) {
                ans = Math.min(nums[low] , ans);
                low = mid + 1;
                if(nums[mid]< ans){
                    ans = Math.min(nums[mid] , ans);
                }
            }else{
                ans = Math.min(nums[mid] , ans);
                high = mid-1;
                if(nums[mid]< ans){
                    ans = Math.min(nums[mid] , ans);
                }
            }

        }
        return ans;
    }
}
```

---

## ⭐ Main Logic

```java
if(nums[low] <= nums[high]){
    ans = Math.min(nums[low], ans);
}

if (nums[low] <= nums[mid]) {
    ans = Math.min(nums[low], ans);
    low = mid + 1;
} else {
    ans = Math.min(nums[mid], ans);
    high = mid - 1;
}
```

### Why is this the Main Logic?

The main idea is to use the sorted property of the rotated array.

If the current range is completely sorted:

```text
nums[low] <= nums[high]
```

then `nums[low]` is the minimum of that range.

Otherwise, I determine which half is sorted.

```text
nums[low] <= nums[mid]
        ↓
Left half sorted
        ↓
Take nums[low] as candidate
        ↓
Search right
```

Otherwise:

```text
Left half is not sorted
        ↓
Minimum is around the left/rotation side
        ↓
Take nums[mid] as candidate
        ↓
Search left
```

> 💡 **Interview Takeaway:**
> In a rotated sorted array, use the sorted half to eliminate unnecessary elements while keeping track of the smallest candidate.

---

## 🎯 Key Pattern

```text
Rotated Sorted Array
        ↓
Check if current range is sorted
        ↓
   Yes → nums[low] is minimum
        ↓
   No
        ↓
Identify sorted half
        ↓
Keep possible minimum
        ↓
Discard unnecessary half
```

The two important checks are:

```text
nums[low] <= nums[high]
```

and:

```text
nums[low] <= nums[mid]
```

---

## 🧪 Another Example

```text
nums = [3,4,5,1,2]
```

The array is not completely sorted.

At the beginning:

```text
[3,4,5,1,2]
 ↑   ↑     ↑
low mid   high
```

The left half:

```text
[3,4,5]
```

is sorted.

So `3` is a candidate, but I search the other half because the rotation point can contain a smaller value.

Eventually the search reaches:

```text
[1,2]
```

which is already sorted.

Therefore:

```text
nums[low] = 1
```

and the answer is:

```text
1
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

Binary Search reduces the search range roughly by half in every iteration.

### Space Complexity

```text
O(1)
```

Only `low`, `high`, `mid`, and `ans` are used.

---

## 📌 Constraints

* `n == nums.length`
* `1 <= n <= 5000`
* `-5000 <= nums[i] <= 5000`
* All integers in `nums` are unique.
* `nums` is sorted and rotated between `1` and `n` times.

---

## 📌 Key Takeaways

* A rotated sorted array still contains sorted portions.
* If `nums[low] <= nums[high]`, the current range is already sorted.
* `nums[low]` is the minimum of an already sorted range.
* Identify the sorted half to decide which part can be discarded.
* Keep updating `ans` with possible minimum values.
* Binary Search reduces the solution to `O(log n)` time.
* Only `O(1)` extra space is required.
