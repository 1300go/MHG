### 📄 파일 3: `03_router_install.md` (BOJ 2110: 공유기 설치)
* **GitHub 파일 이름:** `03_router_install.md`

```markdown
# 📂 BOJ 2110: 공유기 설치

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 이분 탐색(Binary Search), 매개 변수 탐색(Parametric Search)
* **시간 복잡도:** $O(N \log N + N \log D)$ (정렬 시간 및 거리 $D$에 대한 탐색)
* **공간 복잡도:** $O(N)$ (집 좌표 배열)

### 2. 파이썬(Python) 정답 코드
```python
import sys

def solve_2110():
    input = sys.stdin.read
    data = input().split()
    if not data: return
        
    n, c = int(data[0]), int(data[1])
    arr = [int(x) for x in data[2:n+2]]
    arr.sort()
    
    s = 1
    e = arr[-1] - arr[0]
    ans = 0
    
    while s <= e:
        m = (s + e) // 2
        cnt = 1
        befor = arr[0]
        
        for i in range(1, n):
            if arr[i] - befor >= m:
                cnt += 1
                befor = arr[i]
                
        if cnt >= c:
            ans = m
            s = m + 1
        else:
            e = m - 1
    print(ans)

if __name__ == '__main__':
    solve_2110()
