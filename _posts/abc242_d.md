---
tags: ["ABC", "ABC242"]
---

# AtCoderBeginnerContest242 問題 400 点 「ABC Transform」

<a href="https://atcoder.jp/contests/abc242/tasks/abc242_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

0-indexed で話をする
まず，文字列を生成することは不可能。そこで，文字列がどのように遷移していくかを考える。A, B, C -> 0, 1, 2 とすると，各文字列は以下のように遷移する。

- A -> BC(0 -> 12)
- B -> CA(1 -> 20)
- C -> AB(2 -> 01)

ここから，遷移先の 1 文字目は元の文字+1, 2 文字目は+2 された modint になることがわかる。したがって，ある文字が t 段目の k 文字目である場合，k が偶数の場合は k より 1 つ進んだものであり，奇数の場合は[$ S[k]]より 2 つ進んだものであることがわかる。
また，t 段目の k 番目の文字は t-1 段目の k//2 番目の文字から作られている。

以上の 2 つの考察より，以下の漸化式が成り立つ。f(t,k)が t 段目の文字列の k 番目のインデックスを返す関数と定義すると，

$ f(t, k) = f(t-1, k//2) + 1 (k \% 2 == 0)$
$ f(t, k) = f(t-1, k//2) + 2(k \% 2 == 1)$

これは再帰関数になるので，最終的には f(0, k)か f(t, 0)に行きつく。それぞれについての処理を説明する。

- t == 0, k > 0 の場合
  0 段目の k 番目の文字が t 段目の k 番目の文字の祖先なので，[$ S[k]]を返す

- t > 0, k == 0 の場合
  k == 0 ならば[$ S[0]]が祖先であることは確定なので，[$ S[0]]に残りの t を足した値を返す。

## お気持ち

$ O(\min(t, \log_2(K)))$

## AC コード

解説 AC

```python
import sys

sys.setrecursionlimit(10**7)
S = input()
Q = int(input())
ABC = "ABC"


def dfs(t, k):
    if t == 0:
        return ABC.index(S[k])
    if k == 0:
        return ABC.index(S[0]) + t
    if k % 2 == 0:
        return dfs(t - 1, k // 2) + 1
    else:
        return dfs(t - 1, k // 2) + 2


for _ in range(Q):
    t, k = map(int, input().split())
    print(ABC[dfs(t, k - 1) % 3])
```
