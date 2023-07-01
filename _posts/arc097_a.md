---
tags: ["ARC", "ARC097"]
---

# AtCoderRegularContest097 A 問題 300 点 「K-th Substring」

<a href="https://atcoder.jp/contests/arc097/tasks/arc097_a" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

K が異常に小さいことに注目する。K 番目の文字列はどんなに長くても K 文字であることがわかるため，1 文字目から最大 K 文字目までの文字列を調べてソートすることで行ける。なんだかんだ文字列を格納した配列が大きくなるのでは？と思うが，最大でも$ NK$個の文字列なので，制約の範囲内だと大した事ない。

## お気持ち

## AC コード

```python
#coding: utf-8
from collections import OrderedDict, deque
from heapq import heapify, heappop, heappush
S = input()
K = int(input())
od = OrderedDict()
queue = []
for i in range(len(S)):
    for j in range(1, K + 1):
        if S[i:i+j] == "":
            continue
        if S[i:i+j] not in od.keys():
            od[S[i:i+j]] = 1
            queue.append(S[i:i+j])
queue.sort()
print(queue[K-1])
```
