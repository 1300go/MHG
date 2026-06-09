---

### 📄 [6번] `06_subset_sum.md` (교재: Subset Sum k=2)
* **시간 복잡도:** $O(N \log N)$ — $n$개의 숫자를 기본 오름차순으로 정렬하는 데 가장 많은 계산 시간($O(N \log N)$)을 소모하며, 정렬된 배열 위에서 투 포인터(양 끝단 좁히기) 탐색은 단 $O(N)$ 시간에 종료됩니다.
* **공간 복잡도:** $O(1)$ 또는 $O(N)$ — 제자리 정렬 알고리즘 선택에 따라 변동하는 내부 데이터 저장 공간입니다.

```markdown
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
