---

### 📄 파일 4: `04_guitar_lesson.md` (BOJ 2343: 기타 레슨)
* **GitHub 파일 이름:** `04_guitar_lesson.md`

```markdown
# 📂 BOJ 2343: 기타 레슨

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 이분 탐색(Binary Search), 매개 변수 탐색(Parametric Search)
* **시간 복잡도:** $O(N \log(\text{sum} - \text{max}))$ (전체 강의 길이 범위 탐색)
* **공간 복잡도:** $O(N)$ (강의 수 배열)

### 2. 파이썬(Python) 정답 코드
```python
import sys

def solve_2343():
    data = sys.stdin.read().split()
    if not data: return
    n, m = int(data[0]), int(data[1])
    lectures = [int(x) for x in data[2:n+2]]
    
    start, end = max(lectures), sum(lectures)
    result = end
    
    while start <= end:
        mid = (start + end) // 2
        count = 1
        current_sum = 0
        for lecture in lectures:
            if current_sum + lecture > mid:
                count += 1
                current_sum = lecture
            else:
                current_sum += lecture
        if count <= m:
            result = mid
            end = mid - 1
        else:
            start = mid + 1
    print(result)

if __name__ == '__main__':
    solve_2343()
