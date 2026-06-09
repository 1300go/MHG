---

### 📄 파일 6: `06_subset_sum.md` (교재: Subset Sum)
* **GitHub 파일 이름:** `06_subset_sum.md`

```markdown
# 📂 교재 응용: Subset Sum (k=3)

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 다이나믹 프로그래밍(DP) (3차원 테이블 압축 기법)
* **시간 복잡도:** $O(N \cdot K \cdot S)$ (원소 수, 목표 개수, 목표 합 조합)
* **공간 복잡도:** $O(K \cdot S)$

### 2. 파이썬(Python) 정답 코드
```python
def subset_sum(A, S, K_target):
    dp = [[False] * (K_target + 1) for _ in range(S + 1)]
    dp[0][0] = True
    for num in A:
        for j in range(S, num - 1, -1):
            for k in range(K_target, 0, -1):
                if dp[j - num][k - 1]:
                    dp[j][k] = True
    return dp[S][K_target]
