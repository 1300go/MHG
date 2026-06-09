---

### 📄 파일 9: `09_dual_pq.md` (BOJ 7662: 이중 우선순위 큐)
* **GitHub 파일 이름:** `09_dual_pq.md`

```markdown
# 📂 BOJ 7662: 이중 우선순위 큐

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 최대 힙 & 최소 힙 동기화 마킹 연산
* **시간 복잡도:** $O(N \log N)$ (원소의 독립 힙 푸시 및 팝 정렬 시간)
* **공간 복잡도:** $O(N)$ (힙 노드 및 삭제 추적 배열)

### 2. 파이썬(Python) 정답 코드
```python
import sys
import heapq

def solve_7662():
    input = sys.stdin.readline
    tc = int(input())
    for _ in range(tc):
        n = int(input())
        isDeleted = [False] * n
        minHeap, maxHeap = [], []
        for i in range(n):
            cmd, target = input().split()
            target = int(target)
            if cmd == 'I':
                heapq.heappush(minHeap, (target, i))
                heapq.heappush(maxHeap, (-target, i))
            else:
                if target == 1:
                    while maxHeap and isDeleted[maxHeap[0][1]]: heapq.heappop(maxHeap)
                    if maxHeap:
                        _, key = heapq.heappop(maxHeap)
                        isDeleted[key] = True
                else:
                    while minHeap and isDeleted[minHeap[0][1]]: heapq.heappop(minHeap)
                    if minHeap:
                        _, key = heapq.heappop(minHeap)
                        isDeleted[key] = True
        while maxHeap and isDeleted[maxHeap[0][1]]: heapq.heappop(maxHeap)
        while minHeap and isDeleted[minHeap[0][1]]: heapq.heappop(minHeap)
        if not minHeap: print("EMPTY")
        else: print(-maxHeap[0][0], minHeap[0][0])

if __name__ == '__main__':
    solve_7662()
