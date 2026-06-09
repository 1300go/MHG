---

### 📄 파일 14: `14_dice_rolling.md` (BOJ 14499: 주사위 굴리기)
* **GitHub 파일 이름:** `14_dice_rolling.md`

```markdown
# 📂 BOJ 14499: 주사위 굴리기

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 시뮬레이션 및 3차원 입체 도형 상태 회전 구현
* **시간 복잡도:** $O(K)$ (명령어 개수 $K$번만큼 정직하게 루프 실행)
* **공간 복잡도:** $O(N \cdot M)$ (지도의 2차원 격자 정보를 저장하는 보드 메모리 공간)

### 2. 파이썬(Python) 정답 코드
```python
import sys

def solve_14499():
    input = sys.stdin.readline
    n, m, x, y, k = map(int, input().split())
    
    board = [list(map(int, input().split())) for _ in range(n)]
    commands = list(map(int, input().split()))
    
    # 주사위의 각 면 상태 인덱스 정의: [위(0), 아래(1), 앞(2), 뒤(3), 왼쪽(4), 오른쪽(5)]
    dice = [0, 0, 0, 0, 0, 0]
    
    # 1: 동쪽, 2: 서쪽, 3: 북쪽, 4: 남쪽 방향 오프셋 (0번은 dummy)
    dx = [0, 0, 0, -1, 1]
    dy = [0, 1, -1, 0, 0]
    
    for cmd in commands:
        nx = x + dx[cmd]
        ny = y + dy[cmd]
        
        # 지도의 바깥 경계선을 벗어나는 유효하지 않은 명령은 즉시 무시
        if nx < 0 or nx >= n or ny < 0 or ny >= m:
            continue
            
        x, y = nx, ny
        top, bottom, front, back, left, right = dice[0], dice[1], dice[2], dice[3], dice[4], dice[5]
        
        # 굴리는 방향에 맞춰 주사위 전개도 변면 스와핑 진행
        if cmd == 1:    # 동쪽
            dice = [left, right, front, back, bottom, top]
        elif cmd == 2:  # 서쪽
            dice = [right, left, front, back, top, bottom]
        elif cmd == 3:  # 북쪽
            dice = [front, back, bottom, top, left, right]
        elif cmd == 4:  # 남쪽
            dice = [back, front, top, bottom, left, right]
            
        # 이동한 지도 칸의 숫자에 따른 조건식 복사 매핑
        if board[x][y] == 0:
            board[x][y] = dice[1]  # 주사위 바닥면 값을 지도 칸에 복사
        else:
            dice[1] = board[x][y]  # 지도 칸의 값을 주사위 바닥에 복사
            board[x][y] = 0        # 해당 지도 칸은 0으로 리셋
            
        print(dice[0])  # 굴릴 때마다 주사위의 상단 윗면 값 출력

if __name__ == '__main__':
    solve_14499()
