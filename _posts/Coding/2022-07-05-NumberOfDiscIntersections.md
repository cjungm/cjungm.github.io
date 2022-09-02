---
title: NumberOfDiscIntersections
author: J.M
date: 2022-07-05
category: Coding
layout: post
---

###### 문제 설명

We draw N discs on a plane. The discs are numbered from 0 to N − 1. An array A of N non-negative integers, specifying the radiuses of the discs, is given. The J-th disc is drawn with its center at (J, 0) and radius A[J].

We say that the J-th disc and K-th disc intersect if J ≠ K and the J-th and K-th discs have at least one common point (assuming that the discs contain their borders).

The figure below shows discs drawn for N = 6 and A as follows:

```
  A[0] = 1  A[1] = 5  A[2] = 2  A[3] = 1  A[4] = 4  A[5] = 0
```

![img](https://codility-frontend-prod.s3.amazonaws.com/media/task_static/number_of_disc_intersections/static/images/auto/0eed8918b13a735f4e396c9a87182a38.png)

There are eleven (unordered) pairs of discs that intersect, namely:

> - discs 1 and 4 intersect, and both intersect with all the other discs;
> - disc 2 also intersects with discs 0 and 3.

Write a function:

> ```
> def solution(A)
> ```

that, given an array A describing N discs as explained above, returns the number of (unordered) pairs of intersecting discs. The function should return −1 if the number of intersecting pairs exceeds 10,000,000.

Given array A shown above, the function should return 11, as explained above.

Write an **efficient** algorithm for the following assumptions:

> - N is an integer within the range [0..100,000];
> - each element of array A is an integer within the range [0..2,147,483,647].

나의 답 : 

```python
# try 1

def solution(A):
    # write your code in Python 3.6
    answer = 0
    circle_list = []
    for idx, radius in enumerate(A):
        circle_list.append((idx - radius, -1))
        circle_list.append((idx + radius, 1))

    circle_list.sort()
    target = 0

    for pos in circle_list:
        if pos[1]==-1:
            target+=1
            answer+=target
        else:
            target-=1
            answer-=1
    return answer
```

```python
# try 2

def solution(A):
    # write your code in Python 3.6
    answer = 0
    circle_list = []
    for idx, radius in enumerate(A):
        circle_list.append((idx - radius, -1))
        circle_list.append((idx + radius, 1))

    circle_list.sort()
    target = 0

    for pos in circle_list:
        if answer > 10000000 and pos[1]==-1:
            return -1
        if pos[1]==-1:
            target+=1
            answer+=target
        else:
            target-=1
            answer-=1
    return answer
```

[출처](https://app.codility.com/programmers/lessons/6-sorting/number_of_disc_intersections/start/)
