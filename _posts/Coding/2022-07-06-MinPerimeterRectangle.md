---
title: MinPerimeterRectangle
author: J.M
date: 2022-07-06
category: Coding
layout: post
---

###### 문제 설명

An integer N is given, representing the area of some rectangle.

The *area* of a rectangle whose sides are of length A and B is A * B, and the *perimeter* is 2 * (A + B).

The goal is to find the minimal perimeter of any rectangle whose area equals N. The sides of this rectangle should be only integers.

For example, given integer N = 30, rectangles of area 30 are:

> - (1, 30), with a perimeter of 62,
> - (2, 15), with a perimeter of 34,
> - (3, 10), with a perimeter of 26,
> - (5, 6), with a perimeter of 22.

Write a function:

> ```
> def solution(N)
> ```

that, given an integer N, returns the minimal perimeter of any rectangle whose area is exactly equal to N.

For example, given an integer N = 30, the function should return 22, as explained above.

Write an **efficient** algorithm for the following assumptions:

> - N is an integer within the range [1..1,000,000,000].

나의 답 : 

```python
# 주어진 수 N의 약수 집합에서 가장 낮은 짝의 합을 구하시오
def solution(N):

    divisorsList = []

    for i in range(1, int(N**(1/2)) + 1):
        if (N % i == 0):
            if ( (i**2) != N) : 
                divisorsList.append((i + N // i) * 2)
            else:
                divisorsList.append((i + i) * 2)
    
    return min(divisorsList)
```

[출처](https://app.codility.com/programmers/lessons/10-prime_and_composite_numbers/min_perimeter_rectangle/start/)
