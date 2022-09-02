---
title: CountSemiprimes
author: J.M
date: 2022-07-10
category: Coding
layout: post
---

###### 문제 설명

A *prime* is a positive integer X that has exactly two distinct divisors: 1 and X. The first few prime integers are 2, 3, 5, 7, 11 and 13.

A *semiprime* is a natural number that is the product of two (not necessarily distinct) prime numbers. The first few semiprimes are 4, 6, 9, 10, 14, 15, 21, 22, 25, 26.

You are given two non-empty arrays P and Q, each consisting of M integers. These arrays represent queries about the number of semiprimes within specified ranges.

Query K requires you to find the number of semiprimes within the range (P[K], Q[K]), where 1 ≤ P[K] ≤ Q[K] ≤ N.

For example, consider an integer N = 26 and arrays P, Q such that:

```
    P[0] = 1    Q[0] = 26    P[1] = 4    Q[1] = 10    P[2] = 16   Q[2] = 20
```

The number of semiprimes within each of these ranges is as follows:

> - (1, 26) is 10,
> - (4, 10) is 4,
> - (16, 20) is 0.

Write a function:

> ```
> def solution(N, P, Q)
> ```

that, given an integer N and two non-empty arrays P and Q consisting of M integers, returns an array consisting of M elements specifying the consecutive answers to all the queries.

For example, given an integer N = 26 and arrays P, Q such that:

```
    P[0] = 1    Q[0] = 26    P[1] = 4    Q[1] = 10    P[2] = 16   Q[2] = 20
```

the function should return the values [10, 4, 0], as explained above.

Write an **efficient** algorithm for the following assumptions:

> - N is an integer within the range [1..50,000];
> - M is an integer within the range [1..30,000];
> - each element of arrays P and Q is an integer within the range [1..N];
> - P[i] ≤ Q[i].

나의 답 : 

```python
# try 1

import math

def checkSemiprime(num):
    cnt = 0
 
    for i in range(2, int(math.sqrt(num)) + 1):
        while num % i == 0:
            num /= i
            cnt += 1
        if cnt >= 2:
            break
    if(num > 1):
        cnt += 1

    return cnt == 2

def solution(N, P, Q):
    # write your code in Python 3.6
    answer = []
    min_val = min(P)
    max_val = max(Q)
    prime_list = [0] * (max_val + 1)
    for elem in range(min_val, max_val+1):
        if int(elem**(1/3)) == elem**(1/3):
            pass
        elif count_measure(elem) in (3, 4):
            prime_list[elem]=1

    for p, q in zip(P, Q):
        answer.append(sum(prime_list[p:q+1]))
    return answer
```

```python
# try 2

import math

def checkSemiprime(num):
    cnt = 0
 
    for i in range(2, int(math.sqrt(num)) + 1):
        while num % i == 0:
            num /= i
            cnt += 1
        if cnt >= 2:
            break
    if(num > 1):
        cnt += 1

    return cnt == 2

def solution(N, P, Q):
    # write your code in Python 3.6
    answer = []
    min_val = min(P)
    max_val = max(Q)
    prime_list = [0] * (max_val + 1)
    for p, q in zip(P, Q):
        temp = 0
        for elem in range(p, q+1):
            if checkSemiprime(elem):
                temp+=1
        answer.append(temp)
    return answer
```

```python
# try 3

import math

def checkSemiprime(num):
    cnt = 0
 
    for i in range(2, int(math.sqrt(num)) + 1):
        while num % i == 0:
            num /= i
            cnt += 1
        if cnt >= 2:
            break
    if(num > 1):
        cnt += 1

    return cnt == 2

def solution(N, P, Q):
    # write your code in Python 3.6
    answer = []
    min_val = min(P)
    max_val = max(Q)
    prime_list = [0] * (max_val + 1)
    for elem in range(min_val, max_val+1):
        if checkSemiprime(elem):
            prime_list[elem]=prime_list[elem-1] + 1
        else:
            prime_list[elem]=prime_list[elem-1]

    for p, q in zip(P, Q):
        answer.append(prime_list[q]-prime_list[p-1])
    return answer
```

[출처](https://app.codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_semiprimes/start/)
