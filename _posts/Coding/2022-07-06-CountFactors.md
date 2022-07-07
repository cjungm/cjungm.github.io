---
title: CountFactors
author: J.M
date: 2022-07-06
category: Coding
layout: post
---

###### 문제 설명

A positive integer D is a *factor* of a positive integer N if there exists an integer M such that N = D * M.

For example, 6 is a factor of 24, because M = 4 satisfies the above condition (24 = 6 * 4).

Write a function:

> ```
> def solution(N)
> ```

that, given a positive integer N, returns the number of its factors.

For example, given N = 24, the function should return 8, because 24 has 8 factors, namely 1, 2, 3, 4, 6, 8, 12, 24. There are no other factors of 24.

Write an **efficient** algorithm for the following assumptions:

> - N is an integer within the range [1..2,147,483,647].

나의 답 : 

```python
# 주어진 수 N의 약수의 갯수를 구하시오
# 전체 리스트 순회
# try 1

def solution(N):
    # write your code in Python 3.6
    divisorsList = []

    for i in range(1, N + 1):
        if (N % i == 0) :
            divisorsList.append(i)

    return len(divisorsList)
```

```python
# N의 약수의 짝 중 작은 수는 N의 제곱근을 넘지 않는다.
# 따라서 N의 제곱근까지만 순회합니다.
# try 2

def solution(N):

    divisorsList = []

    for i in range(1, int(N**(1/2)) + 1):
        if (N % i == 0):
            divisorsList.append(i) 
            if ( (i**2) != N) : 
                divisorsList.append(N // i)

    divisorsList.sort()
    
    return len(divisorsList)
```

[출처](https://app.codility.com/programmers/lessons/10-prime_and_composite_numbers/count_factors/start/)
