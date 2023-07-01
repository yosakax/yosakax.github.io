---
tags: ["caddi""]
---

# CADDi 2018 for Beginners D 問題 400 点 「Harlequin」

<a href="https://atcoder.jp/contests/abc242/tasks/abc242_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

それぞれのリンゴの数の偶奇を見ていく。すべてのリンゴが偶数である場合，後手は先手の後追いをしていくと自然と勝つ。対して奇数が存在する場合，奇数のリンゴを一回目ですべて選択することで先手と後手が入れ替わるので，結果的に先手が勝つことができる。一度に取れるリンゴは 1 つかつ一度取ったリンゴは取ってはいけないと誤読してた…問題はよく読もう

## お気持ち

## AC コード

```python
#coding: utf-8
N = int(input())
f, s = 0, 0
odd, even = 0, 0
for i in range(N):
    a = int(input())
    if a % 2 == 0:
        even += 1
    else:
        odd += 1
if odd > 0:
    flag = True
else:
    flag = False
print("first" if flag else "second")
```
