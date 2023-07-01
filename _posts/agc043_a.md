---
tags: ["AGC", "AGC043"]
---

# AtCoderGrandContest043 A 問題 400 点 「Range Flip Find Route」

<a href="https://atcoder.jp/contests/agc043/tasks/agc043_a" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

ある経路を考えるとき，「.」 -->「 # 」となる時のみ値が増えるような DP を考える。#-->#の時はその範囲を丸ごと反転させることで一回で済む

## お気持ち

## AC コード

```python
#coding: utf-8
from collections import deque
H, W = map(int, input().split())
mat = [input() for _ in range(H)]
V = [[10**4 for _ in range(W)] for _ in range(H)]
# V = [[0 for _ in range(W)] for _ in range(H)]
visited = [[False for _ in range(W)] for _ in range(H)]
queue = deque()
queue.append([0, 0])
dx = [1, 0]
dy = [0, 1]
visited[0][0] = True
if mat[0][0] == "#":
    V[0][0] = 1
else:
    V[0][0] = 0
dx = [0, 1]
dy = [1, 0]
for i in range(H):
    for j in range(W):
        for d in range(2):
            ni = i + dx[d]
            nj = j + dy[d]
            if ni >= H or nj >= W:
                continue
            add = 0
            if mat[ni][nj] == "#" and mat[i][j] == ".":
                add = 1
            V[ni][nj] = min(V[ni][nj], V[i][j] + add)
print(V[H-1][W-1])
```
