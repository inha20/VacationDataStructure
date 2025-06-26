# 그래프

<details>
    <summary>그래프의 방향</summary>
2차원 배열 형태로 표현된다. 한 쪽에서 다른 쪽으로 가는 방향만 1이면 방향 그래프, 다른 쪽에서 한 쪽으로 오는 길도 1이면 무방향 그래프이며 이 때 나머지는 모드 0이여야만 한다. 
</details>


<details>
    <summary>DFS, BFS</summary>
순서대로 깊이 우선 탐색, 너비 우선 탐색이다.
    
```python
def dfs(g, i, visited):
    visited[i] = True
    print(chr(ord('A')+i), end=' ')
    for j in range(len(g)):
        if g[i][j] == 1 and not visited[j]:
            dfs(g, j, visited)

def bfs(g, i, visited):
    queue = deque([i])
    visited[i] = 1
    # while len(queue) != 0:
    while queue:
        i = queue.popleft()
        print(chr(ord('A') + i), end=' ')
        for j in range(len(g)):
            if g[i][j] == 1 and not visited[j]:
                queue.append(j)
                visited[j] = 1
```

print(chr(ord('A')+i)은 숫자를 알파벳으로 치환해주는 역할을 한다. ASCII 관련 코드이다. <br>
dfs ; // i행을 먼저 방문 후(0번부터 시작), i행을 알파벳으로 바꿔 출력한다. 이후 추가적으로 연결된 j에게 dfs(g, j, visited)와 같이 재귀적으로 호출한다. 만약 j가 여러개일 경우 스택에 쌓이게 된다.
bfs ; // i행을 먼저 큐에 넣은 후 i를 알파벳으로 출력하고 나서 큐에 노드가 남아있는 동안 큐에 넣는다.
</details>
