---
tags: 백준, Easy
---
[[Algorithm 문제풀이]]
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
[문제 링크](https://www.acmicpc.net/problem/8958)
# 문제 정리
푸셈
# 복잡도
- `시간복잡도 : O(N)`
- `공간복잡도 : O(1)`

# 코드
``` cpp
#include "iostream"  
#include "string"  
  
using namespace std;  
  
int main() {  
    string answer;  
    int cntOfProblemSet;  
    cin >> cntOfProblemSet;  
  
    while (cntOfProblemSet-- > 0) {  
        string marks;  
        cin >> marks;  
  
        int cntOfCorrectedAnswer = 0;  
        int cntOfContinuousO = 0;  
        for (const char &mark : marks) {  
            if (mark == 'O') {  
                cntOfContinuousO++;  
            } else {  
                cntOfContinuousO = 0;  
            }  
            cntOfCorrectedAnswer += cntOfContinuousO;  
        }  
        answer.append(to_string(cntOfCorrectedAnswer));  
        answer.append("\n");  
    }  
  
    cout << answer;  
    return 0;  
}
```

