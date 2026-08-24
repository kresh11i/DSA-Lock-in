**File name:** `LC - 35 Search Insert Position.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 35 - Search Insert Position

## 🔗 Problem

Given a sorted array `nums` and a target value, return the index if the target is found.

If the target is not present, return the index where it should be inserted so that the array remains sorted.

The key idea behind this problem is **Lower Bound**.

---

## 🏷️ Tags

* Array
* Binary Search
* Lower Bound

---

## 📚 Topics

* Arrays
* Binary Search
* Lower Bound

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

This problem is basically asking us to find the **Lower Bound** of `target`.

### What is Lower Bound?

The **Lower Bound** of `target` is:

> The **first index** where `nums[index] >= target`.

In simple words:

```text
Find the first element that is greater than or equal to target.
```

For example:

```text
nums = [1,2,4,4,5,7]
target = 4
```

The first element `>= 4` is at index `2`.

```text
index:  0 1 2 3 4 5
nums:  [1,2,4,4,5,7]
            ↑
          answer
```

So the Lower Bound is:

```text
2
```

---

## 🧠 Thought Process

### Step 1 : Initialize Binary Search

```java
int low = 0, high = nums.length - 1;
```

I also initialize:

```java
int ans = nums.length;
```

Why `nums.length`?

Because the target might be greater than every element.

Example:

```text
nums = [1,2,3,4]
target = 7
```

There is no element `>= 7`.

So the target should be inserted at the end:

```text
index = 4
```

Therefore, `ans` initially stores `nums.length`.

---

### Step 2 : Find the Middle

```java
int mid = (low + high) / 2;
```

Now compare:

```text
nums[mid] >= target
```

This condition is the **heart of Lower Bound**.

---

### Step 3 : When `nums[mid] >= target`

```java
if(nums[mid]>=target){
    ans = mid;
    high = mid-1;
}
```

This means `mid` **can be the answer** because `nums[mid]` is greater than or equal to the target.

So I store:

```java
ans = mid;
```

But I don't stop.

Why?

Because I need the **first** position where `nums[index] >= target`.

There might be another valid position further to the left.

So I eliminate the right half:

```java
high = mid - 1;
```

This is the most important part of Lower Bound.

### Example

```text
nums = [1,2,4,4,4,7]
target = 4
```

Suppose:

```text
mid = 3
nums[mid] = 4
```

`4 >= 4`, so index `3` is a valid answer.

But there may be another `4` before it.

So:

```text
ans = 3
high = 2
```

We continue searching to the left.

Eventually:

```text
ans = 2
```

which is the **first** position where `nums[index] >= 4`.

---

### Step 4 : When `nums[mid] < target`

```java
else{
    low = mid+1;
}
```

If:

```text
nums[mid] < target
```

then `mid` cannot be the answer.

Everything before `mid` is also smaller because the array is sorted.

So we discard the left half:

```java
low = mid + 1;
```

---

## 🔍 Lower Bound Example

Consider:

```text
nums = [1,2,4,4,5,7]
target = 4
```

We want:

```text
first element >= 4
```

### Iteration 1

```text
low = 0
high = 5

mid = 2

nums[mid] = 4
```

Since:

```text
4 >= 4
```

Store:

```text
ans = 2
```

and search left:

```text
high = 1
```

### Iteration 2

```text
low = 0
high = 1

mid = 0

nums[mid] = 1
```

Since:

```text
1 < 4
```

Move right:

```text
low = 1
```

### Iteration 3

```text
low = 1
high = 1

mid = 1

nums[mid] = 2
```

Again:

```text
2 < 4
```

Move right:

```text
low = 2
```

Now:

```text
low > high
```

Search ends.

Final:

```text
ans = 2
```

---

## 🎯 Why This is Lower Bound

The standard Lower Bound template is:

```java
int low = 0;
int high = nums.length - 1;
int ans = nums.length;

while(low <= high){

    int mid = (low + high) / 2;

    if(nums[mid] >= target){
        ans = mid;
        high = mid - 1;
    }
    else{
        low = mid + 1;
    }
}
```

The important condition is:

```text
nums[mid] >= target
```

When this condition is true:

```text
answer = mid
```

but we continue searching **left** for an earlier valid position.

---

## 🧪 Dry Run

### Example 1

```text
nums = [1,3,5,6]
target = 5
```

```text
mid = 1
nums[mid] = 3

3 < 5
→ low = 2
```

Then:

```text
mid = 2
nums[mid] = 5

5 >= 5
→ ans = 2
→ high = 1
```

Final:

```text
2
```

---

### Example 2

```text
nums = [1,3,5,6]
target = 2
```

The first element greater than or equal to `2` is `3`.

```text
index:  0 1 2 3
nums:  [1,3,5,6]
          ↑
```

Answer:

```text
1
```

---

### Example 3

```text
nums = [1,3,5,6]
target = 7
```

No element is greater than or equal to `7`.

Therefore:

```text
ans = nums.length
ans = 4
```

The target would be inserted at index `4`.

---

## 💻 Java Solution

```java
class Solution {

    public int searchInsert(int[] nums, int target) {

        int low = 0 , high = nums.length-1;

        int ans = nums.length;

        while(low<=high){

            int mid = (low+high)/2;

            if(nums[mid]>=target){

                ans = mid;

                high = mid-1;

            }else{

                low = mid+1;

            }
        }

        return ans;

    }

}
```

---

## ⭐ Main Logic

```java
if(nums[mid] >= target){

    ans = mid;

    high = mid - 1;

}else{

    low = mid + 1;

}
```

### Why is this the Main Logic?

The condition:

```text
nums[mid] >= target
```

means `mid` is a **possible Lower Bound**.

So I save it:

```text
ans = mid
```

Then I search further left:

```text
high = mid - 1
```

because there might be an earlier index satisfying the same condition.

If:

```text
nums[mid] < target
```

then `mid` and everything before it are too small, so I search right:

```text
low = mid + 1
```

> 💡 **Interview Takeaway:**
> Lower Bound means **first index where `nums[index] >= target`**. Whenever you find a valid index, store it and continue searching to the left.

---

## 🎯 Lower Bound Pattern

```text
Condition:
nums[mid] >= target

       TRUE
        ↓
   ans = mid
        ↓
 search LEFT
 high = mid - 1

       FALSE
        ↓
 search RIGHT
 low = mid + 1
```

Remember:

```text
Lower Bound
= First element >= target
```

Examples:

```text
[1,2,4,4,5,7]
target = 4

Lower Bound = index 2
```

```text
[1,2,4,4,5,7]
target = 3

Lower Bound = index 2
```

```text
[1,2,4,4,5,7]
target = 8

Lower Bound = 6
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

Binary Search eliminates half of the search space in every iteration.

### Space Complexity

```text
O(1)
```

Only `low`, `high`, `mid`, and `ans` are used.

---

## 📌 Constraints

* `1 <= nums.length <= 10⁴`
* `-10⁴ <= nums[i] <= 10⁴`
* `nums` contains distinct values sorted in ascending order.
* `-10⁴ <= target <= 10⁴`

---

## 📌 Key Takeaways

* **Lower Bound = first index where `nums[index] >= target`.**
* If `nums[mid] >= target`, store `mid` and search left.
* If `nums[mid] < target`, search right.
* Initialize `ans = nums.length` for the case where the target is larger than every element.
* Search Insert Position is essentially a **Lower Bound Binary Search**.
* Time complexity is `O(log n)` and space complexity is `O(1)`.
