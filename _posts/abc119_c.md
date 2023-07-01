---
title: "AtCoderBeginnerContest119 C 問題 300 点 「Synthetic Kadomatsu 」"
date: 2022-07-02
layout: post
tags: ["ABC", "ABC119"]
---

# AtCoderBeginnerContest119 C 問題 300 点 「Synthetic Kadomatsu 」

<a href="https://atcoder.jp/contests/abc119/tasks/abc119_c" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

すべての竹に対して

- A を作るために使う
- B を。。。
- C を。。。
- 使わない

の４通りを試し、それぞれでできた竹と目標値との差分の和+合成した竹の数\*10 のうち最小値を取る。この時の差分は正負は関係ない（伸ばしても縮めてもコストは１なので）。深さ優先の問題だと思ったが実装がうまく行かなかったので 4bit で分類してそれぞれの 4 通りを試した。

## お気持ち

## AC コード

```python
# coding: utf-8
def Base_10_to_n(X, n):
    X_dumy = X
    out = ''
    while X_dumy>0:
        out = str(X_dumy%n)+out
        X_dumy = int(X_dumy/n)
    return out

N, A, B, C = map(int, input().split())
L = [int(input()) for _ in range(N)]
ans = float("inf")
for i in range(4**N):
    bits = Base_10_to_n(i, 4).zfill(N)
    a, b, c = 0, 0, 0
    cost = 0
    for j in range(len(bits)):
        if bits[j] == "0":
            pass
        elif bits[j] == "1":
            a += L[j]
            cost += 10
        elif bits[j] == "2":
            b += L[j]
            cost += 10
        else:
            c += L[j]
            cost += 10
    if min(a, b, c) > 0:
        ans = min(ans, cost + abs(a-A)+abs(b-B)+abs(c-C) - 10*3)
print(ans)
```
