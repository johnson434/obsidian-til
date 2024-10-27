---
기술:
  - Bash
  - Linux
---
[[Programming Language]] [[Bash]]
리눅스에서 명령어와 스크립트를 실행을 위한 환경 및 인터프린터를 뜻한다.
# Bash 단기 집중 강좌

일반적인 명령줄에서 실행할 수 있는 모든 시스템 명령, 유틸리티, 애플리케이션을 실행할 수 있지만, 자체 내장 명령도 포함한다.

```Shell
#! [사용할 인터프리터] (셔뱅 = 스크립트에서 사용할 인터프리터를 작성하는 부분)

#! /usr/bin/bash
```

스크립트 작성 후에 ./my_script로 실행이 안됨. 왜냐? 실행 권한이 없어서.
chmod로 권한 수정 후에 ./my_script로 실행 가능.

```Shell
chmod 766 ./my_script
ls -l | grep my_scriptm
./my_script
```