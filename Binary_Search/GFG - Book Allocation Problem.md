**File Name:** `GFG - Book Allocation Problem.md`

# 📚 Book Allocation Problem

## 🔗 Problem

**GeeksforGeeks: Allocate minimum number of pages**

---

## 🏷️ Tags

* Array
* Binary Search
* Binary Search on Answer
* Greedy

---

## 📚 Topics

* Binary Search on Answer
* Minimum Maximum Problem
* Greedy Allocation
* Feasibility Check

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

We have an array where each element represents the number of pages in a book.

We need to distribute the books among `m` students such that:

* Every student gets **at least one book**.
* Books must be allocated **contiguously**.
* Every book must be given to exactly one student.
* We want to **minimize the maximum number of pages** assigned to any student.

For example:

```text
arr = [10, 20, 30, 40]
m = 2
```

One possible allocation:

```text
Student 1 → 10 + 20 = 30
Student 2 → 30 + 40 = 70

Maximum = 70
```

Another allocation:

```text
Student 1 → 10 + 20 + 30 = 60
Student 2 → 40 = 40

Maximum = 60
```

So we want the allocation where this maximum value is as small as possible.

This is a classic **Binary Search on Answer** problem.

---

## 🧠 Thought Process

The answer must lie between two values.

### Minimum possible answer

The student receiving the book with the maximum pages must handle at least that many pages.

So:

```text
low = maximum element
```

### Maximum possible answer

One student could potentially receive all the books.

So:

```text
high = sum of all pages
```

Therefore, our search space is:

```text
max(arr) → sum(arr)
```

Now we ask:

> If I allow each student to have at most `mid` pages, can I successfully allocate all books using `m` students?

This is our **feasibility check**.

---

## 🔍 Feasibility Check

For a given maximum page limit `mid`, we greedily assign books to the current student as long as:

```text
current pages + book pages <= mid
```

If adding the next book exceeds `mid`, we start a new student.

Example:

```text
arr = [10, 20, 30, 40]
mid = 60
```

Allocation:

```text
Student 1:
10 + 20 + 30 = 60

Student 2:
40
```

Students required:

```text
2
```

If:

```text
students required <= m
```

then `mid` is a **possible answer**.

---

## 🧠 Why Binary Search Works

There is a monotonic pattern.

Suppose a maximum limit of `50` requires `3` students.

If we increase the limit to `60`, maybe only `2` students are required.

If we increase it further to `70`, it will still be possible.

So:

```text
Small capacity → Not possible
        ↓
        ↓
First possible answer
        ↓
Larger capacity → Possible
```

Once a particular maximum page limit becomes possible, every larger limit will also be possible.

That makes Binary Search applicable.

---

## 🔍 Dry Run

### Example

```text
arr = [10, 20, 30, 40]
m = 2
```

Search range:

```text
low = max(arr) = 40
high = sum(arr) = 100
```

### Try `mid = 70`

Allocation:

```text
Student 1 → 10 + 20 + 30 = 60
Student 2 → 40
```

Students required:

```text
2
```

Since:

```text
2 <= m
```

`70` is possible.

So we try a smaller answer:

```text
high = mid - 1
```

---

### Try `mid = 54`

Allocation:

```text
Student 1 → 10 + 20 = 30
Student 2 → 30
Student 3 → 40
```

Students required:

```text
3
```

Since:

```text
3 > 2
```

`54` is not possible.

So we need a larger limit:

```text
low = mid + 1
```

---

### Eventually

Binary Search finds:

```text
60
```

Allocation:

```text
Student 1 → 10 + 20 + 30 = 60
Student 2 → 40
```

Therefore:

```text
Answer = 60
```

---

## ⭐ Main Logic

There are **two important functions** in this solution.

### 1. `findPages()`

Performs Binary Search on the answer.

```text
low = maximum book pages
high = total pages
```

For every `mid`:

```text
result = number of students required
```

Then:

```text
if result > m
    → capacity is too small
    → move right

else
    → capacity works
    → try smaller capacity
    → move left
```

---

### 2. `student()`

Checks how many students are required if each student can receive at most `mid` pages.

It greedily keeps adding books to the current student.

When the limit is exceeded:

```java
student++;
pages = arr[i];
```

A new student starts with the current book.

---

## 🎯 Key Pattern

### Binary Search on Answer

Whenever the problem asks something like:

> **Minimize the maximum**

and we can check whether a particular answer is possible, think:

```text
Binary Search on Answer
```

For Book Allocation:

```text
Answer = maximum pages given to any student
```

Search:

```text
max(arr) → sum(arr)
```

Feasibility:

```text
Can we allocate the books using <= m students
with maximum capacity = mid?
```

---

## 💻 Java Solution

```java
import java.util.*;

class Solution {

    // Write your solution here
    public int findPages(int[] arr, int m) {
        int low = Arrays.stream(arr).max().getAsInt();
        int high = Arrays.stream(arr).sum();

        if(m > arr.length){
            return -1;
        }

        while(low <= high){
            int mid = (low + high) / 2;

            int result = student(arr, m, mid);

            if(result > m){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }

        return low;
    }

    public int student(int[] arr, int m, int mid){
        int student = 1;
        int pages = 0;

        for(int i = 0; i < arr.length; i++){
            if(pages + arr[i] <= mid){
                pages += arr[i];
            }else{
                student++;
                pages = arr[i];
            }
        }

        return student;
    }
}
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n × log(sum(arr)))
```

For every Binary Search step, we scan the entire array to count the required students.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Important Observations

### Why `low = max(arr)`?

A book cannot be split between students.

Therefore, if the largest book has `40` pages, the answer can never be less than `40`.

```text
low = max(arr)
```

### Why `high = sum(arr)`?

In the worst case, one student could receive all the books.

```text
high = sum(arr)
```

### Why greedy allocation?

For a fixed `mid`, we want to use the current student's capacity as much as possible before moving to the next student.

This tells us the **minimum number of students required** for that `mid`.

---

## 📌 Key Takeaways

* Book Allocation is a classic **Binary Search on Answer** problem.
* The answer represents the **minimum possible maximum pages**.
* Search range:

```text
max(arr) → sum(arr)
```

* For each `mid`, greedily calculate how many students are needed.
* If students needed `> m`:

  * `mid` is too small.
  * Move right.
* If students needed `<= m`:

  * `mid` is possible.
  * Try a smaller value.
* At the end, `low` gives the minimum feasible maximum.

### 🧠 Pattern to Remember

```text
Minimize the maximum
        ↓
Binary Search on Answer
        ↓
Can this answer work?
        ↓
Greedy feasibility check
```
