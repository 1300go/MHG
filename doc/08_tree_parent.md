---

### 📄 파일 8: `08_tree_parent.md` (BOJ 11725: 트리의 부모 찾기)
* **GitHub 파일 이름:** `08_tree_parent.md`

```markdown
# 📂 BOJ 11725: 트리의 부모 찾기

### 1. 알고리즘 및 복잡도 분석
* **알고리즘:** 깊이 우선 탐색(DFS) 트래버스 마킹
* **시간 복잡도:** $O(N)$ (정점 및 간선 1회 순회)
* **공간 복잡도:** $O(N)$ (트리 인접 그래프 및 재귀 호출 스택 공간)

### 2. 파이썬(Python) 정답 코드
```python
import sys
sys.setrecursionlimit(10**6)

def solve_11725():
    input = sys.stdin.readline
    N = int(input())
    graph = [[] for _ in range(N + 1)]
    for _ in range(N - 1):
        a, b = map(int, input().split())
        graph[a].append(b)
        graph[b].append(a)
        
    visited = [0] * (N + 1)
    def dfs(node):
        for i in graph[node]:
            if visited[i] == 0:
                visited[i] = node
                dfs(i)
    dfs(1)
    for x in range(2, N + 1):
        print(visited[x])

if __name__ == '__main__':
    solve_11725()
