# Subarray Sum Equals K

## 🔗 Problem Link

https://leetcode.com/problems/subarray-sum-equals-k/

---

## 🏷️ Tags

- HashMap
- Prefix Sum

## 📚 Topics

- Array
- Hash Table
- Prefix Sum

---

## 📊 Difficulty

Medium

---

## 📖 Problem Statement

Given an integer array `nums` and an integer `k`, return the **total number of continuous subarrays** whose sum equals `k`.

---

## ✨ Examples

### Example 1

```text
Input:
nums = [1,1,1]
k = 2

Output:
2
```

Explanation

```text
Subarrays are:

[1,1]
   [1,1]
```

---

### Example 2

```text
Input:
nums = [1,2,3]
k = 3

Output:
2
```

Explanation

```text
Subarrays:

[1,2]
[3]
```

---

# 🚀 Approach

## Pattern Used

**Prefix Sum + HashMap**

---

## Intuition

The brute-force solution checks every possible subarray.

That takes **O(n²)** time.

Instead, we use **Prefix Sum**.

As we traverse the array, we keep track of the sum from the beginning up to the current index.

Then we ask:

> "Have I seen another prefix sum before such that removing it gives me exactly `k`?"

If yes, then a valid subarray exists.

---

## Understanding Prefix Sum

Prefix Sum means:

```text
Running Sum
```

For example,

```text
nums = [2,3,1,4]
```

Running sums become

```text
2
5
6
10
```

These values are called **Prefix Sums**.

---

## Main Formula

Suppose

```text
Current Prefix Sum = presum
```

We need

```text
Subarray Sum = k
```

We know

```text
Current Prefix Sum - Previous Prefix Sum = k
```

Rearranging,

```text
Previous Prefix Sum = Current Prefix Sum - k
```

which becomes

```java
need = presum - k;
```

If `need` already exists in the HashMap,

then we have found one (or more) valid subarrays.

---

## Why HashMap?

The HashMap stores

```text
Prefix Sum → Frequency
```

Example

```text
{
0 : 1,
3 : 2,
5 : 1,
8 : 1
}
```

Instead of searching every previous prefix sum,

we can find it instantly in **O(1)** time.

---

## Why do we write?

```java
map.put(0,1);
```

This is one of the most important lines.

Initially,

```text
Prefix Sum = 0
```

has already occurred **once**.

This helps when the subarray starts from index **0**.

Example

```text
nums = [2,3]
k = 5
```

Current Prefix Sum

```text
5
```

Need

```text
5 - 5 = 0
```

Since

```text
0
```

already exists,

we correctly count

```text
[2,3]
```

Without

```java
map.put(0,1);
```

this case would be missed.

---

## Why do we store Frequency?

Notice we store

```text
Prefix Sum → Frequency
```

instead of only

```text
Prefix Sum
```

Example

```text
nums = [1,-1,1,-1,1]
```

Prefix sums become

```text
1
0
1
0
1
```

Here,

Prefix Sum

```text
0
```

appears multiple times.

Each occurrence can create another valid subarray.

That's why we store the frequency.

---

## Algorithm

1. Create a HashMap.
2. Insert `(0,1)` into the map.
3. Maintain a running prefix sum.
4. Compute

```text
need = presum - k
```

5. If `need` exists, add its frequency to the answer.
6. Store the current prefix sum in the HashMap.
7. Continue until the end.

---

## 💻 Java Solution

```java
class Solution {
    public int subarraySum(int[] nums, int k) {

        HashMap<Integer, Integer> map = new HashMap<>();

        int cnt = 0;
        int presum = 0;

        map.put(0, 1);

        for (int i = 0; i < nums.length; i++) {

            presum += nums[i];

            int need = presum - k;

            if (map.containsKey(need)) {
                cnt += map.get(need);
            }

            if (map.containsKey(presum)) {
                map.put(presum, map.get(presum) + 1);
            } else {
                map.put(presum, 1);
            }
        }

        return cnt;
    }
}
```

---

# ⭐ Main Logic

### Step 1

Keep calculating the running prefix sum.

```java
presum += nums[i];
```

---

### Step 2

Find the prefix sum needed.

```java
need = presum - k;
```

If this value already exists,

then a subarray with sum `k` has been found.

---

### Step 3

Increase the answer.

```java
cnt += map.get(need);
```

Notice,

we add the **frequency**, not just `1`.

There may be multiple previous prefix sums with the same value.

---

### Step 4

Store the current prefix sum.

```java
map.put(presum,...)
```

so future elements can use it.

---

## 🧪 Dry Run

### Input

```text
nums = [1,2,3]
k = 3
```

Initially

```text
map = {0=1}

presum = 0

count = 0
```

---

### i = 0

```text
presum = 1

need = -2
```

Not found.

Store

```text
1
```

Map

```text
{0=1,1=1}
```

---

### i = 1

```text
presum = 3

need = 0
```

Found

```text
count = 1
```

Store

```text
3
```

Map

```text
{0=1,1=1,3=1}
```

---

### i = 2

```text
presum = 6

need = 3
```

Found

```text
count = 2
```

Store

```text
6
```

Final Answer

```text
2
```

---

## ⏱️ Complexity Analysis

### Time Complexity

```text
O(n)
```

Each element is processed once.

---

### Space Complexity

```text
O(n)
```

HashMap stores prefix sums.

---

## 📌 Constraints

- `1 <= nums.length <= 2 × 10⁴`
- `-1000 <= nums[i] <= 1000`
- `-10⁷ <= k <= 10⁷`

---

## 💡 Key Points

- Use Prefix Sum.
- HashMap stores **Prefix Sum → Frequency**.
- Formula:

```text
need = presum - k
```

- Insert

```java
map.put(0,1);
```

before starting.
- Store frequencies, not just values.
- Count all valid subarrays.

---

## ⚠️ Common Mistakes

❌ Forgetting

```java
map.put(0,1);
```

---

❌ Updating the HashMap before checking `need`.

Always check first.

---

❌ Storing only the prefix sum instead of its frequency.

Duplicate prefix sums are important.

---

❌ Adding `1` instead of

```java
map.get(need)
```

There may be multiple matching prefix sums.

---

## 📝 Revision Snapshot

**Problem Type**

Prefix Sum + HashMap

---

**Pattern**

Running Prefix Sum

---

**Formula**

```text
need = presum - k
```

---

**HashMap Stores**

```text
Prefix Sum → Frequency
```

---

**Most Important Line**

```java
map.put(0,1);
```

---

**Order**

```text
Update Prefix Sum

↓

Find need

↓

Increase count

↓

Store Prefix Sum
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