**File Name:** `LC - 410 Split Array Largest Sum.md`

# 🧩 LeetCode 410 - Split Array Largest Sum

## 🔗 Problem

[LeetCode 410: Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)

---

## 🏷️ Tags

* Array
* Binary Search
* Binary Search on Answer
* Greedy

---

## 📚 Topics

* Binary Search on Answer
* Partitioning
* Minimum Maximum Problem
* Greedy Feasibility Check

---

## 📊 Difficulty

Hard

---

## 💡 Intuition

We have an array and need to split it into `k` **non-empty continuous subarrays**.

Our goal is to **minimize the largest sum** among those subarrays.

For example:

```text
nums = [7, 2, 5, 10, 8]
k = 2
```

One possible split:

```text
[7, 2, 5] → sum = 14
[10, 8]   → sum = 18
```

The largest sum is:

```text
18
```

We want to find the split where this largest sum is as small as possible.

This is exactly the **Binary Search on Answer** pattern.

---

## 🧠 Thought Process

Instead of directly trying every possible way to split the array, think about the **maximum sum allowed for one subarray**.

Let that maximum allowed sum be `mid`.

Now ask:

> Can I split the array into at most `k` subarrays such that no subarray has a sum greater than `mid`?

This becomes our feasibility check.

### Search Range

The smallest possible answer is the largest element:

```text
low = max(nums)
```

Because every element must belong to some subarray.

The largest possible answer is the total sum:

```text
high = sum(nums)
```

Because one subarray could contain the entire array.

So:

```text
max(nums) → sum(nums)
```

is our Binary Search range.

---

## 🔍 Dry Run

### Example

```text
nums = [7, 2, 5, 10, 8]
k = 2
```

Initial range:

```text
low = 10
high = 32
```

Suppose:

```text
mid = 21
```

Greedily create subarrays:

```text
[7, 2, 5] = 14
[10, 8]   = 18
```

Only `2` partitions are required.

```text
partitions = 2
k = 2
```

So `21` is possible.

We try a smaller maximum:

```text
high = mid - 1
```

---

Suppose:

```text
mid = 15
```

Allocation:

```text
[7, 2, 5] = 14
[10]       = 10
[8]        = 8
```

We need:

```text
3 partitions
```

But:

```text
3 > k
```

So `15` is too small.

Move right:

```text
low = mid + 1
```

Eventually Binary Search finds:

```text
18
```

One optimal split is:

```text
[7, 2, 5] = 14
[10, 8]   = 18
```

Therefore:

```text
Answer = 18
```

---

## ⭐ Main Logic

There are two main parts.

### 1. Binary Search

We search for the minimum possible maximum subarray sum.

```text
low = maximum element
high = total sum
```

For every `mid`:

```text
result = number of partitions required
```

Then:

```text
if result <= k
    → mid is possible
    → try smaller
    → high = mid - 1

else
    → mid is too small
    → need more partitions
    → low = mid + 1
```

---

### 2. Greedy Partitioning

The `split()` method calculates how many subarrays are required for a given `mid`.

We keep adding elements to the current subarray while:

```text
subArrSum + nums[i] <= mid
```

If adding the next element exceeds `mid`, we start a new subarray.

```text
partition++;
subArrSum = nums[i];
```

This gives us the minimum number of partitions required for that `mid`.

---

## 🎯 Key Pattern

### Binary Search on Answer

This problem follows the pattern:

```text
Minimize the maximum
        ↓
Binary Search on Answer
        ↓
Choose a possible maximum = mid
        ↓
Greedily check how many partitions are needed
        ↓
If partitions <= k → try smaller
        ↓
If partitions > k  → increase limit
```

The important question to recognize is:

> **"What is the minimum possible value of the maximum?"**

Whenever you see this type of problem, think about **Binary Search on Answer**.

---

## 💻 Java Solution

```java
class Solution {
    public int splitArray(int[] nums, int k) {
        int low = Arrays.stream(nums).max().getAsInt();
        int high = Arrays.stream(nums).sum();

        while(low <= high){
            int mid = (low + high) / 2;

            int result = split(nums, mid);

            if(result <= k){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }

        return low;
    }

    public int split(int[] nums, int mid){
        int partition = 1;
        int subArrSum = 0;

        for(int i = 0; i < nums.length; i++){
            if(subArrSum + nums[i] <= mid){
                subArrSum += nums[i];
            }else{
                partition++;
                subArrSum = nums[i];
            }
        }

        return partition;
    }
}
```

---

## 🧪 Another Example

```text
nums = [1, 4, 4]
k = 3
```

Since we need exactly `3` non-empty subarrays, the only possible split is:

```text
[1] [4] [4]
```

Largest sum:

```text
4
```

So:

```text
Answer = 4
```

The Binary Search lower bound is already:

```text
max(nums) = 4
```

which is also the answer.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n × log(sum(nums)))
```

For every Binary Search step, we scan the entire array to calculate the number of partitions.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Important Observations

### Why `low = max(nums)`?

Every element must belong to a subarray.

Therefore, the largest element itself determines the minimum possible maximum sum.

```text
low = max(nums)
```

### Why `high = sum(nums)`?

The entire array can be considered as one subarray.

```text
high = sum(nums)
```

### Why `result <= k` is valid?

If a maximum sum of `mid` allows us to split the array into **fewer than `k` partitions**, we can further split some of those partitions because all numbers are positive.

So `mid` is still feasible.

Therefore:

```text
result <= k
```

means the current `mid` is possible.

---

## 📌 Key Takeaways

* The problem asks to **minimize the largest subarray sum**.
* This is a classic **Binary Search on Answer** problem.
* Search range:

```text
max(nums) → sum(nums)
```

* `split()` greedily finds the minimum number of partitions needed for a given `mid`.
* If partitions `> k`:

  * Maximum allowed sum is too small.
  * Move right.
* If partitions `<= k`:

  * Maximum allowed sum is possible.
  * Try a smaller value.
* When Binary Search ends:

```text
low
```

is the minimum feasible maximum subarray sum.

### 🧠 Pattern to Remember

```text
Minimum possible maximum
          ↓
Binary Search on Answer
          ↓
Greedy feasibility check
          ↓
Return first feasible value
```
