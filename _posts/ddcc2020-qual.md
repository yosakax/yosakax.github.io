---
tags: ["ddcc"]
---

# DISCO presents ディスカバリーチャンネル コードコンテスト 2020 予選 C 問題 400 点 「Strawberry Cakes」

<a href="https://atcoder.jp/contests/ddcc2020-qual/tasks/ddcc2020_qual_c" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

以下の手順でグリッドがどのケーキに分類されるかを決定していく。

- あるイチゴの座標[$ (i, j)]から左側をそのイチゴのあるケーキの範囲とする。
- 上から順に，ある座標がまだどのケーキか決まってない場合は左側にのケーキとする
- 同様に，どのケーキか決まっていない場合は右側のケーキとする
- 左から順に，ある座標がまだどのケーキか決まっていない場合は上側のケーキとする
- 同様に，どのケーキか決まっていない場合は下側のケーキとする

以上の手順で，長方形のケーキをＫ個決定することができる

## お気持ち

## AC コード

```python
#coding: utf-8
H, W, K = map(int, input().split())
mat = [input() for _ in range(H)]
coord = []
for i in range(H):
    for j in range(W):
        if mat[i][j] == "#":
            coord.append([i, j])
ans = [[0 for _ in range(W)] for _ in range(H)]
for v in range(K):
    x, y = coord[v]
    # for i in range(x + 1):
    for j in range(y + 1):
        if ans[x][j] == 0:
            ans[x][j] = v + 1
for i in range(H):
    c = 0
    for j in range(W):
        if ans[i][j] != 0:
            c = ans[i][j]
        else:
            ans[i][j] = c
for i in range(H):
    c = 0
    for j in range(W-1, -1, -1):
        if ans[i][j] != 0:
            c = ans[i][j]
        else:
            ans[i][j] = c
for j in range(W):
    c = 0
    for i in range(H):
        if ans[i][j] != 0:
            c = ans[i][j]
        else:
            ans[i][j] = c
for j in range(W):
    c = 0
    for i in range(H-1, -1, -1):
        if ans[i][j] != 0:
            c = ans[i][j]
        else:
            ans[i][j] = c

for i in range(H):
    print(*ans[i])
```
