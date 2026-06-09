---

# 📂 SCPC 2016 기출: 직사각형 포함 관계

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 위상 정렬(Topological Sort) 및 다이나믹 프로그래밍(DP)
* **시간 복잡도:** $O(N^2)$
* **공간 복잡도:** $O(N^2)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
from collections import deque
input = sys.stdin.readline

def maxNestedRectangles(rects):
    n = len(rects)
    # 1. 서로 "직접" 포함되는 관계 조사 (부분 순서 빌드)
    adj = [[] for _ in range(n)]
    indegree = [0] * n
    
    for i in range(n):
        for j in range(n):
            if i != j:
                # rect: (x1, y1, x2, y2) 구조일 때 i가 j를 포함하는지 검사
                if rects[i][0] <= rects[j][0] and rects[i][1] <= rects[j][1] and rects[i][2] >= rects[j][2] and rects[i][3] >= rects[j][3]:
                    adj[i].append(j)
                    indegree[j] += 1
                    
    # 2. 위상 정렬 및 최장 경로(가장 깊은 포함 관계) 탐색
    queue = deque()
    dp = [1] * n
    
    for i in range(n):
        if indegree[i] == 0:
            queue.append(i)
            
    while queue:
        curr = queue.popleft()
        for nxt in adj[curr]:
            if dp[nxt] < dp[curr] + 1:
                dp[nxt] = dp[curr] + 1
            indegree[nxt] -= 1
            if indegree[nxt] == 0:
                queue.append(nxt)
                
    return max(dp) if dp else 0
