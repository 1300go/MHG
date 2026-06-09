---

# 📂 교재 응용: Subset Sum (k=2)

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 정렬 및 투 포인터(Two Pointers) 탐색
* **시간 복잡도:** $O(N \log N)$
* **공간 복잡도:** $O(1)$


### 2. 파이썬(Python) 정답 코드
```python
import sys
input = sys.stdin.readline

def subsetSumK2(arr, s):
    arr.sort()
    left = 0
    right = len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == s:
            return True, (arr[left], arr[right])
        elif current_sum < s:
            left += 1
        else:
            right -= 1
            
    return False, None
