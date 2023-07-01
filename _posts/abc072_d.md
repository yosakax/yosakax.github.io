---
tags: ["ABC", "ABC072"]
---

# AtCoderBeginnerContest072 D 問題 400 点 「Derangement」

<a href="https://atcoder.jp/contests/abc072/tasks/abc072_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

条件を満たしている要素と満たしていない要素が隣り合っていた時，スワップしていくことを前から順に行うことでどちらも条件を満たすことができる。並びが逆でも，どちらも条件を満たしていない場合でも同じことをすればすべての要素で条件を満たせる。

## お気持ち

すごいな～～～思いつかんかった。

## AC コード

```python
# coding: utf-8
N = int(input())
P = list(map(int, input().split()))
ans = 0
for i in range(N-1):
    if i + 1 == P[i]:
        P[i], P[i+1] = P[i+1], P[i]
        ans += 1
if P[N-1] == N:
    ans += 1

print(ans)
```
