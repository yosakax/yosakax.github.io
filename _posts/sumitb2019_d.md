---
title: "三井住友信託銀行プログラミングコンテスト 2019 D 問題 400 点 「Lucky PIN」"
date: 2022-07-02
layout: post
tags: ["sumitb"]
---

# 三井住友信託銀行プログラミングコンテスト 2019 D 問題 400 点 「Lucky PIN」

<a href="https://atcoder.jp/contests/sumitrust2019/tasks/sumitb2019_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

パスワードは３桁であるのは確定なので、000~999 までを解の候補として全探索を行う。解であるための条件はラッキ・ナンバのうち１桁目は２桁目より、２桁目は３桁目よりも前にいることなので、これを都度確認する。

## お気持ち

python では TLE になってしまったの pypy で提出して AC。今度の AtCoder での言語アップデートの後に Nim との速度差を比較してみたい。

## AC コード

```python
# coding: utf-8
N = int(input())
S = input()
ans = 0
for v in range(1000):
    v = str(v).zfill(3)
    flag = [False for _ in range(3)]
    for i in range(len(S)):
        if not flag[0] and v[0] == S[i]:
            flag[0] = True
            continue
        if not flag[1] and v[1] == S[i]and flag[0]:
            flag[1] = True
            continue
        if not flag[2] and v[2] == S[i] and flag[1]:
            flag[2] = True
            break
    if sum(flag) == 3:
        ans += 1
print(ans)
```
