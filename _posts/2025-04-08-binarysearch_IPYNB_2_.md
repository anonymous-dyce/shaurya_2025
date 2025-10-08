---
layout: page
title: Binary Search HW
toc: True
permalink: /binary_history/binarysearchhw
categories: ['CSP Classwork']
---

#### Homework Hack #1

```python
def search(nums, target):
    left = 0
    right = len(nums) - 1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            return mid

        if nums[left] <= nums[mid]:  # Left half is sorted
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:  # Right half is sorted
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1
```

#### Homework Hack #2

``` python
def firstandlast(nums, target):

    first = -1
    left = 0
    right = len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] >= target:
            if nums[mid] == target:
                first = mid
            right = mid - 1
        else:
            left = mid + 1

    last = -1
    left = 0
    right = len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] <= target:
            if nums[mid] == target:
                last = mid
            left = mid + 1
        else:
            right = mid - 1

    return (first, last) if first != -1 else -1
```

#### Homework Hack #3

``` python

def smallest(nums, target):
    result = -1
    left = 0
    right = len(nums) - 1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] >= target:
            result = mid
            right = mid - 1
        else:
            left = mid + 1

    return result
```
