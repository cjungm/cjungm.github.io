---
title: EquiLeader
author: J.M
date: 2022-07-06
category: Coding
layout: post
---

###### 문제 설명

A non-empty array A consisting of N integers is given.

The *leader* of this array is the value that occurs in more than half of the elements of A.

An *equi leader* is an index S such that 0 ≤ S < N − 1 and two sequences A[0], A[1], ..., A[S] and A[S + 1], A[S + 2], ..., A[N − 1] have leaders of the same value.

For example, given array A such that:

```
    A[0] = 4    A[1] = 3    A[2] = 4    A[3] = 4    A[4] = 4    A[5] = 2
```

we can find two equi leaders:

> - 0, because sequences: (4) and (3, 4, 4, 4, 2) have the same leader, whose value is 4.
> - 2, because sequences: (4, 3, 4) and (4, 4, 2) have the same leader, whose value is 4.

The goal is to count the number of equi leaders.

Write a function:

> ```
> def solution(A)
> ```

that, given a non-empty array A consisting of N integers, returns the number of equi leaders.

For example, given:

```
    A[0] = 4    A[1] = 3    A[2] = 4    A[3] = 4    A[4] = 4    A[5] = 2
```

the function should return 2, as explained above.

Write an **efficient** algorithm for the following assumptions:

> - N is an integer within the range [1..100,000];
> - each element of array A is an integer within the range [−1,000,000,000..1,000,000,000].

나의 답 : 

```python
# try 1

from collections import Counter

def solution(A):
    # write your code in Python 3.6
    answer = 0
    total = Counter(A)
    len_a = len(A)
    if total[A[0]]-1 > (len_a-1)/2:
        answer+=1
    mid_idx = len_a//2 if len_a % 2 == 0 else (len_a+1)//2
    
    for idx in range(1,len_a):
        temp_len = idx+1
        other_len = len_a - temp_len
        temp_list = A[:idx+1]
        temp = sorted(list(Counter(temp_list).items()), key=lambda x: x[1], reverse=True)[0]
        temp_dom = temp[1]
        other_dom = total[temp[0]] - temp_dom
        if temp_dom > temp_len/2 and other_dom > other_len/2:
            answer+=1
    return answer
```

```python
# try 2

from collections import Counter

def solution(A):
    # write your code in Python 3.6
    answer = 0
    total = Counter(A)
    max_item = sorted(list(total.items()), key=lambda x: x[1], reverse=True)[0]
    len_a = len(A)

    temp_len = 0
    temp_dom = 0
    for elem in A:
        temp_len += 1
        other_len = len_a - temp_len
        if elem == max_item[0]:
            temp_dom += 1
            other_dom = max_item[1] - temp_dom
        if temp_dom > temp_len/2 and other_dom > other_len/2:

            answer+=1
    return answer
```



[출처](https://app.codility.com/programmers/lessons/8-leader/equi_leader/start/)
