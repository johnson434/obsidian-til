---
기술:
  - 터미널
---
[[Linux]] [[Terminal]]
```JavaScript
# exec를 사용할 때 터미널에서 자주 보이는 --
# 왜 쓰냐? 옵션을 나누고 싶을 때 사용한다
kubectl exec -it nginx-pod ls /run
# 위에 커맨드는 ls /run을 nginx-pod 컨테이너에서 실행하라는 말이다.
# 그런데 ls에 l옵션을 줘서 리스트로 받으면 어떻게 될까?
kubectl exec -it nginx-pod ls -l /run
# 위에 명령어는 -l 옵션을 exec의 옵션으로 입식하고 문제가 발생해
# 따라서 아래처럼 --를 사용해서 옵션을 나눠야해
# kubectl exec -it nginx-pod -- ls -l /run
```