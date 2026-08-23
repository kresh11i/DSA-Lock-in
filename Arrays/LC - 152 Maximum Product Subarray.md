**File name:** `LC - 152 Maximum Product Subarray.md`
**📁 Folder:** `Arrays`

# 🧩 LeetCode 152 - Maximum Product Subarray

## 🔗 Problem

Given an integer array `nums`, find the contiguous subarray that has the largest product and return its product.

The subarray must contain at least one element.

---

## 🏷️ Tags

* Array
* Prefix Product
* Suffix Product
* Subarray

---

## 📚 Topics

* Arrays
* Prefix Traversal
* Suffix Traversal
* Dynamic Programming Concept

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

The main difficulty in this problem is handling **negative numbers and zeros**.

With a normal sum-based subarray problem, we can easily decide whether to extend or restart. But with multiplication, a negative number can change a small negative product into a large positive product.

For example:

```text
[-2, 3, -4]

(-2) × 3 × (-4) = 24
```

So I cannot simply discard negative products.

Instead, I use **prefix and suffix products**.

* `prefix` calculates the product from the left side.
* `suffix` calculates the product from the right side.
* Whenever a `0` is encountered, the product is reset to `1`.
* At every position, I update `max` using both `prefix` and `suffix`.

This allows us to handle negative numbers and zeros without explicitly storing the minimum product.

---

## 🧠 Thought Process

### Step 1 : Initialize Variables

```java
int max = Integer.MIN_VALUE;

int prefix = 1, suffix = 1;
```

`max` stores the maximum product found so far.

`prefix` stores the running product from the left.

`suffix` stores the running product from the right.

---

### Step 2 : Traverse From Both Directions

I use a single loop:

```java
for(int i = 0 ;i <nums.length ; i++)
```

For every `i`:

```text
prefix → nums[i]

suffix → nums[nums.length - i - 1]
```

So the prefix moves:

```text
Left → Right
```

while the suffix moves:

```text
Right → Left
```

---

### Step 3 : Reset After Zero

Before multiplying, I check whether the current product has become `0`.

```java
if(prefix == 0){
    prefix = 1;
}

if(suffix == 0){
    suffix = 1;
}
```

A zero breaks a subarray because any product containing zero becomes zero.

Resetting to `1` allows the next element to start a new product calculation.

Example:

```text
[2,3,0,4,5]
```

The prefix calculation becomes:

```text
2
6
0 → reset
4
20
```

---

### Step 4 : Calculate Prefix and Suffix Products

```java
prefix = prefix * nums[i];

suffix = suffix * nums[nums.length-i-1];
```

The prefix handles products from the left.

The suffix handles products from the right.

This is useful because when there are negative numbers, the maximum product may require removing a prefix or suffix containing a negative number.

---

### Step 5 : Update Maximum

At every position:

```java
max = Math.max(max , Math.max(prefix , suffix));
```

I compare:

```text
current prefix product
current suffix product
current maximum
```

and keep the largest value.

---

## 🔍 Dry Run

Input:

```text
nums = [2,3,-2,4]
```

We calculate products from both directions.

| `i` | Prefix | Suffix | `max` |
| --: | -----: | -----: | ----: |
|   0 |      2 |      4 |     4 |
|   1 |      6 |     -8 |     6 |
|   2 |    -12 |    -48 |     6 |
|   3 |    -48 |    -48 |     6 |

Final answer:

```text
6
```

The maximum product subarray is:

```text
[2,3]

2 × 3 = 6
```

---

### Example With Negative Numbers

Input:

```text
nums = [-2,3,-4]
```

The complete subarray gives:

```text
(-2) × 3 × (-4) = 24
```

The negative values cancel each other, giving the maximum product:

```text
24
```

This is why simply ignoring negative products would not work.

---

## 💻 Java Solution

```java
class Solution {

    public int maxProduct(int[] nums) {

        int max = Integer.MIN_VALUE;

        int prefix = 1, suffix = 1;

        for(int i = 0 ;i <nums.length ; i++){

            if(prefix == 0){

                prefix = 1;

            }

            if(suffix == 0){

                suffix = 1;

            }

            prefix = prefix* nums[i];

            suffix = suffix * nums[nums.length-i-1];

            max = Math.max(max , Math.max(prefix , suffix));

        }

        return max;

    }

}
```

---

## ⭐ Main Logic

```java
if(prefix == 0){
    prefix = 1;
}

if(suffix == 0){
    suffix = 1;
}

prefix = prefix * nums[i];

suffix = suffix * nums[nums.length-i-1];

max = Math.max(max , Math.max(prefix , suffix));
```

### Why is this the Main Logic?

* `prefix` keeps the product from the left.
* `suffix` keeps the product from the right.
* A `0` resets the product and starts a new subarray.
* Checking from both directions handles negative numbers effectively.
* `max` stores the largest product found during the traversal.

> 💡 **Interview Takeaway:**
> For maximum product subarray problems, negative numbers make the problem different from maximum sum. Prefix and suffix products provide a simple way to handle both negative values and zeros.

---

## 🎯 Key Pattern

```text
Prefix Product →→→→
               ↕
             Maximum
               ↕
Suffix Product ←←←←
```

The important idea is:

```text
Prefix + Suffix + Reset at Zero
```

This avoids using nested loops to calculate every possible subarray.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n)
```

The array is traversed only once, while calculating both prefix and suffix products in the same loop.

### Space Complexity

```text
O(1)
```

Only `max`, `prefix`, and `suffix` variables are used.

---

## 📌 Constraints

* `1 <= nums.length <= 2 * 10⁴`
* `-10 <= nums[i] <= 10`
* The product of any prefix or suffix fits within a 32-bit integer.

---

## 📌 Key Takeaways

* Negative numbers can turn a minimum product into a maximum product.
* Calculate products from both the prefix and suffix directions.
* Reset the running product after encountering `0`.
* Track the maximum product at every position.
* The solution works in `O(n)` time and `O(1)` extra space.
