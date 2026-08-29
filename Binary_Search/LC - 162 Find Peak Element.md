**File name:** `LC - 162 Find Peak Element.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 162 - Find Peak Element

## 🔗 Problem

Given an array `nums`, find a **peak element** and return its index.

A peak element is an element that is greater than its neighboring elements.

For the boundary elements, only the existing neighbour needs to be considered.

The problem guarantees that an answer exists, and we only need to return **any one peak**.

---

## 🏷️ Tags

* Array
* Binary Search
* Peak Element

---

## 📚 Topics

* Arrays
* Binary Search
* Divide and Conquer

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

A brute-force approach would check every element to find a peak.

But I can solve this using **Binary Search**.

The important observation is the direction of the array around `mid`.

If:

```text
nums[mid] < nums[mid + 1]
```

then the array is going **uphill**.

So there must be a peak somewhere on the **right side**.

If:

```text
nums[mid] > nums[mid + 1]
```

then the array is going **downhill**.

So there must be a peak on the **left side**, and `mid` itself can also be a peak.

This allows me to eliminate half of the array at every step.

I also handle the first and last elements separately because they can themselves be peaks.

---

## 🧠 Thought Process

### Step 1 : Handle Single Element

If the array contains only one element:

```java id="h9f0ol"
if(nums.length ==1){
    return 0;
}
```

That element is automatically a peak.

---

### Step 2 : Check the First Element

```java id="pjx2lw"
if(nums[0]>nums[1]){
    return 0;
}
```

If the first element is greater than its only neighbour, it is a peak.

Example:

```text id="z6h2nb"
[5,3,4,6]
 ↑
```

Since:

```text id="4xk0wt"
5 > 3
```

index `0` is a valid peak.

---

### Step 3 : Check the Last Element

Similarly:

```java id="jhrgxx"
if(nums[nums.length-1] > nums[nums.length-2]){
    return nums.length-1;
}
```

If the last element is greater than the element before it, it is a peak.

Example:

```text id="4h21fa"
[1,3,4,7]
       ↑
```

Since:

```text id="w9glv1"
7 > 4
```

index `3` is a peak.

---

### Step 4 : Search the Middle

Since both boundaries have already been handled, I search only between them:

```java id="n3c7hv"
int low = 1, high = nums.length-2;
```

Then calculate:

```java id="h8c5jk"
int mid = (low+high)/2;
```

---

### Step 5 : Check if `mid` is a Peak

The direct peak condition is:

```java id="7sp1gd"
if(nums[mid-1]< nums[mid] && nums[mid]> nums[mid+1]){
    return mid;
}
```

This means:

```text id="3b1xjt"
left < mid > right
```

So `mid` is a peak.

---

### Step 6 : If the Array is Going Up

If:

```java id="a3y6a6"
nums[mid-1] < nums[mid] && nums[mid] < nums[mid+1]
```

then:

```text id="jex4dc"
left < mid < right
```

The array is increasing at `mid`.

Example:

```text id="uv0s5q"
[1,3,5,7]
       ↑
      mid
```

Since the array is still going upward, a peak must exist somewhere to the right.

So:

```java id="2j16k2"
low = mid+1;
```

---

### Step 7 : If the Array is Going Down

If:

```java id="qu3x0x"
nums[mid-1]> nums[mid] && nums[mid] > nums[mid+1]
```

then:

```text id="0d3k9j"
left > mid > right
```

The array is going downward.

So there must be a peak somewhere on the left side.

Therefore:

```java id="7e4s3d"
high = mid-1;
```

---

### Step 8 : Handle the Remaining Case

The final `else` handles the case where:

```text id="g4cx7u"
nums[mid-1] < nums[mid]
nums[mid] > nums[mid+1]
```

is not the direct peak condition and the array is not strictly increasing or decreasing in the previous conditions.

In this situation, moving right is safe:

```java id="o8lq5y"
low = mid+1;
```

The important idea is that the search always moves toward a region where a peak must exist.

---

## 🔍 Dry Run

Input:

```text id="y2j3kg"
nums = [1,2,1,3,5,6,4]
```

First and last elements:

```text id="85n0v8"
1 < 2
4 < 6
```

So neither boundary is a peak.

Search:

```text id="0ekxgk"
low = 1
high = 5
```

### Iteration 1

```text id="9r7i3q"
mid = 3

nums[mid-1] = 1
nums[mid]   = 3
nums[mid+1] = 5
```

We have:

```text id="n2y1o3"
1 < 3 < 5
```

The array is going upward.

So:

```text id="48j3z4"
low = mid + 1
low = 4
```

---

### Iteration 2

```text id="jtwzjq"
low = 4
high = 5

mid = 4
```

Values:

```text id="w9q7xy"
3 < 5 > 6
```

Not a peak because:

```text id="xw78c0"
5 < 6
```

The array is still going upward.

So:

```text id="e8xwti"
low = 5
```

---

### Iteration 3

```text id="k0qg1q"
low = 5
high = 5

mid = 5
```

Values:

```text id="4zv0c1"
5 < 6 > 4
```

So `6` is a peak.

```text id="4i5o9j"
return 5
```

### Final Answer

```text id="5s2j4a"
5
```

---

## 💻 Java Solution

```java
class Solution {
    public int findPeakElement(int[] nums) {
        if(nums.length ==1){
            return 0;
        }
        if(nums[0]>nums[1]){
            return 0;
        }
        if(nums[nums.length-1] > nums[nums.length-2]){
            return nums.length-1;
        }
        int low = 1 , high = nums.length-2;
        while(low<=high){
            int mid = (low+high)/2;
            if(nums[mid-1]< nums[mid] && nums[mid]> nums[mid+1]){
                return mid;
            }else if(nums[mid-1] < nums[mid] && nums[mid] < nums[mid+1]){
                low = mid+1;
            }else if (nums[mid-1]> nums[mid]&& nums[mid] > nums[mid+1]){
                high = mid-1;

            }else{
                low = mid+1;
            }
       

        }
         return -1;
    }
}
```

---

## ⭐ Main Logic

```java
if(nums[mid-1] < nums[mid] && nums[mid] > nums[mid+1]){
    return mid;
}
else if(nums[mid-1] < nums[mid] && nums[mid] < nums[mid+1]){
    low = mid + 1;
}
else if(nums[mid-1] > nums[mid] && nums[mid] > nums[mid+1]){
    high = mid - 1;
}
else{
    low = mid + 1;
}
```

### Why is this the Main Logic?

The main thing I observe is the **direction of the slope** around `mid`.

```text id="l5nq1u"
Increasing:
nums[mid-1] < nums[mid] < nums[mid+1]
                         ↑
                    go RIGHT
```

If the array is increasing, I move right because a peak must eventually appear.

For a decreasing section:

```text id="jv5xqj"
nums[mid-1] > nums[mid] > nums[mid+1]
       ↑
   go LEFT
```

I move left because a peak exists somewhere in that direction.

And if:

```text id="q2x1r9"
nums[mid-1] < nums[mid] > nums[mid+1]
```

then `mid` itself is the peak.

> 💡 **Interview Takeaway:**
> You don't need to find the exact shape of the whole array. Just look at the slope around `mid` and move toward the side where a peak must exist.

---

## 🎯 Key Pattern

Think of the array as a mountain:

```text
        Peak
         /\
        /  \
       /    \
      /      \
```

At `mid`:

```text
Going UP
    ↓
nums[mid] < nums[mid+1]
    ↓
Move RIGHT
```

```text
Going DOWN
    ↓
nums[mid] > nums[mid+1]
    ↓
Move LEFT
```

```text
Peak found
    ↓
nums[mid-1] < nums[mid] > nums[mid+1]
    ↓
Return mid
```

The most useful simplified way to remember the Binary Search idea is:

```text
nums[mid] < nums[mid + 1] → RIGHT
nums[mid] > nums[mid + 1] → LEFT
```

---

## 🧪 Another Example

```text
nums = [1,2,3,1]
```

The array is increasing toward `3`.

```text
1 < 2 < 3 > 1
        ↑
       peak
```

When Binary Search sees:

```text
nums[mid] < nums[mid+1]
```

it moves right toward the peak.

The answer is:

```text
2
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

Binary Search eliminates half of the search space in each iteration.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Constraints

* `1 <= nums.length <= 1000`
* `-2³¹ <= nums[i] <= 2³¹ - 1`
* `nums[i] != nums[i + 1]` for all valid `i`.

---

## 📌 Key Takeaways

* A peak is an element greater than its neighbours.
* Check the slope around `mid` instead of searching every element.
* If the array is increasing, move right.
* If the array is decreasing, move left.
* If `nums[mid]` is greater than both neighbours, return `mid`.
* Boundary elements can also be peaks, so handle them separately.
* Binary Search gives `O(log n)` time and `O(1)` space.
