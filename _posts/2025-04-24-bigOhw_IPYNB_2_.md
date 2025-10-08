---
layout: page
title: Big O Algorithmic Efficiency HW
toc: True
permalink: /binary_history/bigOhw
categories: ['CSP Classwork']
---

### Homework Hack:

#### O(1) Complexity

```python
def add_two_multiply_three(n):
    return (n + 2) * 3
```

#### O(log n) Complexity

```python

# Find smallest number greater than target

def smallest(nums, target):
    left = 0
    right = len(nums) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] >= target:
            result = mid
            right = mid - 1
        else:
            left = mid + 1

    return result
```

#### O(n) Complexity:

```python
def factorial(arr):
    total = 0
    for num in arr:
        total *= num
    return total
```

#### O(n²) Complexity:

```python
def duplicates(arr):
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] == arr[j]:
                return True
    return False
```
