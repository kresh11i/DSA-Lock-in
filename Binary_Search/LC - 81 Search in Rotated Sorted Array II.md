**File name:** `LC - 81 Search in Rotated Sorted Array II.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 81 - Search in Rotated Sorted Array II

## 🔗 Problem

Given a sorted array that has been rotated at an unknown position, search for a `target` value.

Unlike the previous rotated-array problem, this array can contain **duplicate values**.

Return `true` if the target exists, otherwise return `false`.

---

## 🏷️ Tags

* Array
* Binary Search
* Rotated Array
* Duplicates

---

## 📚 Topics

* Arrays
* Binary Search
* Rotated Sorted Array
* Duplicate Handling

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

This problem is similar to **LC 33 - Search in Rotated Sorted Array**, but here duplicates are allowed.

With unique values, I can easily identify which half is sorted using:

```text
nums[l] <= nums[mid]
```

But duplicates create an important problem.

For example:

```text
[1,0,1,1,1]
 ↑   ↑     ↑
 l  mid    h
```

Here:

```text
nums[l] = nums[mid] = nums[h] = 1
```

So I cannot confidently determine which half is sorted.

When this happens, I safely remove the duplicate boundary values:

```java
l++;
h--;
```

After removing them, I continue with the normal rotated Binary Search logic.

So the overall idea is:

```text
Target found
    ↓
Return true

Otherwise

Duplicates hide the sorted half?
    ↓
Shrink both boundaries

Otherwise

Identify sorted half
    ↓
Check whether target lies there
    ↓
Discard the other half
```

---

## 🧠 Thought Process

### Step 1 : Initialize Binary Search

```java
int l = 0, h = nums.length - 1;
```

I use:

```text
l → left boundary
h → right boundary
mid → middle element
```

The search continues while:

```java
while(l <= h)
```

---

### Step 2 : Check the Middle Element

The first thing I check is:

```java
if(target == nums[mid]){
    return true;
}
```

If the middle element is the target, there is no need to continue searching.

---

### Step 3 : Handle the Duplicate Problem

This is the most important part of LC 81.

```java
if(nums[l] == nums[mid] && nums[mid] == nums[h]){
    l = l + 1;
    h = h - 1;
    continue;
}
```

If:

```text
nums[l] == nums[mid] == nums[h]
```

I cannot reliably identify which half is sorted.

For example:

```text
[1,0,1,1,1]
 ↑   ↑     ↑
 l  mid    h
```

All three boundary values are `1`, but the `0` is hidden inside the range.

So instead of making a wrong decision, I remove the duplicate boundaries:

```text
l++
h--
```

Then I continue Binary Search with the smaller range.

---

### Step 4 : Identify the Sorted Half

Once the duplicate ambiguity is removed, I use the normal rotated-array condition:

```java
if(nums[l] <= nums[mid])
```

If true, the left half is sorted.

```text
[ sorted | rotated ]
```

Then I check whether the target belongs to the sorted left half:

```java
if(nums[l] <= target && target <= nums[mid])
```

If yes:

```java
h = mid - 1;
```

Otherwise:

```java
l = mid + 1;
```

---

### Step 5 : If the Right Half is Sorted

If:

```java
nums[l] > nums[mid]
```

then the right half is sorted.

I check:

```java
if(nums[mid] <= target && target <= nums[h])
```

If the target lies inside the sorted right half:

```java
l = mid + 1;
```

Otherwise:

```java
h = mid - 1;
```

---

## 🔍 Dry Run

Input:

```text
nums = [1,0,1,1,1]
target = 0
```

### Iteration 1

```text
l = 0
h = 4
mid = 2

nums[l]  = 1
nums[mid] = 1
nums[h]  = 1
```

We have:

```text
nums[l] == nums[mid] == nums[h]
```

So we cannot determine the sorted half.

Shrink:

```text
l = 1
h = 3
```

---

### Iteration 2

```text
nums = [1,0,1,1,1]

     l     mid  h
     ↓      ↓   ↓
[1, 0, 1, 1, 1]
```

Now:

```text
nums[l] = 0
nums[mid] = 1
```

The left half is sorted:

```text
0 <= 1
```

Check:

```text
0 <= target <= 1
```

Since:

```text
0 <= 0 <= 1
```

the target can be in the left half.

So:

```text
h = mid - 1
```

---

### Iteration 3

Now:

```text
l = 1
h = 1
mid = 1
```

```text
nums[mid] = 0
```

Target found.

```text
return true
```

---

## 💻 Java Solution

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int l = 0 , h = nums.length-1 ;
        boolean ans = false;

        while(l<=h){
            int mid = (l+h)/2;

            if(target == nums[mid]){
                return true;
            }

            if(nums[l]== nums[mid] && nums[mid]==nums[h]){
                l = l+1;
                h = h-1;
                continue;
            }

            if(nums[l]<=nums[mid]){
                if(nums[l]<= target && target<= nums[mid]){
                    h = mid-1;
                }else{
                    l = mid+1;
                }
            }else{
                if(nums[mid] <=  target && target <= nums[h]){
                    l = mid +1;
                }else{
                    h = mid-1;
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
if(nums[l] == nums[mid] && nums[mid] == nums[h]){
    l = l + 1;
    h = h - 1;
    continue;
}

if(nums[l] <= nums[mid]){
    if(nums[l] <= target && target <= nums[mid]){
        h = mid - 1;
    }else{
        l = mid + 1;
    }
}else{
    if(nums[mid] <= target && target <= nums[h]){
        l = mid + 1;
    }else{
        h = mid - 1;
    }
}
```

### Why is this the Main Logic?

There are two important ideas.

First, handle the duplicate case:

```text
nums[l] == nums[mid] == nums[h]
```

Here, the sorted half is ambiguous, so I shrink the search space from both sides.

Then I use the same logic as LC 33:

```text
Left half sorted
        ↓
Target inside left?
   ↓             ↓
  Yes            No
   ↓             ↓
Search left   Search right
```

or:

```text
Right half sorted
        ↓
Target inside right?
   ↓             ↓
  Yes            No
   ↓             ↓
Search right  Search left
```

> 💡 **Interview Takeaway:**
> Duplicates don't completely break Binary Search; they only create cases where I cannot identify the sorted half. In that situation, safely shrink the duplicate boundaries and continue.

---

## 🎯 Key Pattern

```text
Find Mid
   ↓
Target == nums[mid] ?
   ↓
  YES → true

  NO
   ↓
nums[l] == nums[mid] == nums[h] ?
   ↓
  YES → l++, h--
   ↓
  NO
   ↓
Identify Sorted Half
   ↓
Check Target Range
   ↓
Discard One Half
```

The special case to remember is:

```text
nums[l] == nums[mid] == nums[h]
```

This is what makes **LC 81 different from LC 33**.

---

## 🧪 Another Example

```text
nums = [2,5,6,0,0,1,2]
target = 0
```

The array contains duplicates, but they don't necessarily cause ambiguity.

When the sorted half can be identified:

```text
[2,5,6] | [0,0,1,2]
```

I can use the normal rotated Binary Search logic.

When the boundaries become:

```text
nums[l] == nums[mid] == nums[h]
```

I simply shrink:

```text
l++
h--
```

and continue.

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n) average
```

Normally, the search space is reduced by half like Binary Search.

However, because duplicates can force us to shrink only one element from each side, the **worst case can become `O(n)`**.

### Space Complexity

```text
O(1)
```

Only a few pointer variables are used.

---

## 📌 Constraints

* `1 <= nums.length <= 5000`
* `-10⁴ <= nums[i] <= 10⁴`
* `nums` is sorted and rotated.
* Duplicate values are allowed.
* `-10⁴ <= target <= 10⁴`

---

## 📌 Key Takeaways

* LC 81 is the duplicate version of rotated Binary Search.
* With duplicates, `nums[l] == nums[mid] == nums[h]` makes the sorted half ambiguous.
* Safely shrink the boundaries when this happens.
* Otherwise, use the same sorted-half logic as LC 33.
* Duplicates can degrade the worst-case complexity to `O(n)`.
* Average-case performance remains close to `O(log n)`.
* Space complexity is `O(1)`.
