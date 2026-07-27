# Two Sum (Optimal)

## 🔗 Problem Link

https://leetcode.com/problems/two-sum/

## 🏷️ Tags

- Array
- Hash Table

## 📚 Topics

- Array
- Hash Table

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input has exactly one solution, and you may not use the same element twice.

The answer can be returned in any order.

---

## ✨ Examples

### Example 1

```text
Input: nums = [2,7,11,15], target = 9

Output: [0,1]
```

### Example 2

```text
Input: nums = [3,2,4], target = 6

Output: [1,2]
```

### Example 3

```text
Input: nums = [3,3], target = 6

Output: [0,1]
```

---

## 🚀 Approach

### Pattern Used

**Hash Table**

### Intuition

Instead of checking every possible pair, store the elements that have already been visited in a `HashMap`.

For every element, calculate the required complement (`target - currentElement`). If the complement is already present in the `HashMap`, we have found the answer.

### Why This Approach Works

A `HashMap` provides **O(1)** average lookup time.

Instead of searching the remaining array for every element, we directly check whether the required complement already exists.

This reduces the time complexity from **O(n²)** to **O(n)**.

### Algorithm

1. Create an empty `HashMap`.
2. Traverse the array.
3. Calculate the required complement.
4. Check whether the complement exists in the `HashMap`.
5. If it exists, return both indices.
6. Otherwise, store the current element and its index in the `HashMap`.
7. Continue until the answer is found.

---

## 💻 Java Solution

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        int[] arr = new int[2];
        HashMap<Integer, Integer> map = new HashMap<>();

        for(int i = 0; i < nums.length; i++){

            int ans = target - nums[i];

            if(map.containsKey(ans)){
                arr[0] = map.get(ans);
                arr[1] = i;
            }else{
                map.put(nums[i], i);
            }

        }

        return arr;
    }
}
```

---

## ⭐ Main Logic

```java
int ans = target - nums[i];

if(map.containsKey(ans)){
    arr[0] = map.get(ans);
    arr[1] = i;
}
```

### Why is this the Main Logic?

This is the heart of the algorithm.

- Calculate the required complement.
- Check if it has already been seen.
- If yes, immediately return the pair of indices.

> **Interview Takeaway:**  
> Whenever a problem asks to find a pair with a given target, think of using a **HashMap** to store previously visited elements.

---

## 🧪 Dry Run

### Input

```text
nums = [2,7,11,15]
target = 9
```

### Initial State

```text
map = {}
```

| i | nums[i] | Required (`target - nums[i]`) | HashMap | Action |
|---|---------|-------------------------------|---------|--------|
|0|2|7|{}|Store (2 → 0)|
|1|7|2|{2 → 0}|2 Found ✅ Return [0,1]|

### Final Output

```text
[0,1]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The array is traversed only once.
- HashMap lookup takes **O(1)** on average.

### Space Complexity

**O(n)**

- In the worst case, all elements are stored in the `HashMap`.

---

## 📌 Constraints

- `2 <= nums.length <= 10⁴`
- `-10⁹ <= nums[i] <= 10⁹`
- `-10⁹ <= target <= 10⁹`
- Exactly one valid answer exists.

---

## 💡 Key Points

- Store previously visited elements.
- Calculate the required complement.
- HashMap lookup is **O(1)** on average.
- Return indices, not values.
- Avoid nested loops.
- One traversal is enough.

---

## ⚠️ Common Mistakes

- Storing the current element before checking the complement.
- Returning the values instead of the indices.
- Forgetting that the HashMap stores **value → index**.
- Using the same element twice.
- Using nested loops even after choosing a HashMap.

---

## 📝 Revision Snapshot

**Problem Type:** Pair Sum

**Pattern Used:** Hash Table

**Main Data Structure:** HashMap

**Main Formula:**

```text
Required Complement = target - currentElement
```

**Key Idea:**

For every element, calculate the required complement and check whether it already exists in the `HashMap`. If it exists, return both indices immediately. Otherwise, store the current element and continue.