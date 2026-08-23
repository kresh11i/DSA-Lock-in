**File name:** `LC - 704 Binary Search.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 704 - Binary Search

## 🔗 Problem

Given a sorted array `nums` and a target value, return the index of the target if it exists in the array.

If the target is not present, return `-1`.

---

## 🏷️ Tags

* Array
* Binary Search
* Searching

---

## 📚 Topics

* Arrays
* Binary Search
* Divide and Conquer

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

Since the array is already **sorted**, I don't need to check every element one by one.

Instead, I use **Binary Search**.

I maintain two pointers:

```text
low  → beginning of the search range
high → end of the search range
```

Then I calculate the middle element.

```text
mid = (low + high) / 2
```

I compare `nums[mid]` with the target.

* If they are equal, return `mid`.
* If the target is greater, search in the right half.
* If the target is smaller, search in the left half.

Every iteration removes half of the remaining search space.

---

## 🧠 Thought Process

### Step 1 : Initialize Pointers

```java
int low = 0, high = nums.length - 1;
```

Initially, the entire array is the search space.

For example:

```text
nums = [-1,0,3,5,9,12]
target = 9

low = 0
high = 5
```

---

### Step 2 : Find the Middle

```java
int mid = (low + high) / 2;
```

The middle element divides the current search space into two halves.

```text
[-1, 0, 3, 5, 9, 12]
          ↑
         mid
```

---

### Step 3 : Compare With Target

If:

```java
if(nums[mid] == target)
```

the target is found, so return its index.

If:

```java
else if(target > nums[mid])
```

the target must be on the right side because the array is sorted.

So:

```java
low = mid + 1;
```

Otherwise, the target must be on the left side:

```java
high = mid - 1;
```

---

### Step 4 : Continue Until Search Space Ends

The loop continues while:

```java
while(low <= high)
```

If eventually:

```text
low > high
```

the search space is empty, which means the target does not exist.

So we return:

```java
return -1;
```

---

## 🔍 Dry Run

Input:

```text
nums = [-1,0,3,5,9,12]
target = 9
```

### Iteration 1

```text
low = 0
high = 5

mid = (0 + 5) / 2
mid = 2

nums[mid] = 3
```

Since:

```text
9 > 3
```

Search the right half:

```text
low = 3
```

---

### Iteration 2

```text
low = 3
high = 5

mid = (3 + 5) / 2
mid = 4

nums[mid] = 9
```

Target found:

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
        int low = 0 , high = nums.length-1; 
        while(low <= high){ 
            int mid = (low + high)/2; 
            if(nums[mid]==target){ 
                return mid; 
            }else if(target> nums[mid]){ 
                low = mid+1; 
            }else{ 
                high = mid -1; 
            } 
         
        } 
        return -1; 
    } 
}
```

---

## ⭐ Main Logic

```java
int mid = (low + high) / 2;

if(nums[mid] == target){
    return mid;
}
else if(target > nums[mid]){
    low = mid + 1;
}
else{
    high = mid - 1;
}
```

### Why is this the Main Logic?

* `mid` checks the middle element.
* If the target is equal to `nums[mid]`, we found it.
* If the target is greater, eliminate the left half.
* If the target is smaller, eliminate the right half.
* This reduces the search space by half after every iteration.

> 💡 **Interview Takeaway:**
> Whenever the array is sorted and you need to search for an element, always think about Binary Search before using a linear search.

---

## 🎯 Key Pattern

```text
Sorted Array
     ↓
Find Middle
     ↓
Compare Target
     ↓
Discard Half
     ↓
Repeat
```

The main idea is:

```text
target > nums[mid] → search right
target < nums[mid] → search left
target == nums[mid] → found
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

The search space is divided into half in every iteration.

### Space Complexity

```text
O(1)
```

Only `low`, `high`, and `mid` variables are used.

---

## 📌 Constraints

* `1 <= nums.length <= 10⁴`
* `-10⁴ <= nums[i], target <= 10⁴`
* All integers in `nums` are unique.
* `nums` is sorted in ascending order.

---

## 📌 Key Takeaways

* Binary Search works on a sorted array.
* Use `low`, `mid`, and `high` to maintain the search range.
* Each comparison eliminates half of the search space.
* `low = mid + 1` searches the right half.
* `high = mid - 1` searches the left half.
* Binary Search reduces `O(n)` linear search to `O(log n)`.
