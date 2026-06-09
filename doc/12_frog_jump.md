---

### 📄 파일 12: `12_frog_jump.md` (SCPC 2015: 개구리 뛰기)
* **GitHub 파일 이름:** `12_frog_jump.md`

```markdown
# 📂 SCPC 2015 기출: 개구리 뛰기

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 그리디(Greedy) 알고리즘 (매 순간 갈 수 있는 가장 먼 돌을 선택)
* **시간 복잡도:** $O(N)$ (돌의 개수만큼 단 한 번 선형 순회 탐색)
* **공간 복잡도:** $O(N)$ (입력된 돌의 좌표 리스트 저장 공간)

### 2. 파이썬(Python) 정답 코드
```python
def frog_jump(stones, K):
    pos = 0     # 개구리의 현재 돌 좌표 값 (0번 위치 고정 시작)
    jumps = 0   # 총 점프 횟수
    i = 1       # 탐색 기준이 되는 돌의 인덱스 (1번 돌부터 출발)
    
    while i < len(stones):
        # 이번에 확인하는 돌이 현재 위치에서 점프 사거리(K) 이내인 경우
        if stones[i] <= pos + K:
            # 해당 돌이 마지막 목적지라면 점프 횟수를 최종 반영하고 즉시 종료
            if i == len(stones) - 1:
                return jumps + 1
            i += 1  # 사거리 이내라면 더 멀리 있는 돌이 있는지 인덱스 점증 확장
        else:
            # 직전 돌마저 개구리의 현재 위치와 같다면, 두 돌 사이 거리가 K를 초과해 도달 불가능함
            if stones[i-1] == pos:
                return -1
            
            # 사거리를 벗어나기 직전 단계의 가장 멀었던 돌(i-1)로 개구리의 실질적 위치 확정
            pos = stones[i-1]
            jumps += 1
            # 인덱스 i는 현재 돌 위치에서 다시 새롭게 사거리를 재야 하므로 i를 늘리지 않음
            
    return jumps

if __name__ == '__main__':
    # 교재 예시 데이터 테스트
    sample_stones = [0, 1, 2, 5, 7, 9, 10, 12, 15]
    print(frog_jump(sample_stones, 4))  # 출력: 5
