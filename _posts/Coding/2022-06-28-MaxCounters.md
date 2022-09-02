---
title: MaxCounters
author: J.M
date: 2022-06-28
category: Coding
layout: post
---

###### 문제 설명

You are given N counters, initially set to 0, and you have two possible operations on them:

> - *increase(X)* − counter X is increased by 1,
> - *max counter* − all counters are set to the maximum value of any counter.

A non-empty array A of M integers is given. This array represents consecutive operations:

> - if A[K] = X, such that 1 ≤ X ≤ N, then operation K is increase(X),
> - if A[K] = N + 1 then operation K is max counter.

For example, given integer N = 5 and array A such that:

```
    A[0] = 3    A[1] = 4    A[2] = 4    A[3] = 6    A[4] = 1    A[5] = 4    A[6] = 4
```

the values of the counters after each consecutive operation will be:

```
    (0, 0, 1, 0, 0)    (0, 0, 1, 1, 0)    (0, 0, 1, 2, 0)    (2, 2, 2, 2, 2)    (3, 2, 2, 2, 2)    (3, 2, 2, 3, 2)    (3, 2, 2, 4, 2)
```

The goal is to calculate the value of every counter after all operations.

Write a function:

> ```
> def solution(N, A)
> ```

that, given an integer N and a non-empty array A consisting of M integers, returns a sequence of integers representing the values of the counters.

Result array should be returned as an array of integers.

For example, given:

```
    A[0] = 3    A[1] = 4    A[2] = 4    A[3] = 6    A[4] = 1    A[5] = 4    A[6] = 4
```

the function should return [3, 2, 2, 4, 2], as explained above.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N and M are integers within the range [1..100,000];
> - each element of array A is an integer within the range [1..`N + 1`].

나의 답 :

```python
# 1 try

def solution(N, A):
    # write your code in Python 3.6
    answer = [0]*N
    for elem in A:
        if elem == N+1:
            answer= [max(answer)]*N
        else:
            answer[elem-1]+=1
    return answer
```

```python
# 2 try

def solution(N, A):
    # write your code in Python 3.6
    answer = [0]*N
    max_elem = 0
    for elem in A:
        if elem == N+1:
            answer= [max_elem]*N
        else:
            answer[elem-1]+=1
            max_elem = answer[elem-1] if answer[elem-1] > max_elem else max_elem
    return answer
```

```python
# 3 try

def solution(N, A):
    # write your code in Python 3.6
    answer = [0]*N
    next_max_elem =  max_elem = 0
    for elem in A:
        if elem == N+1:
            max_elem = next_max_elem
        else:
            answer[elem-1]=max(max_elem +1,answer[elem-1]+1)
            next_max_elem = max(answer[elem-1], next_max_elem)
    return [c if c > max_elem else max_elem for c in answer]
```



[출처](https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/start/)



