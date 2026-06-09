---

### 📄 파일 11: `11_paper_stack.md` (BOJ 2643: 색종이 올려 놓기)
* **GitHub 파일 이름:** `11_paper_stack.md`

```markdown
# 📂 BOJ 2643: 색종이 올려 놓기

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 정렬 후 가장 긴 증가하는 부분 수열 (LIS) 응용 다이나믹 프로그래밍
* **시간 복잡도:** $O(N^2)$ (모든 색종이 쌍을 이중 루프로 비교 탐색)
* **공간 복잡도:** $O(N)$ (DP 테이블 저장용 1차원 배열)

### 2. 파이썬(Python) 정답 코드
```python
import sys

def solve_2643():
    input = sys.stdin.read
    data = input().split()
    if not data: return
    
    n = int(data[0])
    papers = []
    idx = 1
    for _ in range(n):
        w, h = int(data[idx]), int(data[idx+1])
        # 조건 2(90도 회전 허용)에 맞춰 항상 짧은 변을 0번에, 긴 변을 1번에 정렬
        papers.append((min(w, h), max(w, h)))
        idx += 2
        
    # 첫 번째 변 기준 오름차순, 같으면 두 번째 변 기준 오름차순 정렬
    papers.sort()
    
    # dp[i]: i번째 색종이를 맨 위에 올렸을 때 쌓을 수 있는 최대 색종이 장수
    dp = [1] * n
    
    for i in range(1, n):
        for j in range(i):
            # 정렬 상태이므로 두 번째 변(긴 변)의 길이 조건만 충족하면 j를 i 위에 포갤 수 있음
            if papers[i][1] >= papers[j][1]:
                dp[i] = max(dp[i], dp[j] + 1)
                
    print(max(dp))

if __name__ == '__main__':
    solve_2643()
