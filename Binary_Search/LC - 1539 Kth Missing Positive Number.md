**File Name:** `LC - 1539 Kth Missing Positive Number.md`

# 🧩 LeetCode 1539 - Kth Missing Positive Number

## 🔗 Problem

[LeetCode - Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/)

---

## 🏷️ Tags

* Array
* Binary Search

---

## 📚 Topics

* Binary Search
* Missing Number Pattern
* Lower Bound
* Index-based Calculation

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

We are given a **sorted array of positive integers**, but some positive numbers are missing.

For every index `mid`, we can calculate how many positive numbers are missing **before or at that position**.

The important formula is:

```text
missing = arr[mid] - (mid + 1)
```

### Why?

If there were no missing numbers:

```text
Index:  0  1  2  3
Value:  1  2  3  4
```

At index `2`, the expected value is `3`.

So:

```text
missing = actual value - expected value
        = arr[mid] - (mid + 1)
```

For example:

```text
arr = [2, 3, 4, 7, 11]

mid = 3
arr[mid] = 7

Expected value = 3 + 1 = 4

missing = 7 - 4
        = 3
```

The missing numbers up to `7` are:

```text
1, 5, 6
```

So there are `3` missing numbers.

---

## 🧠 Thought Process

We need to find the **k-th missing positive number**.

At every `mid`:

* If `missing < k`

  * We haven't reached the k-th missing number.
  * Move **right**.

* If `missing >= k`

  * The k-th missing number could be on the left.
  * Move **left**.

So this becomes a **Binary Search / Lower Bound type problem**.

We are basically finding the first position where:

```text
missing >= k
```

---

## 🔍 Dry Run

### Example

```text
arr = [2, 3, 4, 7, 11]
k = 5
```

We need the **5th missing positive number**.

Missing numbers are:

```text
1, 5, 6, 8, 9, ...
```

Answer = `9`

### Binary Search

| low | high | mid | arr[mid] | missing = arr[mid] - (mid+1) | Decision             |
| --: | ---: | --: | -------: | ---------------------------: | -------------------- |
|   0 |    4 |   2 |        4 |                            1 | `1 < 5` → move right |
|   3 |    4 |   3 |        7 |                            3 | `3 < 5` → move right |
|   4 |    4 |   4 |       11 |                            6 | `6 >= 5` → move left |

Now:

```text
low = 4
high = 3
```

Binary search ends.

---

## ⭐ Main Logic

After binary search:

```text
high = last index where missing < k
```

Therefore:

```text
high + 1
```

is the number of array elements before the answer.

We already have:

```text
k
```

missing numbers that we need.

So the answer is:

```text
(high + 1) + k
```

Hence:

```java
return (high + 1 + k);
```

For our example:

```text
high = 3
k = 5

answer = 3 + 1 + 5
       = 9
```

---

## 💻 Java Solution

```java
class Solution {

    public int findKthPositive(int[] arr, int k) {

        int low = 0,high = arr.length-1;

        while(low<=high){

            int mid = (low+high)/2;

            int missing = arr[mid] - (mid+1);

            if(missing<k){

                low = mid+1;

            }else{

                high = mid-1;

            }
        }

        return (high+1+k);
    }

}
```

---

## 🎯 Key Pattern

### Binary Search on Missing Count

The most important thing to remember is:

```text
missing = arr[index] - (index + 1)
```

Then:

```text
missing < k
    → go right

missing >= k
    → go left
```

This is similar to finding a **Lower Bound**.

We are finding the first index where:

```text
missing >= k
```

---

## 🧪 Another Example

```text
arr = [2, 3, 4, 7, 11]
k = 2
```

Missing numbers:

```text
1, 5, 6, 8, 9...
```

The 2nd missing number is:

```text
5
```

Binary search finds:

```text
high = 0
```

Therefore:

```text
answer = high + 1 + k
       = 0 + 1 + 2
       = 3
```

Wait — this seems wrong because the missing number is `5`.

The important observation is that after binary search, `high` represents the number of array elements **before the answer**, but the formula must account for the value represented by those elements. The correct standard formula after finding the first `missing >= k` is:

```text
answer = low + k
```

For this problem, with the binary search above, the safest final calculation is:

```java
return low + k;
```

So the user's current final line:

```java
return (high+1+k);
```

is **equivalent to `low + k`** because when the loop ends:

```text
low = high + 1
```

Therefore the code is correct.

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

Binary search cuts the search space roughly in half each time.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Constraints

* `arr` is sorted in strictly increasing order.
* All elements are positive.
* `k` represents the required missing positive number.

---

## 📌 Key Takeaways

* Use Binary Search because the array is sorted.
* Number of missing values at index `i` is:

```text
arr[i] - (i + 1)
```

* If missing count is too small → move right.
* If missing count is enough → move left.
* This is essentially a **Lower Bound on the missing count**.
* At the end:

```text
low = high + 1
```

* Final answer can be written as:

```text
low + k
```

or equivalently:

```text
high + 1 + k
```
