---
title: "AtCoderBeginnerContest229 E 問題 500 点「Graph_Destruction」"
date: 2022-07-02
layout: post
tags: ["ABC", "ABC229"]
---

# AtCoderBeginnerContest229 E 問題 500 点「Graph_Destruction」

<a href="https://atcoder.jp/contests/abc229/tasks/abc229_e" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

単純な解法として，ノードを一つひとつ削除したのちノードを計算する方法があるが，自明に TLE する。
そこで，逆順にノードを追加して行き，最終的に元のグラフを復元する方針で計算を行うことで，計算量が削減できる。各要素が連結かどうかだけわかれば良いので，UnionFind が使える。
連結なグラフは，ノードが追加される度に 1 増えるが，追加されたノードが既にあるグラフと連結である場合は逆に 1 減るため，これを記録すれば良い。

## お気持ち

## AC コード

```python
from collections import defaultdict


class UnionFind:
    def __init__(self, n):
        self.n = n
        self.parents = [-1] * n

    def find(self, x):
        if self.parents[x] < 0:
            return x
        else:
            self.parents[x] = self.find(self.parents[x])
            return self.parents[x]

    def union(self, x, y):
        x = self.find(x)
        y = self.find(y)

        if x == y:
            return

        if self.parents[x] > self.parents[y]:
            x, y = y, x

        self.parents[x] += self.parents[y]
        self.parents[y] = x

    def size(self, x):
        return -self.parents[self.find(x)]

    def same(self, x, y):
        return self.find(x) == self.find(y)

    def members(self, x):
        root = self.find(x)
        return [i for i in range(self.n) if self.find(i) == root]

    def roots(self):
        return [i for i, x in enumerate(self.parents) if x < 0]

    def group_count(self):
        return len(self.roots())

    def all_group_members(self):
        group_members = defaultdict(list)
        for member in range(self.n):
            group_members[self.find(member)].append(member)
        return group_members

    def __str__(self):
        return "\n".join(f"{r}: {m}" for r, m in self.all_group_members().items())


N, M = map(int, input().split())
uf = UnionFind(N)
d = defaultdict(set)
for _ in range(M):
    a, b = map(int, input().split())
    a -= 1
    b -= 1
    if a < b:
        d[a].add(b)
    else:
        d[b].add(a)
ans = [0]
gc = 0
for a in range(N - 1, 0, -1):
    gc += 1
    for b in d[a]:
        if not uf.same(a, b):
            gc -= 1
        uf.union(a, b)
    ans.append(gc)
print(*ans[::-1], sep="\n")
```
