# Majority Element

## 🔗 Problem Link

https://leetcode.com/problems/majority-element/

---

## 🏷️ Tags

- HashMap
- Frequency Counting

## 📚 Topics

- Array
- Hash Table
- Counting

---

## 📊 Difficulty

Easy

---

## 📖 Problem Statement

Given an integer array `nums` of size `n`, return the **majority element**.

The majority element is the element that appears **more than ⌊n / 2⌋ times**.

It is guaranteed that the majority element always exists.

---

## ✨ Examples

### Example 1

```text
Input:
nums = [3,2,3]

Output:
3
```

---

### Example 2

```text
Input:
nums = [2,2,1,1,1,2,2]

Output:
2
```

---

# 🚀 Approach

## Pattern Used

**HashMap (Frequency Counting)**

---

## Intuition

The majority element appears more than half of the array size.

So instead of checking every element repeatedly, we count how many times each number appears.

A HashMap stores:

```text
Number → Frequency
```

After counting all frequencies, we simply find the number whose frequency is greater than `n / 2`.

---

## Understanding the Pattern

Suppose

```text
nums = [2,2,1,1,1,2,2]
```

The HashMap becomes

```text
2 → 4

1 → 3
```

Array size

```text
7
```

Majority condition

```text
Frequency > 7 / 2

Frequency > 3
```

Since

```text
2 → 4
```

4 > 3

Therefore,

```text
Answer = 2
```

---

## Algorithm

1. Calculate `n / 2`.
2. Create a HashMap.
3. Traverse the array.
4. Count the frequency of every element.
5. Traverse the HashMap.
6. Return the key whose frequency is greater than `n / 2`.

---

## 💻 Java Solution

```java
class Solution {
    public int majorityElement(int[] nums) {

        int Mlen = nums.length / 2;
        int Melement = 0;

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {

            if (map.containsKey(nums[i])) {
                map.put(nums[i], map.get(nums[i]) + 1);
            } else {
                map.put(nums[i], 1);
            }
        }

        for (int key : map.keySet()) {
            if (map.get(key) > Mlen) {
                return key;
            }
        }

        return -1;
    }
}
```

---

# ⭐ Main Logic

### Step 1

Count the frequency of every number.

```java
if(map.containsKey(nums[i]))
    map.put(nums[i], map.get(nums[i]) + 1);
else
    map.put(nums[i], 1);
```

The HashMap stores

```text
Number → Frequency
```

---

### Step 2

Traverse the HashMap.

```java
for(int key : map.keySet())
```

Check every number's frequency.

---

### Step 3

If any frequency is greater than

```text
n / 2
```

return that number immediately.

```java
if(map.get(key) > Mlen)
    return key;
```

---

## 🧪 Dry Run

### Input

```text
nums = [2,2,1,1,1,2,2]
```

Threshold

```text
7 / 2 = 3
```

---

### Build HashMap

```text
2 → 1

2 → 2

1 → 1

1 → 2

1 → 3

2 → 3

2 → 4
```

Final Map

```text
{
2 = 4,
1 = 3
}
```

---

### Traverse Map

Check

```text
2 → 4
```

Since

```text
4 > 3
```

Return

```text
2
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n)
```

- One traversal to build the HashMap.
- One traversal through the HashMap.

---

### Space Complexity

```text
O(n)
```

HashMap stores the frequencies of elements.

---

## 📌 Constraints

- `1 <= nums.length <= 5 × 10⁴`
- `-10⁹ <= nums[i] <= 10⁹`
- The majority element always exists.

---

## 💡 Key Points

- Use a HashMap to count frequencies.
- Store

```text
Element → Frequency
```

- Majority means

```text
Frequency > n / 2
```

- Traverse the map once to find the answer.

---

## ⚠️ Common Mistakes

❌ Forgetting to increase the frequency.

```java
map.put(nums[i], map.get(nums[i]) + 1);
```

---

❌ Comparing with

```text
>= n / 2
```

The condition is

```text
> n / 2
```

---

❌ Forgetting to initialize a new element with frequency `1`.

---

## 📝 Revision Snapshot

**Problem Type**

Frequency Counting

---

**Pattern**

HashMap

---

**HashMap Stores**

```text
Element → Frequency
```

---

**Majority Condition**

```text
Frequency > n / 2
```

---

**Steps**

```text
Traverse Array

↓

Count Frequencies

↓

Traverse HashMap

↓

Return Frequency > n/2
```

---

**Time Complexity**

```text
O(n)
```

**Space Complexity**

```text
O(n)
```