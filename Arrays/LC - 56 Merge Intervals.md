**File name:** `LC - 56 Merge Intervals.md`
**📁 Folder:** `Arrays` — your repository doesn't have a dedicated `Intervals` folder, and this is primarily an Array + Sorting problem.

# 🧩 LeetCode 56 - Merge Intervals

## 🔗 Problem

Given an array of intervals where each interval is represented as `[start, end]`, merge all overlapping intervals and return the non-overlapping intervals that cover the same ranges.

---

## 🏷️ Tags

* Array
* Sorting
* Intervals
* Greedy

---

## 📚 Topics

* Arrays
* Sorting
* Interval Merging

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

The main idea is to first **sort the intervals based on their starting value**.

Once sorted, overlapping intervals will come next to each other.

For every interval, I check whether:

```text
current start > previous end
```

If this is true, there is no overlap, so I add the current interval separately.

Otherwise, the intervals overlap, so I merge them by updating the end of the previous interval to the maximum of both ending values.

---

## 🧠 Thought Process

### Step 1 : Sort the Intervals

First, sort the intervals based on their starting values.

```java
Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
```

Example:

```text
Input:

[[1,3],[2,6],[8,10],[15,18]]

After sorting:

[[1,3],[2,6],[8,10],[15,18]]
```

Now overlapping intervals will be easier to identify.

---

### Step 2 : Create the Result List

Create a list called `ans` to store the merged intervals.

```java
List<int[]> ans = new ArrayList<>();
```

For every interval, check whether it can be added as a new interval or needs to be merged.

---

### Step 3 : Check for Overlap

The main condition is:

```java
if(ans.size() == 0 || intervals[i][0] > ans.get(ans.size() - 1)[1])
```

This means:

* If `ans` is empty, simply add the interval.
* If the current interval starts **after** the end of the previous interval, there is no overlap.

Example:

```text
Previous: [1,6]
Current : [8,10]

8 > 6 ✔
```

So `[8,10]` can be added separately.

---

### Step 4 : Merge Overlapping Intervals

If the current interval overlaps with the previous interval, update the end value.

```java
ans.get(ans.size() - 1)[1] =
    Math.max(ans.get(ans.size() - 1)[1], intervals[i][1]);
```

Example:

```text
Previous: [1,3]
Current : [2,6]
```

Since:

```text
2 <= 3
```

they overlap.

So:

```text
[1,3] + [2,6]
```

becomes:

```text
[1,6]
```

The `Math.max()` is important because the current interval might end before or after the previous interval.

---

## 🔍 Dry Run

Input:

```text
intervals = [[1,3],[2,6],[8,10],[15,18]]
```

### Step 1 : Start

```text
ans = []
```

### Step 2 : Process `[1,3]`

`ans` is empty, so add it.

```text
ans = [[1,3]]
```

### Step 3 : Process `[2,6]`

Check:

```text
2 <= 3
```

They overlap.

Merge them:

```text
[1,3] + [2,6]

=> [1,6]
```

Now:

```text
ans = [[1,6]]
```

### Step 4 : Process `[8,10]`

Check:

```text
8 > 6
```

No overlap.

Add it:

```text
ans = [[1,6],[8,10]]
```

### Step 5 : Process `[15,18]`

Check:

```text
15 > 10
```

No overlap.

Add it:

```text
ans = [[1,6],[8,10],[15,18]]
```

### Final Answer

```text
[[1,6],[8,10],[15,18]]
```

---

## 💻 Java Solution

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> ans = new ArrayList<>();

        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        for(int i = 0; i < intervals.length; i++){
            if(ans.size() == 0 || intervals[i][0] > ans.get(ans.size() - 1)[1]){
                ans.add(intervals[i]);
            }
            else{
                ans.get(ans.size() - 1)[1] =
                    Math.max(ans.get(ans.size() - 1)[1], intervals[i][1]);
            }
        }

        return ans.toArray(new int[0][]);
    }
}
```

---

## ⭐ Main Logic

```java
if(ans.size() == 0 || intervals[i][0] > ans.get(ans.size() - 1)[1]){
    ans.add(intervals[i]);
}
else{
    ans.get(ans.size() - 1)[1] =
        Math.max(ans.get(ans.size() - 1)[1], intervals[i][1]);
}
```

### Why is this the Main Logic?

* If there is no previous interval, add the current interval.
* If the current interval starts after the previous interval ends, there is no overlap.
* Otherwise, the intervals overlap and should be merged.
* `Math.max()` keeps the farthest ending point after merging.

> 💡 **Interview Takeaway:**
> For interval problems, sorting by the starting point often makes overlapping ranges easy to process from left to right.

---

## 🎯 Key Pattern

```text
Sort → Compare Start with Previous End → Merge or Add
```

The important condition is:

```text
current start > previous end
```

No overlap:

```text
[1,3]    [5,7]
     3 < 5
```

Overlap:

```text
[1,5]
   [3,7]
```

Merge:

```text
[1,7]
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n log n)
```

* Sorting the intervals takes `O(n log n)`.
* Traversing all intervals takes `O(n)`.
* Overall complexity is `O(n log n)`.

### Space Complexity

```text
O(n)
```

The `ans` list can store up to `n` non-overlapping intervals.

---

## 📌 Constraints

* `1 <= intervals.length <= 10⁴`
* `intervals[i].length == 2`
* `0 <= start <= end <= 10⁴`

---

## 📌 Key Takeaways

* Sort intervals by their starting value first.
* Compare the current start with the previous merged interval's end.
* If there is no overlap, add the interval.
* If there is overlap, update the end using `Math.max()`.
* The main pattern is **Sort + Merge Intervals**.
* Sorting makes the intervals easy to process from left to right.
