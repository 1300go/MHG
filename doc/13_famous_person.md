---

### 📄 파일 13: `13_famous_person.md` (인터뷰 기출: 유명인 찾기)
* **GitHub 파일 이름:** `13_famous_person.md`

```markdown
# 📂 유명인 찾기 (Famous Person Problem)

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 소거법을 활용한 그리디 일차 탐색 및 완전 교차 검증
* **시간 복잡도:** $O(N)$ (후보 선별에 $N-1$번, 검증에 $2N$번 질의 수행)
* **공간 복잡도:** $O(1)$ (상수 포인터 변수 변환 외 추가 메모리 없음)

### 2. 파이썬(Python) 정답 코드
```python
# 교재 조건: i가 j를 아는지 판별하여 True/False를 리턴하는 가상의 빌트인 함수
def doesKnow(i, j):
    return True

def find_famous(n):
    candidate = 0  # 0번 사람을 최초의 유명인 후보로 임의 가정
    
    # 1단계: O(N) 질문을 통해 유명인이 절대 될 수 없는 자들을 소거해 나감
    for i in range(1, n):
        # 현재 후보가 i를 안다면, 유명인 정의(아무도 몰라야 함)에 의해 candidate 소거 -> i가 새 후보
        if doesKnow(candidate, i):
            candidate = i
        # 현재 후보가 i를 모른다면, 유명인 정의(모두가 알아야 함)에 의해 i가 소거 -> 기존 후보 유지
        else:
            pass
            
    # 2단계: 최종 살아남은 1인이 진짜 유명인이 맞는지 완벽하게 교차 검증 진행
    for i in range(n):
        if i == candidate: continue
        # 유명인이 다른 사람을 한 명이라도 알거나, 다른 사람이 유명인을 모른다면 유명인 없음(-1)
        if doesKnow(candidate, i) or not doesKnow(i, candidate):
            return -1
            
    return candidate
