---
tags: ["ABC", "ABC124"]
---

# AtCoderBeginnerContest124 D 問題 400 点 「Handstand」

<a href="https://atcoder.jp/contests/abc124/tasks/abc124_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

1 をまたぐように反転することは無駄。0 が連続している個数を見て，K 個以上選択して最大になる所を探す。まず，連続する 0 か 1 の数を記録する配列を用意する。これにより，偶数番目の要素は連続する 1 の個数，奇数番目の要素は連続する 0 の個数を表す。間に 0 の列を K 個含んだ場合の最大値を求めていく。いつも通り，[けんちょんさんの記事](https://drken1215.hatenablog.com/entry/2019/04/14/222900) が非常に参考になる。というかこれがあればこんなもの書く必要ないのでは…

## お気持ち

## AC コード

```python
#coding: utf-8
N, K = map(int, input().split())
S = input()
nums = []
if S[0] == "0":
    nums.append(0)
i = 0
while i < len(S):
    j = i
    while j < N and S[j] == S[i]:
        j += 1
    nums.append(j - i)
    i = j
if S[-1] == "0":
    nums.append(0)
accum = [0]
for i in range(len(nums)):
    accum.append(accum[-1] + nums[i])

ans = 0
for i in range(0, len(accum), 2):
    r = min(len(accum)-1, i + 2 * K + 1)
    ans = max(ans, accum[r] - accum[i])
print(ans)
```
