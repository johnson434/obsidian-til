---
tags: 백준, Graph, DFS, BFS, Solved, 개념문제
---
[[Algorithm 문제풀이]] [[Algorithm Graph]] [[Algorithm BFS]] [[Algorithm DFS]]
**태그 잊지 않고 붙이세요**
- 출제 사이트
	- LeetCode
	- 백준
- 문제 종류
	- Array
	- String
	- Brute_Force
	- Binary_Search
	- Two_Pointers
	- DP
	- Graph
	- Implementation
	- Data_Structure
- 난이도
	- 리트코드
		- Easy
		- Medium
		- Hard
	- 백준
		- Gold1 ~ Gold5
		- Silver1 ~ Silver5
		- Bronze1 ~ Bronze5
- 혼자 풀었는지 여부
	- 풀었을 경우 : Solved
	- 다른 사람의 답안을 보거나 못 풀었을 경우 : Unsolved
[문제 링크](https://www.acmicpc.net/problem/1260)
# 제한사항
- `1 <= N(정점의 개수) <= 1000`
- `1 <= M(간선의 개수) <= 10,000`
- `v(시작점)`

# 문제 정리
1. DFS 탐색
2. BFS 탐색
3. 단, 정점 번호가 작은 자식 먼저 탐색한다.

# 접근 방법
전형적인 BFS DFS 문제 복습 겸 풀었다.

# 복잡도
시간복잡도 O(N^2) : 입력이 순서대로 주어지지 않아서 연결 리스트가 아닌 배열 형태로 구현했다. 모든 리스트를 탐색해서 방문이 가능한지 확인할 필요가 있으므로 O(N^2)

공간복잡도 O(N^2) : 배열 형태로 구현해서 O(N^2)
# 코드
``` cpp
#include "vector"  
#include "iostream"  
#include "queue"  
  
using namespace std;  
  
string dfs(const vector<vector<bool>>& map, vector<bool>& visited, int currentPoint) {  
    visited[currentPoint] = true;  
    string currentRoute;  
    currentRoute.append(to_string(currentPoint + 1));  
  
    for (int i = 0; i < map[currentPoint].size(); i++) {  
        if (!map[currentPoint][i] || visited[i]) {  
            continue;  
        }  
  
        visited[i] = true;  
        currentRoute.append(" ").append(dfs(map, visited, i));  
    }  
  
    return currentRoute;  
}  
  
string bfs(const vector<vector<bool>>& map, int currentPoint) {  
    vector<bool> visited(map.size(), false);  
    if (visited[currentPoint]) {  
        return "";  
    }  
  
    string answer = "";  
    queue<int> queue;  
    queue.push(currentPoint);  
  
    while (!queue.empty()) {  
        int node = queue.front();  
        queue.pop();  
        if (visited[node]) {  
            continue;  
        }  
        visited[node] = true;  
  
        answer.append(to_string(node + 1)).append(" ");  
        for (int i = 0; i < map[node].size(); i++) {  
            if (!map[node][i] || visited[i]) {  
                continue;  
            }  
  
            queue.push(i);  
        }  
    }  
  
    return answer;  
}  
  
int main() {  
    string answer;  
    cin.tie(nullptr);  
    cin.sync_with_stdio(false);  
    int N, M, V;  
    cin >> N >> M >> V;  
    vector<vector<bool>> map(N, vector<bool>(N, false));  
  
    for (int i = 0; i < M; i++) {  
        int start, end = 0;  
        cin >> start >> end;  
        map[start - 1][end - 1] = true;  
        map[end - 1][start - 1] = true;  
    }  
  
    vector<bool> visited(N,false);  
    answer.append(dfs(map, visited, V - 1));  
    answer.append("\n");  
    answer.append(bfs(map, V - 1));  
    cout << answer;  
  
    return 0;  
}
```

