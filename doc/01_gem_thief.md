# 📂 BOJ 1202: 보석 도둑

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 그리디(Greedy) 알고리즘, 우선순위 큐 (최대 힙)
* **시간 복잡도:** $O(N \log N + K \log K)$ (보석과 가방 정렬 및 힙 연산)
* **공간 복잡도:** $O(N + K)$ (보석 및 가방 데이터 저장 공간)

### 2. 파이썬(Python) 정답 코드
```python
import sys
import heapq

def solve_1202():
    input = sys.stdin.read
    data = input().split()
    if not data: return

    N, K = int(data[0]), int(data[1])
    jewels = []
    idx = 2
    for _ in range(N):
        jewels.append((int(data[idx]), int(data[idx+1])))
        idx += 2
        
    bags = []
    for _ in range(K):
        bags.append(int(data[idx]))
        idx += 1
        
    jewels.sort()
    bags.sort()
    
    max_heap = []
    total_value = 0
    jewel_idx = 0
    
    for bag in bags:
        while jewel_idx < N and jewels[jewel_idx][0] <= bag:
            heapq.heappush(max_heap, -jewels[jewel_idx][1])
            jewel_idx += 1
        if max_heap:
            total_value += -heapq.heappop(max_heap)
            
    print(total_value)

if __name__ == '__main__':
    solve_1202()
