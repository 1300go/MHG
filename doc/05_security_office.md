---

### 📄 파일 5: `05_security_office.md` (교재: 경비실 배치)
* **GitHub 파일 이름:** `05_security_office.md`

```markdown
# 📂 교재 응용: 경비실 배치

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 매개 변수 탐색(Parametric Search) 및 그리디 배치 판정
* **시간 복잡도:** $O(N \log N + N \log M)$ (집 정렬 및 최대 거리 $M$ 탐색)
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
def can_cover(houses, n, k, max_dist):
    count = 1
    limit = houses[0] + max_dist * 2
    for i in range(1, n):
        if houses[i] > limit:
            count += 1
            limit = houses[i] + max_dist * 2
    return count <= k

def solve_security(n, k, houses):
    houses.sort()
    low, high = 0, houses[-1] - houses[0]
    answer = high
    while low <= high:
        mid = (low + high) // 2
        if can_cover(houses, n, k, mid):
            answer = mid
            high = mid - 1
        else:
            low = mid + 1
    return answer
