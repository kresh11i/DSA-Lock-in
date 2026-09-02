**File name:** `LC - 1011 Capacity To Ship Packages Within D Days.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 1011 - Capacity To Ship Packages Within D Days

## 🔗 Problem

Given an array `weights`, where each value represents the weight of a package, find the **minimum ship capacity** that allows all packages to be shipped within `days` days.

The packages must be shipped **in the given order**, so I cannot rearrange them.

Each day, I keep adding packages until adding the next package would exceed the ship's capacity. Then I start a new day.

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
* Greedy
* Capacity Calculation

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

This is another **Binary Search on Answer** problem.

I am not searching for an element in the array. Instead, I am searching for the **minimum ship capacity**.

The smallest possible capacity is the weight of the heaviest package:

```java
int low = Arrays.stream(weights).max().getAsInt();
```

The ship must at least be able to carry that package.

The largest possible capacity is the sum of all package weights:

```java
int high = Arrays.stream(weights).sum();
```

If the capacity is equal to the total weight, everything can be shipped in one day.

So my answer lies between:

```text
maximum single package weight → total weight
```

For every possible capacity `mid`, I calculate how many days are required.

If the required days are:

```text
result <= days
```

then the capacity is enough, so I try a smaller capacity.

If:

```text
result > days
```

then the capacity is too small, so I increase it.

---

## 🧠 Thought Process

### Step 1 : Find the Search Space

The minimum capacity cannot be smaller than the heaviest package.

For example:

```text
weights = [1,2,3,4,5]
```

The ship must be able to carry:

```text
5
```

So:

```java
int low = Arrays.stream(weights).max().getAsInt();
```

The maximum capacity can be the sum of all packages:

```text
1 + 2 + 3 + 4 + 5 = 15
```

So:

```java
int high = Arrays.stream(weights).sum();
```

Therefore:

```text
low = maximum package weight
high = total weight
```

---

### Step 2 : Try a Middle Capacity

```java
int mid = (low + high) / 2;
```

Now I treat `mid` as the ship's capacity.

The next question is:

> With this capacity, how many days will I need to ship all packages?

I calculate this using:

```java
int result = daysN(weights, days, mid);
```

---

### Step 3 : Calculate Number of Days

Inside `daysN()`:

```java
int dayss = 1, load = 0;
```

I start with:

```text
1 day
0 current load
```

Then I go through the packages in their original order.

If the next package can fit:

```java
if(load + weights[i] <= mid)
```

I add it to the current day's load:

```java
load += weights[i];
```

If adding it would exceed the capacity:

```java
if(load + weights[i] > mid)
```

I start a new day:

```java
dayss += 1;
load = weights[i];
```

The current package becomes the first package of the new day.

---

### Step 4 : Decide Which Side to Search

After calculating the required days:

```java
if(result <= days)
```

the current capacity is sufficient.

For example:

```text
capacity = 10
required days = 4
allowed days = 5
```

Since:

```text
4 <= 5
```

capacity `10` works.

But I want the **minimum capacity**, so I search left:

```text
high = mid - 1
```

If:

```text
result > days
```

the capacity is too small.

So I search right:

```text
low = mid + 1
```

---

## 🔍 Dry Run

Input:

```text
weights = [1,2,3,4,5,6,7,8,9,10]
days = 5
```

Search space:

```text
low = 10
high = 55
```

### Try Capacity 32

```text
mid = 32
```

Packages can be grouped as:

```text
Day 1 → 1 + 2 + 3 + 4 + 5 + 6 + 7 = 28
Day 2 → 8 + 9 + 10 = 27
```

Only:

```text
2 days
```

are required.

Since:

```text
2 <= 5
```

capacity `32` works.

So I try a smaller capacity:

```text
high = 31
```

---

### Try Capacity 20

Possible grouping:

```text
Day 1 → 1 + 2 + 3 + 4 + 5 = 15
Day 2 → 6 + 7 = 13
Day 3 → 8 + 9 = 17
Day 4 → 10
```

Required:

```text
4 days
```

Since:

```text
4 <= 5
```

capacity `20` works.

So I search smaller again.

---

### Try Capacity 15

Grouping:

```text
Day 1 → 1 + 2 + 3 + 4 + 5 = 15
Day 2 → 6 + 7 = 13
Day 3 → 8
Day 4 → 9
Day 5 → 10
```

Required:

```text
5 days
```

Since:

```text
5 <= 5
```

capacity `15` works.

Try smaller.

Eventually Binary Search determines that:

```text
capacity = 15
```

is the minimum valid capacity.

---

## 🧪 Important Example

Consider:

```text
weights = [3,2,2,4,1,4]
days = 3
```

Suppose:

```text
capacity = 6
```

We process packages in order:

```text
Day 1:
3 + 2 = 5
next 2 → would become 7 ❌
```

So start a new day:

```text
Day 2:
2 + 4 = 6
next 1 → would become 7 ❌
```

Start another day:

```text
Day 3:
1 + 4 = 5
```

So:

```text
6 capacity → 3 days
```

This is valid.

The important thing is that packages **cannot be rearranged**.

---

## 💻 Java Solution

```java
class Solution {
    public int shipWithinDays(int[] weights, int days) {
        int low = Arrays.stream(weights).max().getAsInt();
        int high = Arrays.stream(weights).sum();
        int ans = -1;

        while(low<=high){
            int mid = (low+high)/2;
            int result = daysN(weights,days , mid);

            if(result<=days){
                high = mid-1;

            }else{
                low = mid+1;
            }
        }

        return low;

    }

    public int daysN(int[] weights , int days ,int mid){
        int dayss = 1 , load = 0;

        for(int i = 0 ; i<weights.length;i++){
             if(load + weights[i]>mid){
                dayss += 1;
                load = weights[i];
             }else{
                load += weights[i];
             }
        }

        return dayss;
    }
}
```

---

## ⭐ Main Logic

```java
int mid = (low + high) / 2;
int result = daysN(weights, days, mid);

if(result <= days){
    high = mid - 1;
}else{
    low = mid + 1;
}
```

### Why is this the Main Logic?

The capacity and required number of days have an inverse relationship.

```text
Capacity ↑
    ↓
More packages fit each day
    ↓
Days required ↓
```

So:

```text
Small capacity → More days → Invalid
Large capacity → Fewer days → Valid
```

The pattern looks like:

```text
Invalid Invalid Invalid Invalid Valid Valid Valid
                                  ↑
                           Minimum Valid Capacity
```

Binary Search finds that first valid capacity.

The `daysN()` method greedily fills each day as much as possible without exceeding the capacity.

> 💡 **Interview Takeaway:**
> When the answer is a numerical capacity and you can check how many days a particular capacity requires, think **Binary Search on Answer**.

---

## 🎯 Key Pattern

```text
Search Space
    ↓
max(weights) → sum(weights)
    ↓
Binary Search
    ↓
capacity = mid
    ↓
Calculate required days
    ↓
required days <= given days?
       /             \
     YES              NO
      ↓                ↓
Search LEFT        Search RIGHT
      ↓                ↓
high = mid - 1     low = mid + 1
```

The important calculation is:

```text
If load + weights[i] > capacity
        ↓
Start new day
```

Otherwise:

```text
load += weights[i]
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n log(sum(weights)))
```

For every Binary Search iteration, I traverse all `n` packages to calculate the number of days.

The search range is from the maximum package weight to the total weight.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Constraints

* `1 <= days <= weights.length <= 5 * 10⁴`
* `1 <= weights[i] <= 500`
* Packages must be shipped in the given order.

---

## 📌 Key Takeaways

* This is **Binary Search on Answer**.
* The minimum capacity is `max(weights)`.
* The maximum capacity is `sum(weights)`.
* For every capacity, greedily load packages until the next package does not fit.
* When a package does not fit, start a new day.
* If required days are within the limit, try a smaller capacity.
* If required days exceed the limit, increase the capacity.
* Return `low` because it represents the smallest valid capacity.
* Time complexity is `O(n log(sum(weights)))` and space complexity is `O(1)`.
