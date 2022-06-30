---
title: MissingInteger
author: J.M
date: 2022-06-29
category: Coding
layout: post
---

###### 문제 설명

Write a function:

> ```
> def solution(A)
> ```

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

For example, given A = [1, 3, 6, 4, 1, 2], the function should return 5.

Given A = [1, 2, 3], the function should return 4.

Given A = [−1, −3], the function should return 1.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N is an integer within the range [1..100,000];
> - each element of array A is an integer within the range [−1,000,000..1,000,000].

나의 답 :

```python
def solution(A):
    # write your code in Python 3.6
    A=set(A)
    max_val = max(max(A)+1,1)
    return min(set(range(1, max_val+1)).difference(A))
```

[출처](https://app.codility.com/programmers/lessons/4-counting_elements/missing_integer/start/)
