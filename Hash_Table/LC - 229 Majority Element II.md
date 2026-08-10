# 🧩 LeetCode 229 - Majority Element II

## 🔗 Problem
Given an integer array `nums`, return **all** elements that appear **more than ⌊ n / 3 ⌋ times**.

There can be **at most 2 majority elements**.

---

## 🏷️ Tags
- Array
- Hash Table
- Counting

---

## 📚 Topics
- Arrays
- HashMap
- Frequency Counting

---

## 💡 Intuition

The problem asks us to find all numbers whose frequency is **greater than n / 3**.

A simple way is:

1. Count the frequency of every element using a HashMap.
2. Traverse the HashMap.
3. If the frequency of an element is greater than `n / 3`, add it to the answer list.

---

## 🧠 Thought Process

1. First calculate the minimum frequency required.

```java
int condition = nums.length / 3;
```

Example:

```
n = 8

condition = 8 / 3 = 2

So frequency must be > 2.
```

Meaning:

```
3 ✔
4 ✔
5 ✔
...
```

---

### Step 2 : Create a HashMap

The HashMap stores

```
Key   -> Number
Value -> Frequency
```

Example:

```
nums = [3,2,3,2,2,1]

Map

3 -> 2
2 -> 3
1 -> 1
```

---

### Step 3 : Count every element

Traverse the array once.

If the number already exists,

increase its frequency.

Otherwise,

insert it with frequency 1.

```java
if(map.containsKey(nums[i])){
    map.put(nums[i], map.get(nums[i]) + 1);
}
else{
    map.put(nums[i], 1);
}
```

Example

```
nums = [1,2,2,3,2]

Iteration 1

1 -> 1

Iteration 2

1 -> 1
2 -> 1

Iteration 3

1 -> 1
2 -> 2

Iteration 4

1 -> 1
2 -> 2
3 -> 1

Iteration 5

1 -> 1
2 -> 3
3 -> 1
```

Now every number's frequency is stored.

---

### Step 4 : Traverse the HashMap

Now check every key.

If its frequency is greater than `condition`,
add it to the answer list.

```java
for(int key : map.keySet()){
    if(map.get(key) > condition){
        list.add(key);
    }
}
```

Example

```
condition = 2

Map

1 -> 1
2 -> 3
3 -> 2
```

Check one by one

```
1 -> 1 > 2 ❌

2 -> 3 > 2 ✅
Add 2

3 -> 2 > 2 ❌
```

Answer

```
[2]
```

---

## 🔍 Dry Run

Input

```
nums = [1,1,1,3,3,2,2,2]
```

Condition

```
n = 8

condition = 8 / 3 = 2
```

### Counting Frequencies

```
1 -> 3
3 -> 2
2 -> 3
```

Now traverse the map

```
1 -> 3 > 2 ✔

3 -> 2 > 2 ✖

2 -> 3 > 2 ✔
```

Answer

```
[1,2]
```

---

## ⏱️ Complexity

### Time Complexity

```
O(n)
```

- One traversal to count frequencies.
- One traversal of the HashMap.

Overall:

```
O(n)
```

---

### Space Complexity

```
O(n)
```

The HashMap may store every distinct element.

---

## 📌 Key Takeaways

- Use a HashMap to store **number → frequency**.
- `condition = n / 3`.
- Only add elements whose frequency is **greater than** `condition`.
- This is the straightforward HashMap solution.
- An optimized Boyer-Moore Voting Algorithm exists with **O(1)** extra space, but this approach is easier to understand and implement.
