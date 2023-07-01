---
tags: ["ABC", "ABC077"]
---

# AtCoderBeginnerContest077 C 問題 300 点 「Snuke Festival」

<a href="https://atcoder.jp/contests/abc077/tasks/abc077_c" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

なんとなく$ A_i$が挿入できる個所を二分探索で求めて，そこからまた$ B_j$の入るところを二分探索で…的な解放を考えたが，オーダが$ O(N^2)$より大きくなりそうだったのでこれはできないと断念。
そこで，真ん中の$ B_j$についてだけ考える。$ B_j$よりも真に小さいAの位置$ i$を二分探索で探し，また真に大きいCの位置$ k$を二分探索で同様に探す。これによって，$ B_j$を用いた場合の組合せは $ i \times (N - k)$と書くことができる。以上より，計算量は$ O(N \times 2 \log N)$となる

## お気持ち

## AC コード

```python
#coding: utf-8
from bisect import bisect_left, bisect_right

N = int(input())
A = list(map(int, input().split()))
B = list(map(int, input().split()))
C = list(map(int, input().split()))
A.sort()
B.sort()
C.sort()
ans = 0
for j in range(N):
    i = bisect_left(A, B[j])
    k = bisect_right(C, B[j])
    ans += i * (N - k)
print(ans)
```
