---
# 📂 SCPC 2015 기출: 개구리 뛰기

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 그리디(Greedy) 알고리즘 (사거리 내 가장 먼 선택지 고르기)
* **시간 복잡도:** $O(N)$
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
input = sys.stdin.readline

def solve_frog():
    n = int(input())
    stones = list(map(int, input().split()))
    k = int(input())
    
    ans = 0
    curr_idx = 0
    possible = True
    
    while curr_idx < n - 1:
        nxt_idx = curr_idx
        while nxt_idx + 1 < n and stones[nxt_idx + 1] - stones[curr_idx] <= k:
            nxt_idx += 1
            
        if nxt_idx == curr_idx:
            possible = False
            break
            
        curr_idx = nxt_idx
        ans += 1
        
    print(ans if possible else -1)
