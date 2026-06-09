---
# 📂 유명인 찾기 (Famous Person Problem)

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 제거법을 활용한 그리디 선형 포인터 축소 및 완전 교차 검증
* **시간 복잡도:** $O(N)$
* **공간 복잡도:** $O(1)$

### 2. 파이썬(Python) 정답 코드
```python
def doesKnow(i, j):
    pass 

def findFamous(n):
    candidate = 0
    for i in range(1, n):
        if doesKnow(candidate, i):
            candidate = i
            
    for i in range(n):
        if i != candidate:
            if doesKnow(candidate, i) or not doesKnow(i, candidate):
                return -1
    return candidate
