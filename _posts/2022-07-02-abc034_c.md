---
title: "AtCoderBeginnerContest034 C 問題 300 点 「経路」"
date: 2022-07-02
layout: post
tags: ["ABC", "ABC034"]
---

# AtCoderBeginnerContest034 C 問題 300 点 「経路」

<a href="https://atcoder.jp/contests/abc034/tasks/abc034_c" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

数学的に考えれば$ (W + H)! / (W! \* H!)$で簡単だが，問題は桁数が大きく計算が難しいこと。しかし，事前に逆源をとっておけば問題なく計算できる。W, Hの制約から，$ 2 \times 10^5$くらい前計算しておけば問題ない

## お気持ち

## AC コード

```python
def make_tables(mod, n):
    fac = [1, 1]  # 階乗テーブル・・・(1)
    ifac = [1, 1]  # 逆元の階乗テーブル・・・(2)
    inverse = [0, 1]  # 逆元テーブル・・・(3)

    for i in range(2, n + 1):
        fac.append((fac[-1] * i) % mod)
        inverse.append((-inverse[mod % i] * (mod // i)) % mod)
        ifac.append((ifac[-1] * inverse[-1]) % mod)
    return fac, ifac


W, H = map(lambda x: int(x) - 1, input().split())
mod = int(1e9) + 7
fac, ifac = make_tables(mod, int(2e5 + 10))
ans = ((fac[H + W] * ifac[H]) % mod * ifac[W]) % mod
print(ans)
```
