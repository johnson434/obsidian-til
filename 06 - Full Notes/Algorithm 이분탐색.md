---
기술:
  - 알고리즘
---
[[Algorithm Notion]] [[Algorithm Binary Search]]
# 관련 블로그

> [!info] 이분 탐색(Binary Search) 헷갈리지 않게 구현하기  
> 이분 탐색은 off-by-one error가 발생하기 쉬워서 늘 헷갈립니다.  
> [https://www.acmicpc.net/blog/view/109](https://www.acmicpc.net/blog/view/109)  

**시간복잡도** : logN

```Python
import bisect
array = [1, 2, 3, 3, 3, 4, 5, 6, 7, 8, 9, 10]

print(bisect.bisect_left(array, 3))
print(bisect.bisect_right(array, 3))
```