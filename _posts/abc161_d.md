---
tags: ["ABC", "ABC161"]
---

# AtCoderBeginnerContest161 D 問題 400 点 「Lunlun Number」

<a href="https://atcoder.jp/contests/abc161/tasks/abc161_d" blank="_target">問題リンク</a>

## 問題概要

## 制約

## 解法

ある桁の数字 v に注目した時、v と差の絶対値が 1 になるような数字は v-1 と v+1 のみとなる。小さい順に見る必要があるので、桁を追加する場合は v-1 --> v + 1 の順に追加する。これを配列に入れて都度 pop していき、K 回目に pop した値を出力すれば良いのだが…
Python での実装の場合では通常の List よりも deque の方が先頭/末尾の値の取り出し速度が早いことが知られている([参考](https://dev.classmethod.jp/articles/python_list_vs_deque/))。

## お気持ち

実際にコンテスト中は List でやっててずっと TLE 食らってて脳みそが溶けました。

## AC コード

```python
# coding: utf-8
from collections import deque
K = int(input())
queue = [str(i) for i in range(1, 10)]
queue = deque(queue)
L = []
cnt = 0
while cnt < K:
    v = queue.popleft()
    # L.push(int(v))
    L.append(int(v))
    if v[-1] == "0":
        queue.append(v + v[-1])
        queue.append(v+"1")

    elif v[-1] == "9":
        queue.append(v + "8")
        queue.append(v + v[-1])
    else:
        # print("else", v)
        t = int(v[-1])
        queue.append(v+str(t-1))
        queue.append(v + v[-1])
        queue.append(v+str(t+1))
    cnt += 1
print(v)
```
