---
title: "AtCoderBeginnerContest183 E 問題 500 点 「Queen on Grid」"
date: 2022-07-02
layout: post
tags: ["ABC", "ABC183"]
---

# AtCoderBeginnerContest183 E 問題 500 点 「Queen on Grid」

<a href="https://atcoder.jp/contests/abc183/tasks/abc183_e" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

もらう DP とかいうやつらしい。マップの各地点の数とその累積和が必要で，それぞれ DP と累積和で表せるっぽい。こういう DP は初めてだが，理解はできる…？

## お気持ち

## AC コード

```python
#coding: utf-8
H, W = map(int, input().split())
mod = 10**9 + 7
mat = [input() for _ in range(H)]
dp = [[0 for _ in range(2000)] for _ in range(2000)]
X = [[0 for _ in range(2000)] for _ in range(2000)]
Y = [[0 for _ in range(2000)] for _ in range(2000)]
Z = [[0 for _ in range(2000)] for _ in range(2000)]
dp[0][0] = 1
for i in range(H):
    for j in range(W):
        if i == 0 and j == 0:
            continue
        if mat[i][j] == "#":
            continue
        if j > 0:
            X[i][j] = (X[i][j-1] + dp[i][j-1]) % mod
        if i > 0:
            Y[i][j] = (Y[i-1][j] + dp[i-1][j]) % mod
        if i > 0 and j > 0:
            Z[i][j] = (Z[i-1][j-1] + dp[i-1][j-1]) % mod
        dp[i][j] = (X[i][j] + Y[i][j] + Z[i][j]) % mod
print(dp[H-1][W-1])
```
