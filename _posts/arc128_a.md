---
tags: ["ARC", "ARC128"]
---

# AtCoderRegularContest128 A 問題 400 点 「Gold and Silver」

<a href="hhttps://atcoder.jp/contests/arc128/tasks/arc128_a]" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

金を増やすためには，金 → 銀 → 金の手順を踏む必要がある。また，金の量は増加する場合は必ず単調増加であるため，金 → 銀に交換する$ A_x$と銀→金に交換する$ A_y$は$ A_x \gt A_y$の関係となる。
このような関係にあるx, yを見つけ，すべてで交換を行えば金は増えるが，それで必ず金の量が最大化するとは限らない。排他的論理和をとることで，$ A_x \gt A_y$の連続する区間の両端でのみ交換することで金の量を最大化することができる。

## お気持ち

## AC コード

```python
N = int(input())
A = list(map(int, input().split()))
ans = [0] * N
for i in range(N - 1):
    if A[i] > A[i + 1]:
        ans[i] ^= 1
        ans[i + 1] ^= 1
print(*ans)
```
