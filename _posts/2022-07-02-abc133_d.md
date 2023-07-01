---
title: "AtCoderBeginnerContest133 D 問題 400 点 「Rain Flows into Dams」"
date: 2022-07-02
layout: post
tags: ["ABC", "ABC133"]
---

# AtCoderBeginnerContest133 D 問題 400 点 「Rain Flows into Dams」

<a href="https://atcoder.jp/contests/abc133/tasks/abc133_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

入力例を眺める。

```
3
2 2 4
```

入力例から式を考えると，各山の水量を$v_i$とすると
$\frac{v_0}{2} + \frac{v_1}{2} = A_0$
$\frac{v_1}{2} + \frac{v_2}{2} = A_1$
$\frac{v_2}{2} + \frac{v_0}{2} = A_2$
式を$v_i$について解くと，
$v_0 = 2A_0 - v_1$
$v_1 = 2A_1 - v_2$
$v_2 = 2A_2 - v_0$
となり，$v_0$が$\bold{A}$だけを用いて$A_0 - A_1 + A_2$と表せる。
つまり，$v_0$には$i$の偶奇で足すか引くかが決まる。
$v_1 \dots v_N$に関しては，$v_i =2A_i - v_{i - 1}$と表せるので，$\mathcal{O}(N)$で計算可能。

## お気持ち

式変形して答え求めるのつらい

## AC コード

```python
N = int(input())
A = list(map(int, input().split()))
X = [0] * N
for i in range(N):
    if i % 2 == 0:
        X[0] += A[i]
    else:
        X[0] -= A[i]
for i in range(1, N):
    X[i] = 2 * A[i - 1] - X[i - 1]
print(*X)
```
