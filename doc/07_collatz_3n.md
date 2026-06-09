---

### 📄 파일 7: `07_collatz_3n.md` (SCPC 기출: 3n + 1)
* **GitHub 파일 이름:** `07_collatz_3n.md`

```markdown
# 📂 SCPC 기출: 3n + 1

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 너비 우선 탐색(BFS) 기반 역방향 상태 공간 탐색
* **시간 복잡도:** $O(2^K)$ (중복 차단으로 실제 연산 범위는 극소화)
* **공간 복잡도:** $O(2^K)$

### 2. 파이썬(Python) 정답 코드
```python
def solve_3n_plus_1(K):
    current_set = {1}
    for _ in range(K):
        next_set = set()
        for x in current_set:
            next_set.add(x * 2)
            if (x - 1) % 3 == 0:
                prev_odd = (x - 1) // 3
                if prev_odd > 1 and prev_odd % 2 != 0:
                    next_set.add(prev_odd)
        current_set = next_set
    print(f"가장 큰수: {max(current_set)}")
    print(f"가장 작은 수: {min(current_set)}")
