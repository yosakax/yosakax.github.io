---
title: "AtCoderPetrozavodskContest001 B 問題 300 点 「Two Arrays」"
date: 2022-07-02
layout: post
tags: ["APC"]
---

# AtCoderPetrozavodskContest001 B 問題 300 点 「Two Arrays」

<a href="https://atcoder.jp/contests/apc001/tasks/apc001_b" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

どの要素にどれだけ足すかはあまり考えなくてよい。問題は要素ごとの差の合計を考える。
ある要素$ a_i, b_i$について考える。

- もし$ a_i \le b_i$の時
  - B 側には$ \frac{b_i - a_i}{2}$だけ足される
- そうでない場合
  - A 側には$ a_i - b_i$だけ足される

$ 1 \le i \le N$について以上の操作を行うことで，それぞれに何回加算されるかがわかる。$ A \ge B$となれば条件を満たす。<-- これがまだちゃんとわかっていない

## お気持ち

## AC コード

```python
#coding: utf-8
N = int(input())
A = list(map(int, input().split()))
B = list(map(int, input().split()))
# K = sum(B) - sum(A)
a, b = 0, 0
for i in range(N):
    if A[i] < B[i]:
        b += (B[i] - A[i]) // 2
    else:
        a += A[i] - B[i]
flag = a <= b
print("Yes" if flag else "No")
```
