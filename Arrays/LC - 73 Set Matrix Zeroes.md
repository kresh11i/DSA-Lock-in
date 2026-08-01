# Set Matrix Zeroes

## 🔗 Problem Link

https://leetcode.com/problems/set-matrix-zeroes/

## 🏷️ Tags

- Array
- Matrix

## 📚 Topics

- Array
- Hash Table
- Matrix

## 📊 Difficulty

Medium

## 📖 Problem Statement

Given an `m × n` integer matrix, if an element is `0`, set its **entire row** and **entire column** to `0`.

The modification must be done **in-place**.

---

## ✨ Examples

### Example 1

```text
Input:
[
 [1,1,1],
 [1,0,1],
 [1,1,1]
]

Output:
[
 [1,0,1],
 [0,0,0],
 [1,0,1]
]
```

### Example 2

```text
Input:
[
 [0,1,2,0],
 [3,4,5,2],
 [1,3,1,5]
]

Output:
[
 [0,0,0,0],
 [0,4,5,0],
 [0,3,1,0]
]
```

---

## 🚀 Approach

### Pattern Used

**Matrix Traversal + Row & Column Marking**

### Intuition

Whenever there is a `0` in the matrix, the **entire row and column containing that `0`** must be converted into `0`.

To solve this, create two extra arrays:

- `row[]`
- `col[]`

Initially, every element in both arrays is `0`.

If the matrix contains a `0`, mark its corresponding row and column as `1`.

After marking all the rows and columns, traverse the matrix again.

If either the corresponding row or column is marked as `1`, make that cell `0`.

This avoids modifying the matrix while we are still checking it.

---

### Why This Approach Works

If we immediately change a cell to `0`, that new zero may incorrectly affect other rows and columns.

Instead,

- First identify all rows and columns that need to become zero.
- Store this information in separate arrays.
- Finally update the original matrix.

This ensures only the original zeros determine the result.

---

### Algorithm

1. Create two arrays:
   - `row[]`
   - `col[]`
2. Traverse the matrix.
3. Whenever a `0` is found:
   - Mark `row[i] = 1`
   - Mark `col[j] = 1`
4. Traverse the matrix again.
5. If `row[i] == 1` **or** `col[j] == 1`, change `matrix[i][j]` to `0`.
6. Return the modified matrix.

---

## 💻 Java Solution

```java
class Solution {
    public void setZeroes(int[][] matrix) {

        int rows = matrix.length;
        int cols = matrix[0].length;

        int[] row = new int[rows];
        int[] col = new int[cols];

        for (int i = 0; i < rows; i++) {

            for (int j = 0; j < cols; j++) {

                if (matrix[i][j] == 0) {
                    row[i] = 1;
                    col[j] = 1;
                }
            }
        }

        for (int i = 0; i < rows; i++) {

            for (int j = 0; j < cols; j++) {

                if (row[i] == 1 || col[j] == 1) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

---

## ⭐ Main Logic

### Step 1 - Mark the Rows and Columns

```java
if(matrix[i][j] == 0){

    row[i] = 1;
    col[j] = 1;
}
```

This records which rows and columns need to become zero.

---

### Step 2 - Update the Matrix

```java
if(row[i] == 1 || col[j] == 1){

    matrix[i][j] = 0;
}
```

If either the row or column is marked, the current cell must become `0`.

> **Interview Takeaway:**  
> Whenever modifying the input during traversal can affect future decisions, first **mark** the required changes and then **apply** them in a second traversal.

---

## 🧪 Dry Run

### Input

```text
[
 [1,1,1],
 [1,0,1],
 [1,1,1]
]
```

### Step 1 - Mark Rows and Columns

```
row = [0,1,0]

col = [0,1,0]
```

---

### Step 2 - Update Matrix

| Cell | row[i] | col[j] | Result |
|------|--------|--------|--------|
|(0,0)|0|0|1|
|(0,1)|0|1|0|
|(0,2)|0|0|1|
|(1,0)|1|0|0|
|(1,1)|1|1|0|
|(1,2)|1|0|0|
|(2,0)|0|0|1|
|(2,1)|0|1|0|
|(2,2)|0|0|1|

### Final Output

```text
[
 [1,0,1],
 [0,0,0],
 [1,0,1]
]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(m × n)**

- First traversal to mark rows and columns.
- Second traversal to update the matrix.

Overall Time Complexity = **O(m × n)**.

### Space Complexity

**O(m + n)**

- `row[]` uses **O(m)** space.
- `col[]` uses **O(n)** space.

---

## 📌 Constraints

- `m == matrix.length`
- `n == matrix[0].length`
- `1 <= m, n <= 200`
- `-2³¹ <= matrix[i][j] <= 2³¹ - 1`

---

## 💡 Key Points

- Create separate arrays for rows and columns.
- First traversal is only for marking.
- Second traversal updates the matrix.
- Never modify the matrix while identifying zeros.
- Use `row[i] || col[j]` to decide whether a cell becomes zero.
- Simple and easy-to-understand approach.

---

## ⚠️ Common Mistakes

- Changing the matrix during the first traversal.
- Forgetting to mark both the row and the column.
- Using `&&` instead of `||` while updating the matrix.
- Creating arrays with incorrect sizes.
- Forgetting the second traversal.

---

## 📝 Revision Snapshot

**Problem Type:** Matrix Manipulation

**Pattern Used:** Matrix Traversal + Row & Column Marking

**Main Data Structure:** Matrix + Two Helper Arrays

**Main Flow**

```text
Traverse Matrix
      │
      ▼
Found Zero?
      │
      ▼
Mark Row & Column
      │
      ▼
Second Traversal
      │
      ▼
row[i] == 1 OR col[j] == 1
      │
      ▼
Make Cell = 0
```

**Key Idea**

```text
Never modify the matrix while searching.

↓

Mark affected rows and columns first.

↓

Update the matrix in a second traversal.
```