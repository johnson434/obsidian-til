---
기술:
  - Hacking
  - Network
  - Tool
---
[[Linux]] [[Linux Network Tool]] [[03 - Tags/Network]] 
nmap : 네트워크 툴로 해당 주소에 열려있는 포트를 확인하는 데에 사용한다.

```Shell
nmap [스캔 종류] [대상 IP] [대상 포트(선택적)]
# TCP를 쓰는 포트를 스캔
# 포트번호는 80
nmap -sT -p 80 google.com
# TCP SYN Scan
# 3-Way handshake 과정에서 Syn만 보낸 후에 종료한다.
# 따라서, 실행시간이 빠르고 흔적을 남기지 않아 더 private하다.
# MySQL은 3306 포트를 사용한다.
nmap -sS -p 3306 google.com
-oG : grep이 쉬운 형식으로 파일을 저장한다.
nmap -sS -p 3306 google.com >/dev/null -oG MYSQLscan
nmap -sS -p 3306 192.150.0.1-255
```