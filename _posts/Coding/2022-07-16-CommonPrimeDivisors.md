---
title: CommonPrimeDivisors
author: J.M
date: 2022-07-16
category: Coding
layout: post
---

###### 문제 설명

A *prime* is a positive integer X that has exactly two distinct divisors: 1 and X. The first few prime integers are 2, 3, 5, 7, 11 and 13.

A prime D is called a *prime divisor* of a positive integer P if there exists a positive integer K such that D * K = P. For example, 2 and 5 are prime divisors of 20.

You are given two positive integers N and M. The goal is to check whether the sets of prime divisors of integers N and M are exactly the same.

For example, given:

> - N = 15 and M = 75, the prime divisors are the same: {3, 5};
> - N = 10 and M = 30, the prime divisors aren't the same: {2, 5} is not equal to {2, 3, 5};
> - N = 9 and M = 5, the prime divisors aren't the same: {3} is not equal to {5}.

Write a function:

> ```
> def solution(A, B)
> ```

that, given two non-empty arrays A and B of Z integers, returns the number of positions K for which the prime divisors of A[K] and B[K] are exactly the same.

For example, given:

```
    A[0] = 15   B[0] = 75    A[1] = 10   B[1] = 30    A[2] = 3    B[2] = 5
```

the function should return 1, because only one pair (15, 75) has the same set of prime divisors.

Write an **\*efficient\*** algorithm for the following assumptions:

> - Z is an integer within the range [1..6,000];
> - each element of arrays A and B is an integer within the range [1..2,147,483,647].

모범 답 : 

```python
def gcd(x, y):
    ''' Compute the greatest common divisor.
    '''
    if x%y == 0:
        return y;
    else:
        return gcd(y, x%y)
def removeCommonPrimeDivisors(x, y):
    ''' Remove all prime divisors of x, which also exist in y. And
        return the remaining part of x.
    '''
    while x != 1:
        gcd_value = gcd(x, y)
        if gcd_value == 1:
            # x does not contain any more
            # common prime divisors
            break
        x /= gcd_value
    return x
def hasSamePrimeDivisors(x, y):
    gcd_value = gcd(x, y)   # The gcd contains all
                            # the common prime divisors
    x = removeCommonPrimeDivisors(x, gcd_value)
    if x != 1:
        # If x and y have exactly the same common
        # prime divisors, x must be composed by
        # the prime divisors in gcd_value. So
        # after previous loop, x must be one.
        return False
    y = removeCommonPrimeDivisors(y, gcd_value)
    return y == 1
def solution(A, B):
    count = 0
    for x,y in zip(A,B):
        if hasSamePrimeDivisors(x,y):
            count += 1
    return count
```

[출처](https://app.codility.com/programmers/lessons/12-euclidean_algorithm/common_prime_divisors/start/)

[설명 링크](https://mirae-kim.tistory.com/135)

[정답 링크](https://codesays.com/2014/solution-to-common-prime-divisors-by-codility/)
