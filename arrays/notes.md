# Arrays - DSA

## What is an Array?

An array is basically a collection of elements stored together.

Example:

```python
arr = [10, 20, 30, 40, 50]
```

Each element has an index.

```text
10  20  30  40  50
0   1   2   3   4
```

Index starts from `0`, not `1`.

So:

```python
arr[0]  # 10
arr[2]  # 30
```

---

## Accessing Elements

We can directly access an element using its index.

```python
arr = [10, 20, 30, 40]

print(arr[2])
```

Output:

```text
30
```

Time: **O(1)**

Because we already know the index, so we don't need to search through the array.

---

## Updating Elements

We can change an element using its index.

```python
arr = [10, 20, 30, 40]

arr[1] = 100

print(arr)
```

Output:

```text
[10, 100, 30, 40]
```

Time: **O(1)**

---

## Traversing

Traversal just means going through all the elements.

```python
arr = [10, 20, 30, 40]

for x in arr:
    print(x)
```

If there are `n` elements, we visit all of them.

Time: **O(n)**

---

## Sum of Array

Simple way:

```python
arr = [2, 4, 6, 8]

total = 0

for x in arr:
    total += x

print(total)
```

Output:

```text
20
```

Time: **O(n)**
Space: **O(1)**

---

## Maximum and Minimum

Can find both by going through the array once.

```python
arr = [5, 2, 9, 1, 7]

largest = arr[0]
smallest = arr[0]

for x in arr:
    if x > largest:
        largest = x

    if x < smallest:
        smallest = x

print(largest)
print(smallest)
```

Output:

```text
9
1
```

Time: **O(n)**
Space: **O(1)**

---

## Linear Search

Linear search = checking elements one by one until we find the target.

```python
arr = [10, 20, 30, 40, 50]
target = 40

for i in range(len(arr)):
    if arr[i] == target:
        print("Found at index", i)
        break
```

Output:

```text
Found at index 3
```

Best case: **O(1)**
Worst case: **O(n)**

If the element is at the beginning, we're lucky.

If it's at the end or not present, we might check the whole array.

Space: **O(1)**

---

# Insertion

Insertion means adding a new element.

Adding at the end:

```python
arr = [10, 20, 30]

arr.append(40)

print(arr)
```

Output:

```text
[10, 20, 30, 40]
```

For Python lists, append is **O(1) amortized**.

But inserting in the middle is slower.

Example:

```text
[10, 20, 30, 40]
```

Insert `25` at index `2`:

```text
[10, 20, 25, 30, 40]
```

The elements after it have to shift.

So middle insertion = **O(n)**

---

# Deletion

Deleting from the middle also needs shifting.

Example:

```text
[10, 20, 30, 40, 50]
```

Remove `30`:

```text
[10, 20, 40, 50]
```

`40` and `50` have to move.

So deletion from the middle = **O(n)**

---

# Prefix Sum

This was one of the important things from arrays.

Prefix sum is useful when we have to find the sum of different ranges again and again.

Example:

```text
arr = [2, 4, 1, 5, 3]
```

Prefix:

```text
[2, 6, 7, 12, 15]
```

Basically:

```text
2
2 + 4 = 6
2 + 4 + 1 = 7
2 + 4 + 1 + 5 = 12
2 + 4 + 1 + 5 + 3 = 15
```

Formula:

```text
prefix[i] = prefix[i - 1] + arr[i]
```

Code:

```python
arr = [2, 4, 1, 5, 3]

prefix = [0] * len(arr)

prefix[0] = arr[0]

for i in range(1, len(arr)):
    prefix[i] = prefix[i - 1] + arr[i]

print(prefix)
```

Output:

```text
[2, 6, 7, 12, 15]
```

Building prefix array = **O(n)**

---

# Range Sum

Suppose:

```text
arr = [2, 4, 1, 5, 3]
```

I want the sum from index `1` to `3`.

That is:

```text
4 + 1 + 5 = 10
```

Using prefix:

```text
prefix = [2, 6, 7, 12, 15]
```

Formula:

```text
prefix[r] - prefix[l - 1]
```

So:

```text
prefix[3] - prefix[0]
12 - 2
= 10
```

If `l = 0`, then just use:

```text
prefix[r]
```

So each range query becomes **O(1)**.

This is useful when there are a lot of queries.

Overall:

```text
Build prefix = O(n)
q queries = O(q)

Total = O(n + q)
```

---

# Two Pointers

Two pointers basically means using two indexes instead of doing everything with one.

Usually:

```python
left = 0
right = len(arr) - 1
```

One starts from the left and one from the right.

A simple example is reversing an array.

```python
arr = [1, 2, 3, 4, 5]

left = 0
right = len(arr) - 1

while left < right:
    arr[left], arr[right] = arr[right], arr[left]

    left += 1
    right -= 1

print(arr)
```

Output:

```text
[5, 4, 3, 2, 1]
```

Time: **O(n)**
Space: **O(1)**

The nice thing is that we're modifying the same array instead of creating another one.

---

# Move Zeros to End

Example:

```text
[0, 1, 0, 3, 12]
```

We want:

```text
[1, 3, 12, 0, 0]
```

The non-zero numbers should stay in the same order.

One way:

```python
arr = [0, 1, 0, 3, 12]

insert_pos = 0

for i in range(len(arr)):
    if arr[i] != 0:
        arr[insert_pos] = arr[i]
        insert_pos += 1

while insert_pos < len(arr):
    arr[insert_pos] = 0
    insert_pos += 1

print(arr)
```

Output:

```text
[1, 3, 12, 0, 0]
```

Time: **O(n)**
Space: **O(1)**

---

# Maximum Subarray Sum - Kadane's Algorithm

This finds the maximum sum of a **contiguous** part of an array.

Example:

```text
[-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

The best subarray is:

```text
[4, -1, 2, 1]
```

Sum = `6`

Code:

```python
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

current_sum = arr[0]
best_sum = arr[0]

for i in range(1, len(arr)):
    current_sum = max(arr[i], current_sum + arr[i])
    best_sum = max(best_sum, current_sum)

print(best_sum)
```

Output:

```text
6
```

The main idea is:

```text
Should I start a new subarray here?

OR

Should I continue the previous one?
```

Time: **O(n)**
Space: **O(1)**

---

# Complexity I Should Remember

| Operation        | Time           |
| ---------------- | -------------- |
| Access           | O(1)           |
| Update           | O(1)           |
| Traversal        | O(n)           |
| Linear Search    | O(n)           |
| Append           | O(1) amortized |
| Insert in middle | O(n)           |
| Delete in middle | O(n)           |
| Build Prefix Sum | O(n)           |
| Prefix Sum Query | O(1)           |

---

# My Takeaways

* Array index starts from `0`.
* Access using index is **O(1)**.
* Searching normally takes **O(n)**.
* Middle insertion/deletion takes **O(n)** because of shifting.
* Prefix sum is useful for repeated range-sum questions.
* Two pointers can reduce unnecessary work in some array problems.
* Kadane's algorithm is used for maximum subarray sum.
* Always check **time + space complexity** after solving a problem.
* Don't just memorize the code. Understand why it works.
