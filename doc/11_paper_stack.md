---
# 📂 BOJ 2643: 색종이 올려 놓기

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 정렬 후 가장 긴 증가하는 부분 수열 (LIS) 응용 다이나믹 프로그래밍
* **시간 복잡도:** $O(N^2)$
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
input = sys.stdin.readline

n = int(input())
papers = []
for _ in range(n):
    a, b = map(int, input().split())
    papers.append((min(a, b), max(a, b)))

papers.sort()

dp = [1] * n
for i in range(n):
    for j in range(i):
        if papers[j][0] <= papers[i][0] and papers[j][1] <= papers[i][1]:
            dp[i] = max(dp[i], dp[j] + 1)

print(max(dp))
