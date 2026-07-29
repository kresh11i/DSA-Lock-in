# Best Time to Buy and Sell Stock

## 🔗 Problem Link

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

## 🏷️ Tags

- Array
- Dynamic Programming

## 📚 Topics

- Array
- Dynamic Programming

## 📊 Difficulty

Easy

## 📖 Problem Statement

You are given an array `prices` where `prices[i]` is the price of a stock on the `iᵗʰ` day.

Choose **one day** to buy the stock and **a later day** to sell it.

Return the **maximum profit** you can make.

If no profit is possible, return `0`.

---

## ✨ Examples

### Example 1

```text
Input: prices = [7,1,5,3,6,4]

Output: 5
```

### Example 2

```text
Input: prices = [7,6,4,3,1]

Output: 0
```

---

## 🚀 Approach

### Pattern Used

**Running Minimum (Greedy)**

### Intuition

To get the maximum profit, we should always buy at the **lowest price** seen so far.

As we traverse the array:

- Keep track of the minimum price.
- Calculate the profit if we sell on the current day.
- Update the maximum profit whenever we find a better one.

This way, we never need to check every possible buy and sell pair.

---

### Why This Approach Works

For every day,

- The minimum price stores the best buying opportunity until that day.
- The current price acts as the selling price.
- Their difference gives the profit for selling today.

By checking every day once, we automatically find the maximum possible profit.

---

### Algorithm

1. Store the first price as the minimum price.
2. Traverse the array from the second element.
3. Calculate the current profit.
4. Update the maximum profit.
5. Update the minimum price if a smaller value is found.
6. Return the maximum profit.

---

## 💻 Java Solution

```java
class Solution {
    public int maxProfit(int[] prices) {

        int minimum = prices[0], profit = 0;

        for(int i = 1; i < prices.length; i++){

            int cost = prices[i] - minimum;

            profit = Math.max(profit, cost);

            minimum = Math.min(minimum, prices[i]);
        }

        return profit;
    }
}
```

---

## ⭐ Main Logic

```java
int cost = prices[i] - minimum;

profit = Math.max(profit, cost);

minimum = Math.min(minimum, prices[i]);
```

### Why is this the Main Logic?

These three lines solve the entire problem.

- Calculate the profit if we sell today.
- Update the maximum profit found so far.
- Update the minimum buying price.

> **Interview Takeaway:**  
> Always keep track of the **minimum value seen so far** when you need the maximum difference.

---

## 🧪 Dry Run

### Input

```text
prices = [7,1,5,3,6,4]
```

| Day | Price | Minimum Price | Current Profit | Maximum Profit |
|----:|------:|--------------:|---------------:|---------------:|
|0|7|7|0|0|
|1|1|1|0|0|
|2|5|1|4|4|
|3|3|1|2|4|
|4|6|1|5|5|
|5|4|1|3|5|

### Final Output

```text
5
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- The array is traversed only once.

### Space Complexity

**O(1)**

- Only a few integer variables are used.

---

## 📌 Constraints

- `1 <= prices.length <= 10⁵`
- `0 <= prices[i] <= 10⁴`

---

## 💡 Key Points

- Traverse the array only once.
- Always store the minimum price seen so far.
- Calculate profit for every day.
- Update the answer whenever a larger profit is found.
- Greedy approach with constant space.
- Return `0` if no profit is possible.

---

## ⚠️ Common Mistakes

- Updating the minimum price before calculating the current profit.
- Buying and selling on the same day incorrectly.
- Returning a negative profit instead of `0`.
- Using nested loops, resulting in **O(n²)** time.

---

## 📝 Revision Snapshot

**Problem Type:** Maximum Profit

**Pattern Used:** Running Minimum (Greedy)

**Main Data Structure:** Array

**Main Logic:**

```text
Profit = Current Price - Minimum Price So Far

Maximum Profit = max(Maximum Profit, Profit)

Minimum Price = min(Minimum Price, Current Price)
```

**Key Idea:**

Keep track of the **lowest buying price** while traversing the array. At every step, calculate the profit if you sell today and keep the maximum profit found.