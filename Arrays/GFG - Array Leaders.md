# Array Leaders

## 🔗 Problem Link

https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1

## 🏷️ Tags

- Array

## 📚 Topics

- Array
- Traversal
- Greedy

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given an array of positive integers, find all the **leaders** in the array.

A leader is an element that is **greater than or equal to every element on its right**.

The rightmost element is always a leader.

Return the leaders in their original order.

---

## ✨ Examples

### Example 1

```text
Input: arr = [16,17,4,3,5,2]

Output: [17,5,2]
```

### Example 2

```text
Input: arr = [10,4,2,4,1]

Output: [10,4,4,1]
```

---

## 🚀 Approach

### Pattern Used

**Reverse Traversal + Running Maximum**

### Intuition

A leader is an element whose **current value is greater than or equal to every element after it**.

To check this efficiently, traverse the array **from right to left**.

Initialize a variable called `leader` to store the largest element seen so far.

- If the current element is greater than or equal to `leader`, it is a leader.
- Add it to the answer list.
- Update `leader` with the current element.

Since we are traversing from right to left, the answer is stored in reverse order.

If the platform asks for the leaders in their original order, simply reverse the answer list using two pointers.

---

### Why This Approach Works

While moving from right to left, `leader` always stores the **largest element seen so far**.

If the current element is greater than or equal to `leader`, then every element to its right is smaller than or equal to it.

Therefore, it is a leader.

Each element is processed only once, making the solution efficient.

---

### Algorithm

1. Initialize `leader = Integer.MIN_VALUE`.
2. Traverse the array from right to left.
3. If the current element is greater than or equal to `leader`:
   - Add it to the answer list.
   - Update `leader`.
4. Reverse the answer list using two pointers.
5. Return the answer.

---

## 💻 Java Solution

```java
class Solution {
    static ArrayList<Integer> leaders(int arr[]) {

        ArrayList<Integer> ans = new ArrayList<>();

        int leader = Integer.MIN_VALUE;

        for (int i = arr.length - 1; i >= 0; i--) {

            if (arr[i] >= leader) {
                ans.add(arr[i]);
                leader = arr[i];
            }
        }

        int l = 0;
        int r = ans.size() - 1;

        while (l < r) {

            int temp = ans.get(l);
            ans.set(l, ans.get(r));
            ans.set(r, temp);

            l++;
            r--;
        }

        return ans;
    }
}
```

---

## ⭐ Main Logic

```java
if (arr[i] >= leader) {

    ans.add(arr[i]);

    leader = arr[i];
}
```

### Why is this the Main Logic?

This block determines whether the current element is a leader.

- `leader` stores the largest element seen so far from the right.
- If the current element is greater than or equal to `leader`, it is a leader.
- Update `leader` so future elements can be compared against it.

> **Interview Takeaway:**  
> When a problem asks you to compare an element with everything on its right, think about **traversing from right to left** while maintaining a running maximum.

---

## 🧪 Dry Run

### Input

```text
arr = [16,17,4,3,5,2]
```

Initially

```text
leader = -∞

ans = []
```

| Index | Current Element | Leader | Action | Answer |
|------:|----------------:|-------:|--------|--------|
|5|2|-∞|Add & Update|[2]|
|4|5|2|Add & Update|[2,5]|
|3|3|5|Skip|[2,5]|
|2|4|5|Skip|[2,5]|
|1|17|5|Add & Update|[2,5,17]|
|0|16|17|Skip|[2,5,17]|

Reverse the answer list.

```text
Before Reverse

[2,5,17]

After Reverse

[17,5,2]
```

### Final Output

```text
[17,5,2]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- One traversal to find the leaders.
- One traversal to reverse the answer list.

Overall Time Complexity = **O(n)**.

### Space Complexity

**O(n)**

- An extra list is used to store the leaders.

---

## 📌 Constraints

- `1 <= arr.size() <= 10⁶`
- `0 <= arr[i] <= 10⁶`

---

## 💡 Key Points

- Traverse from right to left.
- `leader` stores the largest element seen so far.
- If `arr[i] >= leader`, it is a leader.
- Update `leader` after adding the current element.
- Reverse the answer list before returning.
- Every element is visited only once.

---

## ⚠️ Common Mistakes

- Traversing from left to right.
- Forgetting to update the `leader`.
- Using `>` instead of `>=`.
- Forgetting to reverse the answer list.
- Initializing `leader` with `0` instead of `Integer.MIN_VALUE`.

---

## 📝 Revision Snapshot

**Problem Type:** Array Traversal

**Pattern Used:** Reverse Traversal + Running Maximum

**Main Data Structure:** ArrayList

**Main Flow**

```text
Traverse from Right
        │
        ▼
Current >= Leader ?
      /       \
    Yes        No
    │          │
Add to      Ignore
Answer
    │
Update Leader
    │
Continue
    │
Reverse Answer
```

**Key Idea**

```text
Leader = Largest Element Seen So Far

Current >= Leader

↓

Current becomes a Leader

↓

Update Leader

↓

Reverse the Answer List
```