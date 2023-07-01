---
tags: ["ABC", "ABC241"]
---

# AtCoderBeginnerContest241 E 問題 500 点 「Putting Candies」

<a href="https://atcoder.jp/contests/abc242/tasks/abc242_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

一見簡単に見えたが，K がとても多いので単純に回すだけでは TLE になる。ここで，追加するアメのパターンはたかだか N 通りなので，K がどれだけ大きくともループする箇所ができる。ループを検知することで，ループの和を K // loop_num 回足せば良いので，計算量を大幅に削減することができる。ループ前の遷移が K よりも大きい場合があることと，K % loop_num 分だけループの中から値を足すこと に注意する。

## お気持ち

[他の人の解説](https://qiita.com/u2dayo/items/092fcdfb7902db6a9a72#e%E5%95%8F%E9%A1%8Cputting-candies)を見ると，どうやらダブリングという技術が使えるらしい。

## AC コード

```python
N, K = map(int, input().split())
A = list(map(int, input().split()))
tmp = 0
st = set()
lst = []
while tmp % N not in st:
    lst.append(tmp % N)
    st.add(tmp % N)
    tmp += A[tmp % N]
v = tmp
sidx = lst.index(tmp % N)
rep = len(lst) - sidx
ans = 0
for v in lst[:sidx]:
    ans += A[v]
    K -= 1
    if K == 0:
        break
tmp = 0
for v in lst[sidx:]:
    tmp += A[v]
ans += tmp * (K // rep)
for v in lst[sidx : sidx + K % rep]:
    ans += A[v]
print(ans)
```
