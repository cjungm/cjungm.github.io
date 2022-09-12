---
title: MinAvgTwoSlice
author: J.M
date: 2022-06-30
category: Coding
layout: post
---

###### 문제 설명

A non-empty array A consisting of N integers is given. A pair of integers (P, Q), such that 0 ≤ P < Q < N, is called a *slice* of array A (notice that the slice contains at least two elements). The *average* of a slice (P, Q) is the sum of A[P] + A[P + 1] + ... + A[Q] divided by the length of the slice. To be precise, the average equals (A[P] + A[P + 1] + ... + A[Q]) / (Q − P + 1).

For example, array A such that:

```
    A[0] = 4    A[1] = 2    A[2] = 2    A[3] = 5    A[4] = 1    A[5] = 5    A[6] = 8
```

contains the following example slices:

> - slice (1, 2), whose average is (2 + 2) / 2 = 2;
> - slice (3, 4), whose average is (5 + 1) / 2 = 3;
> - slice (1, 4), whose average is (2 + 2 + 5 + 1) / 4 = 2.5.

The goal is to find the starting position of a slice whose average is minimal.

Write a function:

> ```
> class Solution { public int solution(int[] A); }
> ```

that, given a non-empty array A consisting of N integers, returns the starting position of the slice with the minimal average. If there is more than one slice with a minimal average, you should return the smallest starting position of such a slice.

For example, given array A such that:

```
    A[0] = 4    A[1] = 2    A[2] = 2    A[3] = 5    A[4] = 1    A[5] = 5    A[6] = 8
```

the function should return 1, as explained above.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N is an integer within the range [2..100,000];
> - each element of array A is an integer within the range [−10,000..10,000].

나의 답 : 

```python
# try 1

def solution(S, P, Q):
    # write your code in Python 3.6
    letter_dict = {
        "A" : 1,
        "C" : 2,
        "G" : 3,
        "T" : 4
    }

    list_s = list(S)
    max_len = len(list_s)
    answer = []
    
    for p, q in zip(P, Q):
        if p > max_len:
            p=max_len
        if q > max_len:
            q=max_len
        answer.append(letter_dict[min(list_s[p:q+1])])
    
    return answer
```

```python
# try 2

def solution(S, P, Q):
    # write your code in Python 3.6
    answer=[]
    for p, q in zip(P, Q):
        if p > len(S):
            p=len(S)
        if q > len(S):
            q=len(S)

        if 'A' in S[p:q+1]:
            answer.append(1)
        elif 'C' in S[p:q+1]:
            answer.append(2)
        elif 'G' in S[p:q+1]:
            answer.append(3)
        elif 'T' in S[p:q+1]:
            answer.append(4)
    
    return answer
```

[출처](https://app.codility.com/programmers/lessons/5-prefix_sums/min_avg_two_slice/)
