---
title: "AtCoderBeginnerContest090 D 問題 400 点 「emainder Reminder」"
date: 2022-07-02
layout: post
tags: ["ABC", "ABC090"]
---

# AtCoderBeginnerContest090 D 問題 400 点 「emainder Reminder」

<a href="https://atcoder.jp/contests/abc090/tasks/abc090_d" blank="_target">問題リンク</a>

## 問題概要

$ a \mod b \ge K$となる$ (a, b)$の個数を列挙する

## 制約

## 解法

$ a = pb + r (0 \le r < b)$と考えると，aを0からNまで見ていくとき，それぞれのaで余りは $ 0, 1, ..., b-1$となる配列が p 回続き，$ 0, 1, ..., r$がそのあとに続く。
$ p = 0$の時の余りがK以上のものは$ b - K$個続く。さらに，$ r$の方を見ると$max(0, r - b + 1)$個ある。bを固定して考えることで，$\mathcal{O}(N)$で計算することができる。

## お気持ち

## AC コード

```python
#coding: utf-8
N, K = map(int, input().split())
ans = 0
if K == 0:
    ans = N ** 2
else:
    for b in range(K + 1, N + 1):
        if b > N:
            break
        ans += (b - K) * (N // b)
        tmp = max(N % b - K + 1, 0)
    ans += tmp
print(ans)
```
