**File name:** `LC - 540 Single Element in a Sorted Array.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 540 - Single Element in a Sorted Array

## 🔗 Problem

Given a sorted array where every element appears exactly twice except for one element that appears only once, find and return the single element.

The solution should run in `O(log n)` time and use `O(1)` extra space.

---

## 🏷️ Tags

* Array
* Binary Search
* Bitwise Pattern

---

## 📚 Topics

* Arrays
* Binary Search
* Pair Matching

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

Since the array is sorted, all duplicate elements appear next to each other.

Normally, the array follows this pattern:

```text
[1,1,2,2,3,3,4,4,5,5]
```

Before the single element, pairs follow:

```text
Even index → first element
Odd index  → second element
```

For example:

```text
Index:  0 1 2 3 4 5
Array:  [1,1,2,2,3,3]
         ↑ ↑ ↑ ↑ ↑ ↑
        pair pair pair
```

But after the single element, this pattern gets shifted.

So I use Binary Search to find where this pattern breaks.

The important part of my approach is checking whether `mid` belongs to a correctly aligned pair.

```text
mid is odd  → nums[mid] should equal nums[mid - 1]
mid is even → nums[mid] should equal nums[mid + 1]
```

If the pairing is correct, the single element is on the **right side**.

Otherwise, the single element is on the **left side**.

---

## 🧠 Thought Process

### Step 1 : Handle Edge Cases

If the array contains only one element:

```java
if (nums.length == 1) {
    return nums[0];
}
```

That element is obviously the answer.

I also check the first and last elements separately:

```java
if(nums[0]!=nums[1]){
    return nums[0];
}
```

and:

```java
if(nums[nums.length-1] != nums[nums.length-2]){
    return nums[nums.length-1];
}
```

This allows the main Binary Search to work safely from index `1` to `n - 2`.

---

### Step 2 : Set the Binary Search Range

```java
int low = 1, high = nums.length - 2;
```

I don't need to search the first and last positions because they were already handled.

---

### Step 3 : Check if `mid` is the Single Element

For every `mid`, I check both neighbours:

```java
if(nums[mid]!= nums[mid-1] && nums[mid]!= nums[mid+1]){
    return nums[mid];
}
```

If neither neighbour is equal to `nums[mid]`, then it is the only element and we have found the answer.

---

### Step 4 : Understand the Pair Pattern

This is the most important part.

Before the single element, pairs are aligned like:

```text
index:  0 1  2 3  4 5
        [1,1][2,2][3,3]
```

So:

```text
even index → pairs with right neighbour
odd index  → pairs with left neighbour
```

For example:

```text
mid = 3

nums[2] == nums[3]
```

This is the correct pairing.

But after the single element, the pattern shifts.

---

### Step 5 : Check Whether the Pairing is Correct

My condition is:

```java
if(mid%2==1 && nums[mid-1] == nums[mid] ||
   mid%2==0 && nums[mid]== nums[mid+1])
```

This checks whether `mid` is correctly paired according to the normal even-odd pattern.

For an odd `mid`:

```text
mid = 3
```

the expected pair is:

```text
nums[2] == nums[3]
```

For an even `mid`:

```text
mid = 4
```

the expected pair is:

```text
nums[4] == nums[5]
```

---

### Step 6 : Decide Which Half Contains the Answer

If the pairing is correct:

```java
low = mid + 1;
```

This means the single element must be somewhere to the **right**.

If the pairing is broken:

```java
high = mid - 1;
```

This means the single element is on the **left side**, including possibly around `mid`.

The whole idea is:

```text
Correct pair pattern
        ↓
Single element is RIGHT

Broken pair pattern
        ↓
Single element is LEFT
```

---

## 🔍 Dry Run

Input:

```text
nums = [1,1,2,3,3,4,4]
```

The single element is:

```text
3
```

Initial:

```text
low = 1
high = 5
```

### Iteration 1

```text
mid = (1 + 5) / 2
mid = 3

nums[mid] = 3
```

Check neighbours:

```text
nums[2] = 2
nums[4] = 3
```

Since:

```text
2 != 3
3 == 3
```

`mid` is not the single element.

Now:

```text
mid = 3
```

is odd.

For an odd index, the expected pair is:

```text
nums[mid - 1] == nums[mid]
```

But:

```text
2 != 3
```

So the normal pairing is broken.

Therefore:

```java
high = mid - 1;
```

---

### Iteration 2

```text
low = 1
high = 2

mid = 1
```

```text
nums[1] = 1
```

It is paired with:

```text
nums[0] = 1
```

Since `mid` is odd and:

```text
nums[mid - 1] == nums[mid]
```

the pairing is correct.

So the single element must be to the right:

```java
low = mid + 1;
```

Now:

```text
low = 2
```

---

### Iteration 3

```text
low = 2
high = 2

mid = 2
```

```text
nums[2] = 2
```

Its neighbours are:

```text
nums[1] = 1
nums[3] = 3
```

Neither is equal to `2`.

Therefore:

```text
2
```

is the single element.

### Final Answer

```text
2
```

---

## 💻 Java Solution

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        if (nums.length == 1) {
            return nums[0];
        }
        int low = 1, high = nums.length - 2;
        while (low <= high) {
            int mid = (low+high)/2;
            if(nums[0]!=nums[1]){
                return nums[0];
            }
            if(nums[nums.length-1] != nums[nums.length-2]){
                return nums[nums.length-1];
            }
            if(nums[mid]!= nums[mid-1] && nums[mid]!= nums[mid+1]){
                return nums[mid];
            }
            if(mid%2==1 && nums[mid-1] == nums[mid] || mid%2==0 && nums[mid]== nums[mid+1]){ 
                   low = mid+1;
                
            }else{
                high = mid-1;
            }
        }
        return -1;
    }
}
```

---

## ⭐ Main Logic

```java
if(mid%2==1 && nums[mid-1] == nums[mid] ||
   mid%2==0 && nums[mid]== nums[mid+1]){ 
    low = mid+1;
}else{
    high = mid-1;
}
```

### Why is this the Main Logic?

The array follows a fixed pair pattern before reaching the single element:

```text
Even index → pairs with next index
Odd index  → pairs with previous index
```

So I check whether `mid` follows this pattern.

If it does:

```text
pairing is still normal
→ single element is on the right
```

If it doesn't:

```text
pairing has already shifted
→ single element is on the left
```

This lets Binary Search locate the single element without checking every pair.

> 💡 **Interview Takeaway:**
> The key is not searching for the unique value directly. Instead, search for the point where the normal **even-odd pair pattern breaks**.

---

## 🎯 Key Pattern

Before the single element:

```text
[1,1] [2,2] [3,3] [4,4]
 ↑     ↑     ↑
0,1   2,3   4,5
```

The pattern is:

```text
even → next
odd  → previous
```

After the single element:

```text
[1,1] [2,2] [3] [4,4] [5,5]
 ↑     ↑      ↑
0,1   2,3    shifted
```

The pairing pattern gets shifted because of the single element.

So:

```text
Correct pairing → search RIGHT
Broken pairing  → search LEFT
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(log n)
```

Binary Search eliminates roughly half of the search space in every iteration.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Constraints

* `1 <= nums.length <= 10⁵`
* `0 <= nums[i] <= 10⁵`
* Every element appears exactly twice except for one element.
* The array is sorted in non-decreasing order.

---

## 📌 Key Takeaways

* Every element appears twice except one.
* Because the array is sorted, duplicates always appear next to each other.
* Before the single element, pairs follow the `even → odd` pattern.
* The single element breaks this pairing pattern.
* Use `mid` parity to check whether the pair is correctly aligned.
* Correct pairing means search right; broken pairing means search left.
* Binary Search gives `O(log n)` time and `O(1)` space.
