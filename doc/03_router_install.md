---

# 📂 BOJ 2110: 공유기 설치

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 이분 탐색(Binary Search), 매개 변수 탐색(Parametric Search)
* **시간 복잡도:** $O(N \log N + N \log D)$ (단, D는 좌표의 최대 범위)
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
input = sys.stdin.readline

n, c = map(int, input().split())
arr = [int(input()) for _ in range(n)]
arr.sort()

s = 1
e = 1000000000
ans = 0

while s <= e:
    m = (s + e) // 2
    cnt = 1
    before = arr[0]
    
    for i in range(1, n):
        if arr[i] - before >= m:
            cnt += 1
            before = arr[i]
            
    if cnt >= c:
        ans = m
        s = m + 1
    else:
        e = m - 1

print(ans)
