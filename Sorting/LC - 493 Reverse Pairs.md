**File name:** `LC - 493 Reverse Pairs.md`
**📁 Folder:** `Sorting`

# 🧩 LeetCode 493 - Reverse Pairs

## 🔗 Problem

Given an integer array `nums`, count the number of **reverse pairs**.

A reverse pair is a pair of indices `(i, j)` where:

```text
i < j
nums[i] > 2 * nums[j]
```

The goal is to count all such pairs efficiently.

---

## 🏷️ Tags

* Array
* Merge Sort
* Divide and Conquer
* Two Pointer

---

## 📚 Topics

* Arrays
* Merge Sort
* Divide and Conquer
* Counting Pairs

---

## 📊 Difficulty

Hard

---

## 💡 Intuition

A brute-force solution would check every possible pair `(i, j)` using two loops.

That would take:

```text
O(n²)
```

which is too slow for large arrays.

Instead, I use **Merge Sort**.

While performing merge sort, the left half and right half are already sorted. This allows me to efficiently count reverse pairs before merging the two halves.

For every element in the left half, I find how many elements in the right half satisfy:

```text
nums[i] > 2 * nums[j]
```

Since the right half is sorted, I can move a pointer only forward instead of checking every element again.

---

## 🧠 Thought Process

### Step 1 : Divide the Array

The `mergeSort()` function divides the array into smaller halves.

```java
int mid = (l + r) / 2;
```

Then recursively sort both halves:

```java
cnt += mergeSort(nums, l, mid);
cnt += mergeSort(nums, mid + 1, r);
```

This continues until each part contains only one element.

---

### Step 2 : Count Reverse Pairs

After both halves are sorted, I call:

```java
cnt += countPairs(nums, mid, r, l);
```

At this point:

```text
Left Half  → [l ... mid]
Right Half → [mid + 1 ... r]
```

Both halves are already sorted.

I use `right` to traverse the right half.

```java
int right = mid + 1;
```

For every element in the left half:

```java
for (int i = l; i <= mid; i++)
```

I move `right` while:

```java
nums[i] > 2L * nums[right]
```

The `2L` is important because it forces the multiplication to happen using `long`, preventing integer overflow.

---

### Step 3 : Count Valid Pairs

Suppose:

```text
Left  = [4, 5]
Right = [1, 2]
```

For `4`:

```text
4 > 2 × 1
4 > 2 ✔
```

So `(4,1)` is a reverse pair.

Also:

```text
4 > 2 × 2
4 > 4 ✖
```

So only one pair is counted.

The number of valid elements is:

```java
right - (mid + 1)
```

So:

```java
cnt += (right - (mid + 1));
```

Because the right half is sorted, once an element no longer satisfies the condition, all following elements will also fail for the current `i`.

---

### Step 4 : Merge the Two Sorted Halves

After counting all reverse pairs, I merge the two halves using the normal merge sort process.

```java
merge(nums, l, mid, r);
```

The merge step keeps the array sorted so that the next recursive level can efficiently count reverse pairs.

---

## 🔍 Dry Run

Input:

```text
nums = [1,3,2,3,1]
```

We need to find pairs where:

```text
i < j
nums[i] > 2 * nums[j]
```

Valid reverse pairs are:

```text
(3,1)
(3,1)
```

So the answer is:

```text
2
```

### During Merge Sort

Consider:

```text
Left  = [3]
Right = [1]
```

Check:

```text
3 > 2 × 1
3 > 2 ✔
```

So:

```text
count = 1
```

Another merge produces another valid pair.

Final count:

```text
2
```

---

## 💻 Java Solution

```java
class Solution {
    public int mergeSort(int[] nums, int l, int r) {
        int cnt = 0;
        if (l >= r){
            return 0;
        }

        int mid = (l + r) / 2;

        cnt +=mergeSort(nums, l, mid);
        cnt += mergeSort(nums, mid + 1, r);
        cnt += countPairs(nums, mid, r , l);
        merge(nums, l, mid, r);
        return cnt;
    }

    public void merge(int[] nums, int l ,int mid, int r) {
        if (l >= r) {
            return;
        }
        List<Integer> temp = new ArrayList<>();
        int left = l, right = mid + 1;
        while (left <= mid && right<= r) {
            if (nums[left] < nums[right]) {
                temp.add(nums[left]);
                left++;
            } else {
                temp.add(nums[right]);
                right++;
            }
        }
        while (left <= mid) {
            temp.add(nums[left]);
            left++;
        }
        while (right <= r) {
            temp.add(nums[right]);
            right++;
        }
        for (int i = 0; i < temp.size(); i++) {
            nums[l + i] = temp.get(i);
        }

    }

    public int countPairs(int[] nums, int mid, int r ,int l) {
        int cnt = 0;
        int right = mid + 1;
        for (int i = l; i <= mid; i++) {
            while (right <= r && nums[i] > 2L * nums[right]) {

                right++;
            }
            cnt += (right - (mid + 1));
        }
        return cnt;
    }

    public int reversePairs(int[] nums) {
        int l = 0,r = nums.length-1;
        return mergeSort(nums ,l,r);
    }

}
```

---

## ⭐ Main Logic

```java
int right = mid + 1;

for (int i = l; i <= mid; i++) {
    while (right <= r && nums[i] > 2L * nums[right]) {
        right++;
    }

    cnt += (right - (mid + 1));
}
```

### Why is this the Main Logic?

* The left and right halves are already sorted.
* `right` checks how many elements in the right half satisfy the reverse pair condition.
* Since the right half is sorted, `right` never needs to move backward.
* `right - (mid + 1)` gives the number of valid elements for the current `i`.
* `2L` prevents overflow while calculating `2 * nums[right]`.

> 💡 **Interview Takeaway:**
> When a pair-counting problem has a condition involving two sorted halves, Merge Sort can often reduce an `O(n²)` solution to `O(n log n)`.

---

## 🎯 Key Pattern

```text
Divide
   ↓
Sort Left Half
   ↓
Sort Right Half
   ↓
Count Reverse Pairs
   ↓
Merge
```

The important trick is:

```text
Count pairs BEFORE merging
```

because both halves are already sorted at that point.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n log n)
```

* Merge Sort has `O(log n)` levels.
* Each level processes the array in `O(n)`.
* Counting pairs and merging are both linear at each level.

Overall:

```text
O(n log n)
```

### Space Complexity

```text
O(n)
```

The temporary `ArrayList` used during merging requires additional space proportional to the array size.

---

## 📌 Constraints

* `1 <= nums.length <= 5 * 10⁴`
* `-2³¹ <= nums[i] <= 2³¹ - 1`

---

## 📌 Key Takeaways

* Reverse Pairs can be solved efficiently using **Merge Sort**.
* Count reverse pairs while the left and right halves are already sorted.
* Use a separate pointer for the right half instead of checking every pair.
* Use `2L * nums[right]` to avoid integer overflow.
* Count pairs before merging the two halves.
* The final complexity is `O(n log n)` instead of `O(n²)`.
