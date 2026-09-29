# Arrays - Practice
# Day 2


# Problem 1
# Find the second largest DISTINCT element

arr = [10, 5, 8, 20, 20, 3]

largest = float('-inf')
second_largest = float('-inf')

for x in arr:
    if x > largest:
        second_largest = largest
        largest = x
    elif x > second_largest and x != largest:
        second_largest = x

print("Second largest:", second_largest)

# Output:
# Second largest: 10


# Problem 2
# Reverse an array without creating another array

arr = [1, 2, 3, 4, 5]

left = 0
right = len(arr) - 1

while left < right:
    arr[left], arr[right] = arr[right], arr[left]

    left += 1
    right -= 1

print("Reversed:", arr)

# Output:
# Reversed: [5, 4, 3, 2, 1]


# Problem 3
# Move all zeros to the end
# The order of the other elements should stay the same

arr = [0, 1, 0, 3, 12]

insert_pos = 0

for i in range(len(arr)):
    if arr[i] != 0:
        arr[insert_pos] = arr[i]
        insert_pos += 1

while insert_pos < len(arr):
    arr[insert_pos] = 0
    insert_pos += 1

print("After moving zeros:", arr)

# Output:
# After moving zeros: [1, 3, 12, 0, 0]


# Problem 4
# Find the maximum subarray sum
# Using Kadane's Algorithm

arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

current_sum = arr[0]
best_sum = arr[0]

for i in range(1, len(arr)):
    current_sum = max(arr[i], current_sum + arr[i])
    best_sum = max(best_sum, current_sum)

print("Maximum subarray sum:", best_sum)

# Output:
# Maximum subarray sum: 6


# Problem 5
# Find the sum of different ranges using prefix sum

arr = [5, 2, 7, 3, 6, 1]

prefix = [0] * len(arr)
prefix[0] = arr[0]

for i in range(1, len(arr)):
    prefix[i] = prefix[i - 1] + arr[i]

print("Prefix:", prefix)

queries = [(1, 3), (2, 5), (0, 4), (3, 3)]

for l, r in queries:

    if l == 0:
        answer = prefix[r]
    else:
        answer = prefix[r] - prefix[l - 1]

    print("Range", (l, r), "=", answer)

# Output:
# Prefix: [5, 7, 14, 17, 23, 24]
# Range (1, 3) = 12
# Range (2, 5) = 17
# Range (0, 4) = 23
# Range (3, 3) = 3