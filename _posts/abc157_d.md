---
tags: ["ABC", "ABC157"]
---

# AtCoderBeginnerContest157 D 問題 400 点 「Friend Suggestions」

<a href="https://atcoder.jp/contests/abc157/tasks/abc157_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

それぞれが友達になる可能性のある人数を特定するために，UnionFind を使って森を作る。これにより，既に友達である関係とブロック関係を含んだ数を求めることができる。
次に，直接パスが通っている相手は既に友達なので，結合する際にそれぞれ 1 ずつ引いておく。最後に，ブロック関係の相手については，友達になる可能性がある場合のみ 1 引くことで，ブロック関係の友達をカウントしていないように処理する。

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


N, M, K = map(int, input().split())
uf = UnionFind(N)
ans = [0] * N
for _ in range(M):
    a, b = map(lambda x: int(x) - 1, input().split())
    uf.union(a, b)
    ans[a] -= 1
    ans[b] -= 1
for _ in range(K):
    c, d = map(lambda x: int(x) - 1, input().split())
    if uf.same(c, d):
        ans[c] -= 1
        ans[d] -= 1
all_member = uf.all_group_members()
for root in all_member.keys():
    members = set(all_member[root])
    for member in members:
        ans[member] += len(members) - 1
print(*ans)
```
