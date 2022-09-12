---
title: MaxDoubleSliceSum
author: J.M
date: 2022-07-04
category: Coding
layout: post
---

###### 문제 설명

A non-empty array A consisting of N integers is given.

A triplet (X, Y, Z), such that 0 ≤ X < Y < Z < N, is called a *double slice*.

The *sum* of double slice (X, Y, Z) is the total of A[X + 1] + A[X + 2] + ... + A[Y − 1] + A[Y + 1] + A[Y + 2] + ... + A[Z − 1].

For example, array A such that:

```
    A[0] = 3    A[1] = 2    A[2] = 6    A[3] = -1    A[4] = 4    A[5] = 5    A[6] = -1    A[7] = 2
```

contains the following example double slices:

> - double slice (0, 3, 6), sum is 2 + 6 + 4 + 5 = 17,
> - double slice (0, 3, 7), sum is 2 + 6 + 4 + 5 − 1 = 16,
> - double slice (3, 4, 5), sum is 0.

The goal is to find the maximal sum of any double slice.

Write a function:

> ```
> def solution(A)
> ```

that, given a non-empty array A consisting of N integers, returns the maximal sum of any double slice.

For example, given:

```
    A[0] = 3    A[1] = 2    A[2] = 6    A[3] = -1    A[4] = 4    A[5] = 5    A[6] = -1    A[7] = 2
```

the function should return 17, because no double slice of array A has a sum of greater than 17.

Write an **efficient** algorithm for the following assumptions:

> - N is an integer within the range [3..100,000];
> - each element of array A is an integer within the range [−10,000..10,000].

나의 답 : 

```python
def solution(A):
    # write your code in Python 3.6
    len_a = len(A)
    front_sum = [0] * len_a
    back_sum = [0] * len_a
    
    for f in range(1, len_a-2):
        if  front_sum[f-1]+A[f] > 0:
            front_sum[f] = front_sum[f-1] + A[f]
            
    for b in range(len_a-2, 1, -1):
        if  back_sum[b+1] + A[b] > 0:
            back_sum[b] = back_sum[b+1] + A[b]
            
    max_sum = 0
    
    for i in range(1, len_a-1):
        if front_sum[i-1] + back_sum[i+1] > max_sum:
            max_sum = front_sum[i-1] + back_sum[i+1]
            
    return max_sum
```

[출처](https://app.codility.com/programmers/lessons/9-maximum_slice_problem/max_double_slice_sum/start/)
