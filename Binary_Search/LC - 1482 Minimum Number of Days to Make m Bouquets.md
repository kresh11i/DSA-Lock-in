**File name:** `LC - 1482 Minimum Number of Days to Make m Bouquets.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 1482 - Minimum Number of Days to Make m Bouquets

## 🔗 Problem

Given an array `bloomDay`, where `bloomDay[i]` represents the day the `i`th flower blooms, find the **minimum number of days** needed to make `m` bouquets.

Each bouquet requires exactly `k` **adjacent flowers**, and a flower can only be used once.

If it is impossible to make `m` bouquets, return `-1`.

---

## 🏷️ Tags

* Array
* Binary Search
* Binary Search on Answer
* Greedy

---

## 📚 Topics

* Arrays
* Binary Search
* Search Space
* Greedy Counting

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

This is another **Binary Search on Answer** problem.

I am not searching for an element inside the array. Instead, I am searching for the **minimum number of days**.

The possible answer lies between:

```text
minimum bloom day → maximum bloom day
```

For a particular day `mid`, I check whether it is possible to make at least `m` bouquets.

The important part is that the flowers used for one bouquet must be **adjacent**.

So while traversing the array, I keep counting consecutive flowers that have already bloomed by day `mid`.

```text
bloomDay[i] <= mid
        ↓
Flower is available
        ↓
cnt++
```

When I find a flower that has not bloomed yet:

```text
bloomDay[i] > mid
```

the current consecutive group is broken.

So I calculate how many bouquets can be made from that group:

```text
cnt / k
```

Then reset `cnt` to `0`.

If I can make at least `m` bouquets, the current day works, so I try an earlier day.

If I cannot make enough bouquets, I need more days.

---

## 🧠 Thought Process

### Step 1 : Check if Making the Bouquets is Even Possible

Each bouquet needs `k` flowers.

So `m` bouquets need:

```text
m × k
```

flowers.

I calculate:

```java
long required = (long) m * k;
```

I use `long` because `m * k` can be large.

If:

```java
if (required > bloomDay.length)
```

there are not enough flowers to make the required bouquets.

So I immediately return:

```java
return -1;
```

---

### Step 2 : Create the Search Space

The minimum possible day is the smallest value in `bloomDay`.

```java
int low = Arrays.stream(bloomDay).min().getAsInt();
```

The maximum possible day is the largest bloom day.

```java
int high = Arrays.stream(bloomDay).max().getAsInt();
```

So the answer must be somewhere between:

```text
low → high
```

---

### Step 3 : Try a Middle Day

```java
int mid = (low + high) / 2;
```

Now `mid` represents:

> "Suppose today is day `mid`. Can I make `m` bouquets?"

I check this using:

```java
dayCalc(bloomDay, m, k, mid)
```

---

### Step 4 : Count Consecutive Bloomed Flowers

Inside `dayCalc()`:

```java
int cnt = 0;
int cantBloom = 0;
```

Here:

```text
cnt       → consecutive flowers that have bloomed
cantBloom → number of bouquets we can make
```

For every flower:

```java
if (bloomDay[i] <= mid)
```

the flower has bloomed by day `mid`.

So:

```java
cnt++;
```

---

### Step 5 : Handle a Flower That Has Not Bloomed

If:

```java
bloomDay[i] > mid
```

the flower is not available yet.

That means the current consecutive group is broken.

So I calculate:

```java
cantBloom += (cnt / k);
```

For example, if:

```text
k = 3
cnt = 7
```

then:

```text
7 / 3 = 2 bouquets
```

The remaining one flower cannot be used.

Then I reset:

```java
cnt = 0;
```

because the next flower starts a new consecutive group.

---

### Step 6 : Don't Forget the Last Group

After the loop finishes, there may still be a group of bloomed flowers.

So I calculate:

```java
cantBloom += (cnt / k);
```

This handles the final group.

---

### Step 7 : Check if Enough Bouquets Can Be Made

Finally:

```java
return cantBloom >= m;
```

If:

```text
cantBloom >= m
```

then day `mid` is enough.

So I store it:

```java
result = mid;
```

and try an earlier day:

```java
high = mid - 1;
```

If:

```text
cantBloom < m
```

then `mid` is too early.

So I need more days:

```java
low = mid + 1;
```

---

## 🔍 Dry Run

Input:

```text
bloomDay = [1,10,3,10,2]
m = 3
k = 1
```

We need:

```text
3 bouquets
1 flower per bouquet
```

Required flowers:

```text
3 × 1 = 3
```

So it is possible.

Search space:

```text
low = 1
high = 10
```

### Try Day 5

```text
mid = 5
```

Flowers that have bloomed:

```text
[1,10,3,10,2]
 ↓    ↓     ↓
 ✔    ✔     ✔
```

Since `k = 1`, each bloomed flower can make one bouquet.

So:

```text
1 → bouquet
3 → bouquet
2 → bouquet
```

Total:

```text
3 bouquets
```

Therefore day `5` works.

Try an earlier day:

```text
high = 4
```

---

### Try Day 2

```text
mid = 2
```

Available flowers:

```text
[1,10,3,10,2]
 ✔  ✖  ✖  ✖  ✔
```

We can make:

```text
2 bouquets
```

But we need:

```text
3 bouquets
```

So day `2` is not enough.

Increase the number of days:

```text
low = 3
```

---

### Try Day 3

```text
mid = 3
```

Available:

```text
[1,10,3,10,2]
 ✔  ✖  ✔  ✖  ✔
```

We can make:

```text
3 bouquets
```

So day `3` works.

Try earlier:

```text
high = 2
```

Now:

```text
low = 3
high = 2
```

Search ends.

Final answer:

```text
3
```

---

## 🧪 Example With Adjacent Flowers

Consider:

```text
bloomDay = [1,2,4,9,3,4,1]
m = 2
k = 2
```

We need:

```text
2 × 2 = 4 flowers
```

But the flowers must be adjacent.

Suppose:

```text
mid = 4
```

Available flowers:

```text
[1,2,4,9,3,4,1]
 ✔ ✔ ✔ ✖ ✔ ✔ ✔
```

The consecutive groups are:

```text
[1,2,4]     → 3 flowers
[9]         → broken
[3,4,1]     → 3 flowers
```

For `k = 2`:

```text
3 / 2 = 1 bouquet
3 / 2 = 1 bouquet
```

Total:

```text
2 bouquets
```

So day `4` is sufficient.

The important thing is that I **cannot combine flowers from different groups** because the flowers in one bouquet must be adjacent.

---

## 💻 Java Solution

```java
class Solution {
    public int minDays(int[] bloomDay, int m, int k) {
        long required = (long) m * k;
        if (required > bloomDay.length) {
            return -1;
        }

        int result = -1;
        int low = Arrays.stream(bloomDay).min().getAsInt();
        int high = Arrays.stream(bloomDay).max().getAsInt();
        while (low <= high) {
            int mid = (low + high) / 2;
            if (dayCalc(bloomDay,m,k,mid)) {
                result = mid; // possible to form bouquets, try earlier
                high = mid - 1;
            } else {
                low = mid + 1; // need more days
            }
        }

        return result;
    }

    public boolean dayCalc(int[] bloomDay, int m, int k, int mid) {
        int cnt = 0;
        int cantBloom = 0;
        for (int i = 0; i < bloomDay.length; i++) {
            if (bloomDay[i] <= mid) {
                cnt++;
            } else {
               
                cantBloom += (cnt / k);
                cnt = 0;
            }
        }
        cantBloom += (cnt / k);
        return cantBloom >= m;
    }
}
```

---

## ⭐ Main Logic

```java
if (bloomDay[i] <= mid) {
    cnt++;
} else {
    cantBloom += (cnt / k);
    cnt = 0;
}
```

and:

```java
cantBloom += (cnt / k);
return cantBloom >= m;
```

### Why is this the Main Logic?

For a particular day, I only care whether a flower has bloomed:

```text
bloomDay[i] <= mid → available
bloomDay[i] > mid  → unavailable
```

I count consecutive available flowers.

If I have:

```text
cnt = 7
k = 3
```

then:

```text
7 / 3 = 2 bouquets
```

The remaining flower cannot be used.

When an unavailable flower appears, the consecutive group ends, so I calculate the bouquets from that group and start counting again.

Then Binary Search decides whether the current day is enough.

> 💡 **Interview Takeaway:**
> The key is to separate the problem into two parts: **Binary Search finds the minimum day**, while `dayCalc()` checks whether that day can produce enough adjacent bouquets.

---

## 🎯 Key Pattern

```text
Possible Days
      ↓
Minimum Bloom Day → Maximum Bloom Day
      ↓
   Binary Search
      ↓
    mid = day
      ↓
Check which flowers bloomed
      ↓
Count consecutive flowers
      ↓
cnt / k = bouquets
      ↓
Can we make m bouquets?
      ↓
   YES       NO
    ↓         ↓
Search      Search
LEFT        RIGHT
```

The important condition is:

```text
bloomDay[i] <= mid
```

which means:

```text
Flower has bloomed by day mid
```

And:

```text
cnt / k
```

tells how many bouquets can be made from one consecutive group.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n log(maxDay - minDay))
```

For every Binary Search step, I traverse all `n` flowers to check whether enough bouquets can be made.

The search range is between the minimum and maximum bloom day.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Constraints

* `1 <= bloomDay.length <= 10⁵`
* `1 <= bloomDay[i] <= 10⁹`
* `1 <= m <= 10⁶`
* `1 <= k <= 10⁶`

---

## 📌 Key Takeaways

* This is **Binary Search on Answer**.
* The answer is the minimum day on which `m` bouquets can be made.
* Search between the minimum and maximum bloom days.
* `bloomDay[i] <= mid` means the flower is available.
* Count only **consecutive** bloomed flowers because each bouquet needs adjacent flowers.
* `cnt / k` gives the number of bouquets from a consecutive group.
* If enough bouquets can be made, search for an earlier day.
* If not enough can be made, increase the number of days.
* Time complexity is `O(n log(maxDay - minDay))` with `O(1)` extra space.
