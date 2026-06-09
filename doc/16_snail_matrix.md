---

### 📄 파일 16: `16_snail_matrix.md` (BOJ 1913: 달팽이)
* **GitHub 파일 이름:** `16_snail_matrix.md`

```markdown
# 📂 BOJ 1913: 달팽이 (Snail Matrix)

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 2차원 배열 격자 순회 및 경계 조건 회전 시뮬레이션
* **시간 복잡도:** $O(N^2)$ (정사각형의 전체 칸 수인 $N \times N$번의 순차 마킹 진행)
* **공간 복잡도:** $O(N^2)$ (정답 행렬을 담고 출력을 내보내기 위한 2차원 리스트 공간)

### 2. 파이썬(Python) 정답 코드
```python
import sys

def solve_1913():
    # (0,0)에서 N^2부터 거꾸로 감아들어가는 역방향 채우기가 가장 최적화하기 직관적입니다.
    input = sys.stdin.read
    data = input().split()
    if not data: return
    
    N = int(data[0])
    K = int(data[1])
    
    grid = [[0] * N for _ in range(N)]
    
    # 역방향 기준 이동 순서 오프셋: 아래(Down) -> 오른쪽(Right) -> 위(Up) -> 왼쪽(Left)
    dx = [1, 0, -1, 0]
    dy = [0, 1, 0, -1]
    
    x, y = 0, 0
    d = 0  # 초기 가이드 방향 하(Down) 설정
    ans_x, ans_y = 0, 0
    
    for val in range(N*N, 0, -1):
        grid[x][y] = val
        if val == K:
            ans_x, ans_y = x + 1, y + 1 # 1-based 인덱스로 변환 기록
            
        nx = x + dx[d]
        ny = y + dy[d]
        
        # 격자 가장자리를 벗어나거나, 이미 숫자가 채워진 칸을 만나면 90도 회전
        if nx < 0 or nx >= N or ny < 0 or ny >= N or grid[nx][ny] != 0:
            d = (d + 1) % 4
            nx = x + dx[d]
            ny = y + dy[d]
            
        x, y = nx, ny
        
    for row in grid:
        print(*row)
    print(f"{ans_x} {ans_y}")

if __name__ == '__main__':
    solve_1913()
