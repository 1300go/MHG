---
# 📂 BOJ 7662: 이중 우선순위 큐

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 이중 우선순위 큐 (최대 힙 & 최소 힙 상태 동기화 트릭)
* **시간 복잡도:** $O(N \log N)$
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
import heapq
input = sys.stdin.readline

tc = int(input())

for _ in range(tc):
    n = int(input())
    isDeleted = [False] * n
    minHeap = []
    maxHeap = []
    
    for i in range(n):
        cmd, target = input().rstrip().split()
        target = int(target)
        
        if cmd == 'I':
            heapq.heappush(minHeap, (target, i))
            heapq.heappush(maxHeap, (-target, i))
        else:
            if target == 1:
                while maxHeap and isDeleted[maxHeap[0][1]]:
                    heapq.heappop(maxHeap)
                if maxHeap:
                    number, key = heapq.heappop(maxHeap)
                    isDeleted[key] = True
            else:
                while minHeap and isDeleted[minHeap[0][1]]:
                    heapq.heappop(minHeap)
                if minHeap:
                    number, key = heapq.heappop(minHeap)
                    isDeleted[key] = True
                    
    while maxHeap and isDeleted[maxHeap[0][1]]:
        heapq.heappop(maxHeap)
    while minHeap and isDeleted[minHeap[0][1]]:
        heapq.heappop(minHeap)
        
    if maxHeap and minHeap:
        print(-maxHeap[0][0], minHeap[0][0])
    else:
        print("EMPTY")
