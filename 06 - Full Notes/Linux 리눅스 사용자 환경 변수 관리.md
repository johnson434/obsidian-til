---
기술:
  - Linux
---
[[Linux]] [[Linux CLI]]
리눅스에서 존재하는 변수는 두 가지다. 셸 변수(shell variable)와 환경 변수(environment variable)이다.

# 환경 변수

시스템에 내장된 프로세스 전체에서 사용 가능한 변수. 대문자로 표시한다.

## 환경 변수 조회 및 수정

```JavaScript
hwang@hwang:~$ env | grep HOME
HOME=/home/hwang
```

## 모든 환경 변수 조회

셸 변수, 로컬 변수, 사용자 정의 셸 함수, 명령 알리아스(alias) 등 모든 환경 변수를 조회하는 방법

```JavaScript
hwang@hwang:~$ local_variable="hi"
hwang@hwang:~$ set | grep local_variable
local_variable=hi
```

## 셰션을 위한 변숫값 변경

```JavaScript
HISTSIZE=0 # 터미널에서 실행한 명령어 기록의 크기를 0으로 지정 -> 이전 실행 명령어를 하나도 기억 못함.
```

## 영구적인 변숫값 변경

셸 셰션동안 저장되는 변수는 셰션이 끝나면 동작이 끝난다.

**export** : 현재 환경의 새 값을 새롭게 포크 되는 자식 프로세스로 내보낸다. 새 프로세스는 해당 변수값을 상속받는다.

```JavaScript
hwang@hwang:~$ export greeting=hi
hwang@hwang:~$ echo $gretting
hi
hwang@hwang:~$ code &
# visual studio code 내에서 해당 변수 사용 가능하다. 그러나, 셸 스크립트를 새로 열면 해당 변수 사용 불가.
```

# 셸 변수

설정된 셸에서만 사용이 가능한 변수. 소문자로 표시한다.

# PATH 변수

셸에서 입력 되는 명령어들은 PATH 변수에서 찾습니다.

```Shell
# PATH 변수에 추가
PATH=$PATH:[추가할 디렉터리]
PATH=$PATH:/usr/bin/android-studio
```

# 변수 삭제

```Shell
unset [변수명]
```