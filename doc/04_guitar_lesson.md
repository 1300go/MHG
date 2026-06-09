---

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
