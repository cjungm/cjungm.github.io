---
title: ChocolatesByNumbers
author: J.M
date: 2022-07-11
category: Coding
layout: post
---

###### 문제 설명

Two positive integers N and M are given. Integer N represents the number of chocolates arranged in a circle, numbered from 0 to N − 1.

You start to eat the chocolates. After eating a chocolate you leave only a wrapper.

You begin with eating chocolate number 0. Then you omit the next M − 1 chocolates or wrappers on the circle, and eat the following one.

More precisely, if you ate chocolate number X, then you will next eat the chocolate with number (X + M) modulo N (remainder of division).

You stop eating when you encounter an empty wrapper.

For example, given integers N = 10 and M = 4. You will eat the following chocolates: 0, 4, 8, 2, 6.

The goal is to count the number of chocolates that you will eat, following the above rules.

Write a function:

> ```
> def solution(N, M)
> ```

that, given two positive integers N and M, returns the number of chocolates that you will eat.

For example, given integers N = 10 and M = 4. the function should return 5, as explained above.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N and M are integers within the range [1..1,000,000,000].

나의 답 : 

```python
# try 1

def solution(N, M):
    # write your code in Python 3.6
    arr_n = [0]*N
    idx = 0
    count = 0
    while arr_n[idx] == 0:
        arr_n[idx] = 1
        idx = (idx + M) % N
        count += 1
    return count
```

```python
# try 2

def solution(N, M):
    # write your code in Python 3.6
    arr_dict = {}
    idx = 0
    count = 0
    while idx not in arr_dict:
        arr_dict[idx] = 1
        idx = (idx + M) % N
        count += 1
    return count
```

```python
# try 3

def gcd(a, b):
    # 최대 공약수
    if (a % b == 0):
        return b
    else:
        return gcd(b, a % b)
def solution(N, M):
    # write your code in Python 3.6
    lcm = N * M / gcd(N, M) # 최소 공배수
    return int(lcm // M)
```

[출처](https://app.codility.com/programmers/lessons/12-euclidean_algorithm/chocolates_by_numbers/start/)
