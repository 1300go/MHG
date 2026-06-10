---
# 📂 BOJ 20056: 마법사 상어와 파이어볼

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 해시 맵(Dictionary)을 통한 대규모 좌표 객체 이동/병합 시뮬레이션
* **시간 복잡도:** $O(K \cdot (M + N^2))$
* **공간 복잡도:** $O(M + N^2)$

### 2. 파이썬(Python) 정답 코드
```python
import sys
input = sys.stdin.readline

n, m, k = map(int, input().split())
fireballs = []
for _ in range(m):
    r, c, m_val, s, d = map(int, input().split())
    fireballs.append((r-1, c-1, m_val, s, d))

dx = [-1, -1, 0, 1, 1, 1, 0, -1]
dy = [0, 1, 1, 1, 0, -1, -1, -1]

for _ in range(k):
    grid = {}
    for r, c, m_val, s, d in fireballs:
        nr = (r + dx[d] * s) % n
        nc = (c + dy[d] * s) % n
        if (nr, nc) not in grid:
            grid[(nr, nc)] = []
        grid[(nr, nc)].append((m_val, s, d))
        
    next_fireballs = []
    for (r, c), balls in grid.items():
        if len(balls) >= 2:
            sum_m, sum_s = 0, 0
            odd_cnt, even_cnt = 0, 0
            for m_val, s, d in balls:
                sum_m += m_val
                sum_s += s
                if d % 2 == 0: even_cnt += 1
                else: odd_cnt += 1
                
            nm = sum_m // 5
            ns = sum_s // len(balls)
            if nm == 0:
                continue
                
            ndirs = [0, 2, 4, 6] if even_cnt == len(balls) or odd_cnt == len(balls) else [1, 3, 5, 7]
            for nd in ndirs:
                next_fireballs.append((r, c, nm, ns, nd))
        else:
            next_fireballs.append((r, c, balls[0][0], balls[0][1], balls[0][2]))
            
    fireballs = next_fireballs

print(sum(f[2] for f in fireballs))
