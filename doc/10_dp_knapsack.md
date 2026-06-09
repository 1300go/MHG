---

### 📄 파일 10: `10_dp_knapsack.md` (교재: 0-1 배낭 문제)
* **GitHub 파일 이름:** `10_dp_knapsack.md`

```markdown
# 📂 교재 예제: 0-1 Knapsack 배낭 문제

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 다이나믹 프로그래밍(DP) 및 배수 단위 가로축 최적화
* **시간 복잡도:** $O(N \cdot \frac{C}{\text{step}})$ (물건 수 $N$, 총용량 $C$, 압축 단위 $\text{step}=5$)
* **공간 복잡도:** $O(N \cdot \frac{C}{\text{step}})$

### 2. 파이썬(Python) 정답 코드
```python
def solve_knapsack():
    items = [None, {"weight": 5, "value": 50}, {"weight": 20, "value": 140}, {"weight": 10, "value": 60}]
    max_C, step = 30, 5
    columns = [w for w in range(0, max_C + 1, step)]
    D = [[0] * len(columns) for _ in range(len(items))]
    
    for i in range(1, len(items)):
        W_i, V_i = items[i]["weight"], items[i]["value"]
        for c_idx, C in enumerate(columns):
            if C == 0: continue
            if W_i > C:
                D[i][c_idx] = D[i-1][c_idx]
            else:
                prev_c_idx = columns.index(C - W_i)
                D[i][c_idx] = max(D[i-1][c_idx], D[i-1][prev_c_idx] + V_i)
    print("최대 가치:", D[-1][-1])

if __name__ == '__main__':
    solve_knapsack()
