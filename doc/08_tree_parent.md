---
# 📂 BOJ 11725: 트리의 부모 찾기

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 너비 우선 탐색(BFS) 또는 깊이 우선 탐색(DFS)
* **시간 복잡도:** $O(N)$
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
from collections import deque
input = sys.stdin.readline

n = int(input())
adj = [[] for _ in range(n + 1)]
parent = [0] * (n + 1)

for _ in range(n - 1):
    u, v = map(int, input().split())
    adj[u].append(v)
    adj[v].append(u)

queue = deque([1])
while queue:
    curr = queue.popleft()
    for nxt in adj[curr]:
        if parent[nxt] == 0 and nxt != 1:
            parent[nxt] = curr
            queue.append(nxt)

for i in range(2, n + 1):
    print(parent[i])
