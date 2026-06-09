---

### 📄 파일 2: `02_nested_rect.md` (SCPC 2016: 직사각형 포함 관계)
* **GitHub 파일 이름:** `02_nested_rect.md`

```markdown
# 📂 SCPC 2016 기출: 직사각형 포함 관계

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 다이나믹 프로그래밍(DP), 넓이 기준 정렬 (위상 정렬 효과)
* **시간 복잡도:** $O(N^2)$ (이중 루프를 통한 포함 관계 완전 탐색)
* **공간 복잡도:** $O(N)$ (DP 테이블 저장 배열)

### 2. 파이썬(Python) 정답 코드
```python
def maxNestedRectangles(rects):
    # 사각형들을 넓이 기준으로 오름차순 정렬
    rects.sort(key=lambda r: (r[2] - r[0]) * (r[3] - r[1]))
    n = len(rects)
    dp = [1] * n
    
    for i in range(n):
        for j in range(i):
            if (rects[i][0] <= rects[j][0] and
                rects[i][1] <= rects[j][1] and
                rects[i][2] >= rects[j][2] and
                rects[i][3] >= rects[j][3]):
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp) if dp else 0
