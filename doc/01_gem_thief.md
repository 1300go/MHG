# 📂 BOJ 1202: 보석 도둑

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 그리디(Greedy) 알고리즘, 우선순위 큐 (최대 힙)
* **시간 복잡도:** $O(N \log N + K \log K)$
* **공간 복잡도:** $O(N + K)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
import heapq

input = sys.stdin.readline

n, k = map(int, input().split())
gems = [list(map(int, input().split())) for _ in range(n)]
bags = [int(input()) for _ in range(k)]

gems.sort()
bags.sort()

result = 0
tmp = []

for bag in bags:
    while gems and bag >= gems[0][0]:
        heapq.heappush(tmp, -gems[0][1])
        heapq.heappop(gems)
    
    if tmp:
        result -= heapq.heappop(tmp)

print(result)
