# 3Sum

## 🔗 Problem Link

[LeetCode 15 - 3Sum](https://leetcode.com/problems/3sum/)

## 🏷️ Tags

* Array
* Sorting
* Two Pointer
* Duplicate Handling

## 📚 Topics

* Array
* Two Pointers
* Sorting

## 📊 Difficulty

Medium

## 📖 Problem Statement

Given an integer array `nums`, find all unique triplets whose sum is equal to `0`.

Each triplet should contain three different indices, and duplicate triplets should not be included.

---

## ✨ Examples

### Example 1

```text
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

### Example 2

```text
Input: nums = [0,1,1]
Output: []
```

### Example 3

```text
Input: nums = [0,0,0]
Output: [[0,0,0]]
```

---

## 🚀 Approach

### Pattern Used

**Sorting + Two Pointer**

### Intuition

First, sort the array. Sorting makes it easier to use two pointers and also helps in skipping duplicate values.

I fix one element using `i`. For every `i`, I use two pointers:

* `j` starts from `i + 1`.
* `k` starts from the last index.

Then I calculate:

```text
sum = nums[i] + nums[j] + nums[k]
```

If the `sum` is less than `0`, I increase `j` because I need a bigger value.

If the `sum` is greater than `0`, I decrease `k` because I need a smaller value.

If the `sum` is `0`, I found a valid triplet, so I add it to the result and move both pointers.

I also skip duplicate values for `i`, `j`, and `k` so that the same triplet is not added more than once.

### Why This Approach Works

After sorting, the values are arranged in increasing order. So pointer movement becomes predictable.

* `sum < 0` → `j++`
* `sum > 0` → `k--`
* `sum == 0` → add the triplet and move both pointers

For example, after sorting:

```text
[-4,-1,-1,0,1,2]
```

When `i` points to `-1`:

```text
[-1,-1,2] → sum = 0
[-1,0,1]  → sum = 0
```

The duplicate `-1` is skipped for `i`, and duplicate values for `j` and `k` are also skipped after finding a triplet.

### Algorithm

1. Sort the array.
2. Traverse the array using `i`.
3. Skip duplicate values for `i`.
4. Set `j = i + 1` and `k = n - 1`.
5. Calculate the sum of `nums[i]`, `nums[j]`, and `nums[k]`.
6. If the sum is less than `0`, increment `j`.
7. If the sum is greater than `0`, decrement `k`.
8. If the sum is `0`, add the triplet to `list`.
9. Move both `j` and `k`.
10. Skip duplicate values for `j` and `k`.
11. Return `list`.

---

## 💻 Java Solution

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {

        Arrays.sort(nums);

        int n = nums.length;
        List<List<Integer>> list = new ArrayList<>();

        for (int i = 0; i < n; i++) {

            // skip duplicate i
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }

            int j = i + 1;
            int k = n - 1;

            while (j < k) {

                int sum = nums[i] + nums[j] + nums[k];

                if (sum < 0) {
                    j++;
                }

                else if (sum > 0) {
                    k--;
                }

                else {
                    // found triplet
                    list.add(Arrays.asList(nums[i], nums[j], nums[k]));

                    j++;
                    k--;

                    // skip duplicate j
                    while (j < k && nums[j] == nums[j - 1]) {
                        j++;
                    }

                    // skip duplicate k
                    while (j < k && nums[k] == nums[k + 1]) {
                        k--;
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
int sum = nums[i] + nums[j] + nums[k];

if (sum < 0) {
    j++;
}

else if (sum > 0) {
    k--;
}

else {
    list.add(Arrays.asList(nums[i], nums[j], nums[k]));

    j++;
    k--;
}
```

### Why is this the Main Logic?

* `i` fixes the first element of the triplet.
* `j` is used to increase the sum.
* `k` is used to decrease the sum.
* When the sum becomes `0`, the triplet is added to `list`.
* Duplicate values are skipped to prevent repeated answers.

> 💡 **Interview Takeaway:**
> When looking for unique triplets, sorting + fixing one element + two pointers is an important pattern to recognize.

---

## 🧪 Dry Run

### Input

```text
nums = [-1,0,1,2,-1,-4]
```

### Sorted Array

```text
[-4,-1,-1,0,1,2]
```

| Index | `nums[i]` | `j` | `k` | Sum | Action          |
| ----: | --------: | --: | --: | --: | --------------- |
|     0 |        -4 |   1 |   5 |  -3 | `j++`           |
|     0 |        -4 |   2 |   5 |  -3 | `j++`           |
|     0 |        -4 |   3 |   5 |  -2 | `j++`           |
|     0 |        -4 |   4 |   5 |  -1 | `j++`           |
|     1 |        -1 |   2 |   5 |   0 | Add `[-1,-1,2]` |
|     1 |        -1 |   3 |   4 |   0 | Add `[-1,0,1]`  |

The next `-1` is skipped because it is a duplicate of the previous `i`.

### Final Output

```text
[[-1,-1,2],[-1,0,1]]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n²)**

* Sorting takes `O(n log n)`.
* For every `i`, the two pointers traverse the remaining array in `O(n)`.
* Overall complexity is `O(n²)`.

### Space Complexity

**O(1)**

* Only a few variables and pointers are used.
* No additional searching data structure is required apart from the output list.

---

## 📌 Constraints

* `3 <= nums.length <= 3000`
* `-10^5 <= nums[i] <= 10^5`

---

## 💡 Key Points

* Sort the array before applying two pointers.
* Fix one element using `i`.
* Use `j` and `k` to search for the remaining two elements.
* Move `j` when the sum is too small.
* Move `k` when the sum is too large.
* Skip duplicates to avoid repeated triplets.
* This reduces the brute-force `O(n³)` approach to `O(n²)`.

---

## ⚠️ Common Mistakes

* Forgetting to sort the array.
* Not skipping duplicate values for `i`.
* Not skipping duplicate values for `j` and `k`.
* Forgetting to move both pointers after finding a valid triplet.
* Using three nested loops and getting `O(n³)` time.

---

## 📕 Revision Snapshot

**Problem Type:** Array / Triplet Sum

**Pattern Used:** Sorting + Two Pointer

**Main Data Structure:** Array + List

**Main Logic:**

```java
if (sum < 0) {
    j++;
}
else if (sum > 0) {
    k--;
}
else {
    list.add(Arrays.asList(nums[i], nums[j], nums[k]));

    j++;
    k--;
}
```

**Key Idea:**

Fix one element and use two pointers to find the other two elements. Sorting makes pointer movement predictable and helps in handling duplicates efficiently.
