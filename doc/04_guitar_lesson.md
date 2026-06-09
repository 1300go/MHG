---

### 📄 [4번] `04_guitar_lesson.md` (BOJ 2343: 기타 레슨)
* **시간 복잡도:** $O(N \log(\text{sum} - \text{max}))$ — 모든 레슨 시간의 총합과 최대 레슨 시간 간격 사이에서 이분 탐색을 수행하며 [cite: 8591, 8592, 8593], 매 턴마다 $N$개의 강의를 정직하게 1회 완주 검사합니다[cite: 8597].
* **공간 복잡도:** $O(N)$ — 강의 분 단위 데이터를 담는 리스트 공간입니다[cite: 8590].

```markdown
# 📂 BOJ 2343: 기타 레슨

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 이분 탐색(Binary Search), 매개 변수 탐색(Parametric Search)
* **시간 복잡도:** $O(N \log(\text{sum} - \text{max}))$
* **공간 복잡도:** $O(N)$

### 2. 파이썬(Python) 정답 코드
```python
import sys

data = sys.stdin.read().split()
if data:
    n = int(data[0])
    m = int(data[1])
    lectures = [int(x) for x in data[2:n+2]]
    
    start = max(lectures)
    end = sum(lectures)
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
