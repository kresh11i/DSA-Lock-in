**File name:** `LC - 1283 Find the Smallest Divisor Given a Threshold.md`
**📁 Folder:** `Binary_Search`

# 🧩 LeetCode 1283 - Find the Smallest Divisor Given a Threshold

## 🔗 Problem

Given an integer array `nums` and an integer `threshold`, find the **smallest positive divisor** such that the sum of the rounded-up division results is less than or equal to `threshold`.

For every number:

```text
ceil(nums[i] / divisor)
```

is added to the total.

Return the smallest divisor that satisfies the condition.

---

## 🏷️ Tags

* Array
* Binary Search
* Binary Search on Answer
* Math

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

This is another **Binary Search on Answer** problem.

I am not searching for an element in the array. Instead, I am searching for the **smallest divisor**.

The possible divisor starts from:

```text
1
```

and the maximum useful divisor is the maximum value in the array.

```java
int low = 1;
int high = Arrays.stream(nums).max().getAsInt();
```

For every divisor `mid`, I calculate the sum:

```text
ceil(nums[0] / mid)
+ ceil(nums[1] / mid)
+ ...
```

Then I compare that sum with `threshold`.

If:

```text
sum <= threshold
```

the divisor is valid.

Since I need the **smallest** valid divisor, I try a smaller divisor:

```java
high = mid - 1;
```

If:

```text
sum > threshold
```

the divisor is too small, so the sum is too large.

Therefore, I need a bigger divisor:

```java
low = mid + 1;
```

So the pattern becomes:

```text
Small divisor → Large sum → Invalid

Large divisor → Small sum → Valid
```

I use Binary Search to find the **first valid divisor**.

---

## 🧠 Thought Process

### Step 1 : Check if the Answer is Possible

I first check:

```java
if(nums.length > threshold){
    return 1;
}
```

Every positive number contributes at least `1` to the sum, even when the divisor is very large.

Therefore, if:

```text
nums.length > threshold
```

then even the largest possible divisor cannot make the sum small enough.

So there is no valid divisor.

---

### Step 2 : Create the Search Space

The smallest possible divisor is:

```text
1
```

So:

```java
int low = 1;
```

The largest useful divisor is the largest number in the array:

```java
int high = Arrays.stream(nums).max().getAsInt();
```

Why don't I need to go beyond the maximum element?

If the divisor is greater than or equal to the maximum element, every number contributes:

```text
ceil(nums[i] / divisor) = 1
```

So increasing the divisor further cannot improve the result.

---

### Step 3 : Try a Middle Divisor

```java
int mid = (low + high) / 2;
```

`mid` represents a possible divisor.

Now I calculate the total sum using:

```java
int result = divide(nums, threshold, mid);
```

The helper method calculates the total contribution from every number.

---

### Step 4 : Calculate the Division Sum

For every number:

```java
double value = (double) nums[i] / mid;
sum += (int)Math.ceil(value);
```

For example:

```text
nums[i] = 7
mid = 3

7 / 3 = 2.33

ceil(2.33) = 3
```

So this number contributes `3` to the total.

Another example:

```text
nums[i] = 6
mid = 3

6 / 3 = 2

ceil(2) = 2
```

So it contributes `2`.

---

### Step 5 : If the Divisor Works

If:

```java
if(result <= threshold)
```

then the current divisor is valid.

But I want the **smallest** valid divisor.

So I store it:

```java
ans = mid;
```

and search on the left:

```java
high = mid - 1;
```

The thinking is:

```text
mid works ✔
        ↓
Maybe a smaller divisor also works
        ↓
Search LEFT
```

---

### Step 6 : If the Divisor Does Not Work

If:

```text
result > threshold
```

then the current divisor is too small.

A smaller divisor would make every division result the same or larger, increasing the sum even more.

So I need a larger divisor:

```java
low = mid + 1;
```

The thinking is:

```text
mid doesn't work ❌
        ↓
Need a larger divisor
        ↓
Search RIGHT
```

---

## 🔍 Dry Run

Input:

```text
nums = [1,2,5,9]
threshold = 6
```

Search space:

```text
low = 1
high = 9
```

### Iteration 1

```text
mid = 5
```

Calculate:

```text
1 / 5 → 1
2 / 5 → 1
5 / 5 → 1
9 / 5 → 2
```

Total:

```text
1 + 1 + 1 + 2 = 5
```

Since:

```text
5 <= 6
```

divisor `5` works.

So:

```text
ans = 5
high = 4
```

---

### Iteration 2

```text
low = 1
high = 4

mid = 2
```

Calculate:

```text
1 / 2 → 1
2 / 2 → 1
5 / 2 → 3
9 / 2 → 5
```

Total:

```text
1 + 1 + 3 + 5 = 10
```

Since:

```text
10 > 6
```

divisor `2` is too small.

So:

```text
low = 3
```

---

### Iteration 3

```text
low = 3
high = 4

mid = 3
```

Calculate:

```text
1 / 3 → 1
2 / 3 → 1
5 / 3 → 2
9 / 3 → 3
```

Total:

```text
1 + 1 + 2 + 3 = 7
```

Since:

```text
7 > 6
```

divisor `3` is too small.

So:

```text
low = 4
```

---

### Iteration 4

```text
low = 4
high = 4

mid = 4
```

Calculate:

```text
1 / 4 → 1
2 / 4 → 1
5 / 4 → 2
9 / 4 → 3
```

Total:

```text
1 + 1 + 2 + 3 = 7
```

Still greater than `6`.

So:

```text
low = 5
```

Now:

```text
low > high
```

Search ends.

The smallest valid divisor was:

```text
5
```

---

## 💻 Java Solution

```java
class Solution {
    public int smallestDivisor(int[] nums, int threshold) {
        int low = 1;
        int high = Arrays.stream(nums).max().getAsInt();
        int ans = -1;

        if(nums.length> threshold){
            return 1;
        }

        while (low <= high) {
            int mid = (low + high) / 2;
            int result = divide(nums, threshold,mid);

            if(result <= threshold){
                ans = mid;
                high = mid-1;
                
            }else{
                low = mid+1;
            }
    
        }

        return ans;
    }

    public int divide(int[] nums , int threshold ,int mid){
        int sum = 0;

        for(int i = 0 ; i<nums.length;i++){
            sum = sum + (int)Math.ceil((double) nums[i] / mid);
            
        }

        return sum;
    }
}
```

---

## ⭐ Main Logic

```java
int mid = (low + high) / 2;
int result = divide(nums, threshold, mid);

if(result <= threshold){
    ans = mid;
    high = mid - 1;
}else{
    low = mid + 1;
}
```

### Why is this the Main Logic?

The divisor and the total sum have an inverse relationship.

```text
Divisor ↑
   ↓
Division result ↓
   ↓
Total sum ↓
```

So:

```text
Small divisor
    ↓
Large sum
    ↓
May exceed threshold
```

while:

```text
Large divisor
    ↓
Small sum
    ↓
Eventually becomes valid
```

The valid answers look like:

```text
Invalid Invalid Invalid Valid Valid Valid
                          ↑
                    Smallest Valid
```

Binary Search finds this first valid divisor.

> 💡 **Interview Takeaway:**
> Whenever increasing a number makes a condition easier to satisfy, and you need the smallest number that satisfies it, think about **Binary Search on Answer**.

---

## 🎯 Key Pattern

```text
Possible Divisors

1 ---------------- max(nums)
          ↓
       Binary Search
          ↓
       divisor = mid
          ↓
 Calculate division sum
          ↓
   sum <= threshold?
       /          \
     YES           NO
      ↓             ↓
Search LEFT      Search RIGHT
      ↓             ↓
high = mid-1     low = mid+1
```

The important condition is:

```text
sum <= threshold
```

which tells me that the current divisor is valid.

---

## 🧪 Another Example

```text
nums = [44,22,33,11,1]
threshold = 5
```

Since there are `5` numbers, the minimum possible sum is `5`.

So the divisor must be large enough to make every number contribute exactly `1`.

For example, with:

```text
divisor = 44
```

we get:

```text
44 / 44 → 1
22 / 44 → 1
33 / 44 → 1
11 / 44 → 1
1  / 44 → 1
```

Total:

```text
5
```

which satisfies the threshold.

Binary Search checks smaller divisors to find the **smallest** one that still keeps the total within the threshold.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n log(max(nums)))
```

For every Binary Search step, I traverse all `n` elements to calculate the sum.

The divisor search range is from `1` to `max(nums)`.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 📌 Constraints

* `1 <= nums.length <= 5 * 10⁴`
* `1 <= nums[i] <= 10⁶`
* `nums.length <= threshold <= 10⁶`

---

## 📌 Key Takeaways

* This is **Binary Search on Answer**.
* The search space is the possible divisor from `1` to `max(nums)`.
* For every divisor, calculate `ceil(nums[i] / divisor)`.
* If the sum is within the threshold, the divisor works.
* When a divisor works, search left for a smaller valid divisor.
* When it doesn't work, search right for a larger divisor.
* `ans` stores the smallest valid divisor found.
* The condition becomes easier to satisfy as the divisor increases.
* Time complexity is `O(n log(max(nums)))` with `O(1)` extra space.
