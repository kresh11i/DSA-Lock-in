**File name:** `LC - 18 4Sum.md`
**📁 Folder:** `Two_Pointer`

# 🧩 LeetCode 18 - 4Sum

## 🔗 Problem

Given an integer array `nums` and an integer `target`, return all unique quadruplets `[nums[i], nums[j], nums[k], nums[l]]` whose sum is equal to `target`.

Each quadruplet should contain four different indices, and duplicate quadruplets should not be included.

---

## 🏷️ Tags

* Array
* Sorting
* Two Pointer
* Duplicate Handling

---

## 📚 Topics

* Arrays
* Sorting
* Two Pointers
* Nested Loops

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

The problem asks us to find **four numbers** whose sum is equal to the given `target`.

A brute-force approach would use four nested loops, but that would take `O(n⁴)` time.

Instead, I first sort the array and fix the first two elements using `i` and `j`.

Then I use two pointers:

* `k` starts from `j + 1`.
* `l` starts from the last index.

Now I only need to find the remaining two numbers using the two-pointer technique.

The basic idea is:

```text
sum < target  → k++
sum > target  → l--
sum == target → store the quadruplet
```

Sorting also makes it easier to skip duplicate values.

---

## 🧠 Thought Process

### Step 1 : Sort the Array

First, sort the array.

```java
Arrays.sort(nums);
```

Example:

```text
nums = [1,0,-1,0,-2,2]

After sorting:

[-2,-1,0,0,1,2]
```

Now the elements are in increasing order, so moving `k` forward increases the sum and moving `l` backward decreases the sum.

---

### Step 2 : Fix the First Element

Use `i` to fix the first element.

```java
for (int i = 0; i < nums.length; i++) {
```

If the current value is the same as the previous value, skip it.

```java
if (i > 0 && nums[i] == nums[i - 1]) {
    continue;
}
```

This prevents duplicate quadruplets.

---

### Step 3 : Fix the Second Element

Inside the `i` loop, use `j` to fix the second element.

```java
for (int j = i + 1; j < nums.length; j++) {
```

Again, skip duplicate values of `j`.

```java
if (j != (i + 1) && nums[j] == nums[j - 1]) {
    continue;
}
```

Now the first two elements are fixed.

```text
nums[i]
nums[j]
```

---

### Step 4 : Use Two Pointers

Now initialize:

```java
int k = j + 1;
int l = nums.length - 1;
```

So the four elements are:

```text
nums[i] + nums[j] + nums[k] + nums[l]
```

I use `long` while calculating the sum because the values can be large and using `int` may cause integer overflow.

```java
long num = (long) nums[i] + nums[j];
long sum = num + nums[k] + nums[l];
```

---

### Step 5 : Compare the Sum

If the sum is smaller than the target:

```java
if (sum < target) {
    k++;
}
```

Since the array is sorted, increasing `k` gives a larger value and therefore increases the sum.

If the sum is greater than the target:

```java
else if (sum > target) {
    l--;
}
```

Moving `l` backward gives a smaller value and decreases the sum.

If the sum equals the target:

```java
else if (sum == target) {
    list.add(Arrays.asList(nums[i], nums[j], nums[k], nums[l]));
```

The quadruplet is added to the answer.

Then both pointers are moved:

```java
k++;
l--;
```

---

### Step 6 : Skip Duplicate Pointers

After finding a valid quadruplet, duplicate values of `k` are skipped.

```java
while (k < l && nums[k] == nums[k - 1]) {
    k++;
}
```

Similarly, duplicate values of `l` are skipped.

```java
while (k < l && nums[l] == nums[l + 1]) {
    l--;
}
```

This ensures that the same quadruplet is not added again.

---

## 🔍 Dry Run

Input:

```text
nums = [1,0,-1,0,-2,2]
target = 0
```

After sorting:

```text
[-2,-1,0,0,1,2]
```

### Finding `[-2,-1,1,2]`

```text
i = -2
j = -1
k = 1
l = 2

sum = -2 + (-1) + 1 + 2
sum = 0
```

So:

```text
[-2,-1,1,2] ✔
```

### Finding `[-2,0,0,2]`

```text
i = -2
j = 0
k = 0
l = 2

sum = -2 + 0 + 0 + 2
sum = 0
```

So:

```text
[-2,0,0,2] ✔
```

### Finding `[-1,0,0,1]`

```text
i = -1
j = 0
k = 0
l = 1

sum = -1 + 0 + 0 + 1
sum = 0
```

So:

```text
[-1,0,0,1] ✔
```

Final answer:

```text
[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

---

## 💻 Java Solution

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        List<List<Integer>> list = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }

            for (int j = i + 1; j < nums.length; j++) {
                int k = j + 1, l = nums.length - 1;

                if (j != (i + 1) && nums[j] == nums[j - 1]) {
                    continue;
                }

                while (k < l) {
                    long num = (long) nums[i] + nums[j];
                    long sum = num + nums[k] + nums[l];

                    if (sum < target) {
                        k++;
                    } else if (sum > target) {
                        l--;
                    } else if (sum == target) {
                        list.add(Arrays.asList(nums[i], nums[j], nums[k], nums[l]));

                        k++;
                        l--;

                        //skip dup of k
                        while (k < l && nums[k] == nums[k - 1]) {
                            k++;
                        }

                        //skip dup of l
                        while (k < l && nums[l] == nums[l + 1]) {
                            l--;
                        }
                    }
                }
            }
        }

        return list;
    }
}
```

---

## ⭐ Main Logic

```java
long num = (long) nums[i] + nums[j];
long sum = num + nums[k] + nums[l];

if (sum < target) {
    k++;
} else if (sum > target) {
    l--;
} else if (sum == target) {
    list.add(Arrays.asList(nums[i], nums[j], nums[k], nums[l]));

    k++;
    l--;
}
```

### Why is this the Main Logic?

* `i` fixes the first number.
* `j` fixes the second number.
* `k` searches for the third number.
* `l` searches for the fourth number.
* `k++` increases the sum.
* `l--` decreases the sum.
* When the sum equals `target`, the quadruplet is stored.
* Duplicate values are skipped to avoid duplicate answers.

---

## 🎯 Interview Takeaway

4Sum is basically an extension of the **3Sum pattern**.

Instead of:

```text
Fix 1 element + Two Pointer
```

we do:

```text
Fix 2 elements + Two Pointer
```

This reduces the brute-force `O(n⁴)` approach to `O(n³)`.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n³)
```

* Sorting takes `O(n log n)`.
* The `i` loop and `j` loop fix two elements.
* The two-pointer traversal takes `O(n)`.
* Overall complexity is `O(n³)`.

### Space Complexity

```text
O(1)
```

Only pointer and temporary variables are used apart from the output list.

---

## 📌 Constraints

* `1 <= nums.length <= 200`
* `-10⁹ <= nums[i] <= 10⁹`
* `-10⁹ <= target <= 10⁹`

---

## 📌 Key Takeaways

* Sort the array before using the two-pointer technique.
* Fix two elements using `i` and `j`.
* Use `k` and `l` to find the remaining two elements.
* If `sum < target`, move `k` forward.
* If `sum > target`, move `l` backward.
* Skip duplicates at every pointer level.
* Use `long` to safely handle large sums.
* 4Sum reduces the brute-force `O(n⁴)` approach to `O(n³)`.
