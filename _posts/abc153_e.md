---
tags: ["ABC", "ABC153"]
---

# AtCoderBeginnerContest153 E 問題 500 点 「Crested Ibis vs Monster」

<a href="https://atcoder.jp/contests/abc153/tasks/abc153_e" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

見るからに DP。とはいえそこまで複雑ではなく，$ dp[i] $はHPを$ i$削るまでに必要な魔力とすれば良い。
注意することとして，Hを超える場合は$ dp[H]$に必要な魔力を書いておくこと。

## お気持ち

## AC コード

```python
H, N = map(int, input().split())
AB = [list(map(int, input().split())) for _ in range(N)]
inf = int(1e9)
dp = [inf] * (H + 1)
dp[0] = 0
for i in range(N):
    a, b = AB[i]
    for j in range(H):
        dp[min(H, j + a)] = min(dp[min(H, j + a)], dp[j] + b)
print(dp[H])
```
