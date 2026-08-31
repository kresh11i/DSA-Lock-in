**File name:** `LC - 875 Koko Eating Bananas.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 875 - Koko Eating Bananas

## 🔗 Problem

Koko has several piles of bananas and has `h` hours to finish eating all of them.

She can choose an eating speed of `k` bananas per hour. In each hour, she eats up to `k` bananas from one pile.

The goal is to find the **minimum eating speed `k`** that allows Koko to finish all the bananas within `h` hours.

---

## 🏷️ Tags

* Binary Search
* Array
* Binary Search on Answer

---

## 📚 Topics

* Arrays
* Binary Search
* Search Space
* Mathematical Calculation

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

Here, I am not searching for an element inside the array.

Instead, I am searching for the **minimum possible eating speed**.

The possible speed starts from:

```text
1
```

and the maximum speed needed can never be greater than the largest pile.

So:

```java id="g1c8zy"
int low = 1;
int high = Arrays.stream(piles).max().getAsInt();
```

For every possible speed `mid`, I calculate how many hours Koko would need to finish all the piles.

If the required hours are:

```text
total <= h
```

then this speed is possible.

But I want the **minimum possible speed**, so I try a smaller speed:

```java id="4z3q0h"
high = mid - 1;
```

If:

```text
total > h
```

the speed is too slow, so I increase it:

```java id="8y5n9f"
low = mid + 1;
```

This is called **Binary Search on Answer**.

---

## 🧠 Thought Process

### Step 1 : Understand the Search Space

The minimum possible speed is:

```text
1 banana/hour
```

The maximum required speed is the size of the largest pile.

For example:

```text id="4yq3m2"
piles = [3,6,7,11]
```

So:

```text
low = 1
high = 11
```

The answer must be somewhere between:

```text
[1 ... 11]
```

---

### Step 2 : Try a Middle Speed

```java id="9x3l0g"
int mid = (low + high) / 2;
```

This `mid` represents a possible eating speed.

For example:

```text
low = 1
high = 11

mid = 6
```

Now I ask:

> Can Koko finish all piles within `h` hours if she eats `6` bananas per hour?

I calculate that using `timeCalc()`.

---

### Step 3 : Calculate Required Hours

For every pile:

```java id="4ty1sr"
double value = (double) piles[i] / (double) mid;
totalHrs += Math.ceil(value);
```

The number of hours required for one pile is:

```text
ceil(pile / speed)
```

For example:

```text
pile = 7
speed = 3

7 / 3 = 2.33

ceil(2.33) = 3 hours
```

So Koko needs `3` hours for that pile.

---

### Step 4 : Decide Which Direction to Search

After calculating the total hours:

```java id="1l6s1p"
if (total <= h) {
    high = mid - 1;
}
```

If Koko can finish within the given hours, `mid` is a valid speed.

But I don't immediately return it because there may be a smaller valid speed.

So I search the left side.

```text id="72uvr6"
Possible speed
      ↓
   mid = 6
      ↓
total <= h
      ↓
Speed works ✔
      ↓
Try smaller speed
```

If:

```java id="4sl4e2"
total > h
```

then Koko cannot finish in time.

So I need a faster speed:

```java id="0h1g3e"
low = mid + 1;
```

---

### Step 5 : Why Return `low`?

At the end:

```java id="1t0jkn"
return low;
```

When Binary Search finishes:

```text id="w5q9a3"
low > high
```

`low` points to the **smallest speed that satisfies the condition**.

So `low` is the answer.

This is the same idea as finding the **first valid answer** in Binary Search.

---

## 🔍 Dry Run

Input:

```text id="3z9tqh"
piles = [3,6,7,11]
h = 8
```

Search space:

```text id="d4jjjv"
low = 1
high = 11
```

### Iteration 1

```text id="qak4bv"
mid = 6
```

Required hours:

```text id="0e2skh"
3 / 6 → 1 hour
6 / 6 → 1 hour
7 / 6 → 2 hours
11 / 6 → 2 hours
```

Total:

```text id="4cv7yz"
1 + 1 + 2 + 2 = 6
```

Since:

```text id="ryx1q0"
6 <= 8
```

speed `6` works.

Try smaller:

```text id="x3gy8f"
high = 5
```

---

### Iteration 2

```text id="17js8q"
low = 1
high = 5

mid = 3
```

Hours:

```text id="o0cqca"
3 / 3 → 1
6 / 3 → 2
7 / 3 → 3
11 / 3 → 4
```

Total:

```text id="s3y5m8"
1 + 2 + 3 + 4 = 10
```

Since:

```text id="hfrj0g"
10 > 8
```

speed `3` is too slow.

Increase speed:

```text id="44j8fr"
low = 4
```

---

### Iteration 3

```text id="39iw0x"
low = 4
high = 5

mid = 4
```

Hours:

```text id="v5p4tj"
3 / 4 → 1
6 / 4 → 2
7 / 4 → 2
11 / 4 → 3
```

Total:

```text id="i5r3c5"
1 + 2 + 2 + 3 = 8
```

Since:

```text id="f1c7cw"
8 <= 8
```

speed `4` works.

Try smaller:

```text id="x0k3t8"
high = 3
```

Now:

```text id="9o0qv9"
low = 4
high = 3
```

Search ends.

Therefore:

```text id="vpl6lf"
answer = low = 4
```

---

## 💻 Java Solution

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int low = 1, high = Arrays.stream(piles).max().getAsInt();
        while (low <= high) {
            int mid = (low + high) / 2;
            int total = timeCalc(mid, piles);
            if (total <= h) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return low;
    }

    public int timeCalc(int mid, int[] piles) {
        int totalHrs = 0;
        for (int i = 0; i < piles.length; i++) {
            double value = (double) piles[i] / (double) mid;
            totalHrs += Math.ceil(value);
        }
        return totalHrs;

    }
}
```

---

## ⭐ Main Logic

```java
int mid = (low + high) / 2;
int total = timeCalc(mid, piles);

if (total <= h) {
    high = mid - 1;
} else {
    low = mid + 1;
}
```

### Why is this the Main Logic?

The important thing is that the answer is a **speed**, not an index.

For every speed, there are only two possibilities:

```text
Speed works
    ↓
Try a smaller speed

Speed doesn't work
    ↓
Need a larger speed
```

So the search space behaves like:

```text
Too Slow → Too Slow → Too Slow → Works → Works → Works
                                      ↑
                                Minimum Answer
```

Binary Search finds the first speed where the condition becomes true.

> 💡 **Interview Takeaway:**
> When the answer lies within a numerical range and you can check whether a particular value is valid, think about **Binary Search on Answer**.

---

## 🎯 Key Pattern

```text
Search Space = Possible Eating Speeds

        1 ---------------- maxPile
        ↓
      Binary Search
        ↓
   Try speed = mid
        ↓
Calculate required hours
        ↓
 ┌───────────────┐
 │ total <= h ?  │
 └───────────────┘
      /       \
    YES        NO
     ↓          ↓
Try smaller   Try larger
speed         speed
     ↓          ↓
high=mid-1   low=mid+1
```

The key condition is:

```text
total hours <= h
```

This tells me whether the current speed is valid.

---

## 🧪 Another Example

```text
piles = [30,11,23,4,20]
h = 5
```

Try:

```text
speed = 23
```

Required hours:

```text
30 → 2
11 → 1
23 → 1
4  → 1
20 → 1

Total = 6
```

Since:

```text
6 > 5
```

speed `23` is too slow.

So I increase the speed.

The Binary Search continues until it finds the minimum speed that allows Koko to finish within `5` hours.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n log(max(piles)))
```

For every Binary Search step, I traverse all `n` piles to calculate the required hours.

The speed search range is from `1` to `max(piles)`.

### Space Complexity

```text
O(1)
```

Only a few variables are used apart from the input array.

---

## 📌 Constraints

* `1 <= piles.length <= 10⁴`
* `piles.length <= h <= 10⁹`
* `1 <= piles[i] <= 10⁹`

---

## 📌 Key Takeaways

* This is **Binary Search on Answer**, not normal Binary Search on an array.
* The search space is the possible eating speed from `1` to `max(piles)`.
* `ceil(pile / speed)` gives the hours needed for each pile.
* If `total <= h`, the speed works, so try a smaller speed.
* If `total > h`, the speed is too slow, so increase it.
* The final `low` represents the minimum valid eating speed.
* Time complexity is `O(n log(max(piles)))` and space complexity is `O(1)`.
