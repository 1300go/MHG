---
# 📂 교재 응용: 0-1 Knapsack (배낭 문제 DP)

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 다이나믹 프로그래밍 (Dynamic Programming, DP)
* **시간 복잡도:** $O(N \cdot C)$ (N은 물건 개수, C는 최대 허용 무게)
* **공간 복잡도:** $O(N \cdot C)$
### 2. 파이썬(Python) 정답 코드
```python
import sys
input = sys.stdin.readline

def knapsack_dp():
    n, C = map(int, input().split())
    
    items = [(0, 0)]
    for _ in range(n):
        wi, vi = map(int, input().split())
        items.append((vi, wi))
    
    D = [[0] * (C + 1) for _ in range(n + 1)]
    
    for i in range(1, n + 1):
        vi, wi = items[i]
        for w in range(1, C + 1):
            if wi > w:
                D[i][w] = D[i-1][w]
            else:
                D[i][w] = max(D[i-1][w], D[i-1][w-wi] + vi)
                
    print(D[n][C])

if __name__ == "__main__":
    knapsack_dp()
