---

### 📄 파일 15: `15_magician_shark.md` (BOJ 20056: 마법사 상어와 파이어볼)
* **GitHub 파일 이름:** `15_magician_shark.md`

```markdown
# 📂 BOJ 20056: 마법사 상어와 파이어볼

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 해시 테이블(Dictionary)을 활용한 좌표계 파이어볼 병합/분할 시뮬레이션
* **시간 복잡도:** $O(K \cdot (M + N^2))$ (이동 명령 수 $K$, 객체 수 $M$, 맵 크기 $N$)
* **공간 복잡도:** $O(M + N^2)$ (좌표 매핑용 딕셔너리 공간 비용)

### 2. 파이썬(Python) 정답 코드
```python
import sys

def solve_20056():
    input = sys.stdin.readline
    N, M, K = map(int, input().split())
    
    fireballs = []
    for _ in range(M):
        r, c, m, s, d = map(int, input().split())
        fireballs.append((r-1, c-1, m, s, d)) # 0-based 인덱스 조정
        
    # 0번 방향부터 7번 방향까지 순서대로 정의된 오프셋
    dx = [-1, -1, 0, 1, 1, 1, 0, -1]
    dy = [0, 1, 1, 1, 0, -1, -1, -1]
    
    for _ in range(K):
        grid = {}
        
        # 1. 모든 파이어볼 독립 이동 후 해당 위치 그룹핑
        for r, c, m, s, d in fireballs:
            nr = (r + s * dx[d]) % N
            nc = (c + s * dy[d]) % N
            if (nr, nc) not in grid:
                grid[(nr, nc)] = []
            grid[(nr, nc)].append((m, s, d))
            
        # 2. 이동 종료 후 원소 개수별 병합 및 4분할 연산
        next_fireballs = []
        for (r, c), balls in grid.items():
            if len(balls) == 1:
                next_fireballs.append((r, c, balls[0][0], balls[0][1], balls[0][2]))
                continue
                
            sum_m, sum_s = 0, 0
            count = len(balls)
            all_even, all_odd = True, True
            
            for m, s, d in balls:
                sum_m += m
                sum_s += s
                if d % 2 == 0: all_odd = False
                else: all_even = False
                
            next_m = sum_m // 5
            if next_m == 0: continue # 질량이 0이 된 파이어볼은 자동 소멸 스킵
            
            next_s = sum_s // count
            # 합쳐지는 방향 성분이 모두 짝수이거나 홀수이면 [0,2,4,6], 아니면 [1,3,5,7]
            next_dirs = (0, 2, 4, 6) if (all_even or all_odd) else (1, 3, 5, 7)
            
            for d in next_dirs:
                next_fireballs.append((r, c, next_m, next_s, d))
                
        fireballs = next_fireballs
        
    # 남아있는 모든 파이어볼의 최종 질량의 총합 구하기
    print(sum(f[2] for f in fireballs))

if __name__ == '__main__':
    solve_20056()
