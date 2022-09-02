---
title: CountNonDivisible
author: J.M
date: 2022-07-09
category: Coding
layout: post
---

###### 문제 설명

You are given an array A consisting of N integers.

For each number A[i] such that 0 ≤ i < N, we want to count the number of elements of the array that are not the divisors of A[i]. We say that these elements are non-divisors.

For example, consider integer N = 5 and array A such that:

```
    A[0] = 3    A[1] = 1    A[2] = 2    A[3] = 3    A[4] = 6
```

For the following elements:

> - A[0] = 3, the non-divisors are: 2, 6,
> - A[1] = 1, the non-divisors are: 3, 2, 3, 6,
> - A[2] = 2, the non-divisors are: 3, 3, 6,
> - A[3] = 3, the non-divisors are: 2, 6,
> - A[4] = 6, there aren't any non-divisors.

Write a function:

> ```
> def solution(A)
> ```

that, given an array A consisting of N integers, returns a sequence of integers representing the amount of non-divisors.

Result array should be returned as an array of integers.

For example, given:

```
    A[0] = 3    A[1] = 1    A[2] = 2    A[3] = 3    A[4] = 6
```

the function should return [2, 4, 3, 2, 0], as explained above.

Write an **efficient** algorithm for the following assumptions:

> - N is an integer within the range [1..50,000];
> - each element of array A is an integer within the range [1..`2 * N`].

나의 답 : 

```python
# try 1

from collections import Counter

def solution(A):
    # write your code in Python 3.6
    elem_dict = list(Counter(A).items())
    elem_dict.sort()
    
    saved = [-1] * (max(A)+1)
    answer = []
    for elem in A:
        if saved[elem] == -1:
            count = 0
            for elem_div in elem_dict:
                if elem%elem_div[0]==0:
                    count+=elem_div[1]
                if elem == elem_div[0]:
                    break
            answer.append(len(A) - count)
            saved[elem] = len(A) - count
        else:
            answer.append(saved[elem])

    return answer
```

```python
# try 2

from collections import Counter

def solution(A):
    # write your code in Python 3.6
    elem_dict = Counter(A)
    
    
    saved = [-1] * (max(A)+1)
    answer = []
    for elem in A:
        if saved[elem] == -1:
            count = 0
            for elem_div in range(1, int(elem**0.5) + 1):
                if elem%elem_div==0:
                    count+=elem_dict[elem_div]
                    if elem / elem_div!=elem_div:
                        count += elem_dict[elem//elem_div]

            answer.append(len(A) - count)
            saved[elem] = len(A) - count
        else:
            answer.append(saved[elem])

    return answer
```

[출처](https://app.codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_non_divisible/start/)
