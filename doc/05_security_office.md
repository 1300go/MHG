---

### 📄 [5번] `05_security_office.md` (교재: 경비실 배치)
* **시간 복잡도:** $O(N \log N + N \log M)$ — 집의 좌표계를 정렬하는 시간 $O(N \log N)$과 양 끝집 사이의 스케일 $M$에 대한 파라메트릭 이분 탐색 루프당 $O(N)$ 판정 처리가 결합됩니다[cite: 8963, 8964].
* **공간 복잡도:** $O(N)$ — 집 위치 배열 공간입니다[cite: 8981].

```markdown
# 📂 교재 응용: 경비실 배치

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 매개 변수 탐색(Parametric Search) 및 이분 탐색 구간 판정
* **시간 복잡도:** $O(N \log N + N \log M)$ (단, M은 양 끝집 사이 거리)
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
input = sys.stdin.readline

def check(d, houses, k):
    count = 0
    i = 0
    n = len(houses)
    
    while i < n:
        count += 1
        pos = houses[i] + d
        while i < n and houses[i] <= pos + d:
            i += 1
    return count <= k

def solve():
    n, k = map(int, input().split())
    houses = [int(input()) for _ in range(n)]
    houses.sort()
    
    start = 0
    end = houses[-1] - houses[0]
    ans = end
    
    while start <= end:
        mid = (start + end) // 2
        if check(mid, houses, k):
            ans = mid
            end = mid - 1
        else:
            start = mid + 1
            
    print(ans)
