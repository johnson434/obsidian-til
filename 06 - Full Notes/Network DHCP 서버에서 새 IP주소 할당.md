---
기술:
  - Linux
  - Network
---
[[Linux]] [[Linux CLI]] [[03 - Tags/Network]]
```Bash
dhclient '네트워크 인터페이스'
# 만약, File Exists라는 메시지가 뜬다면
# 이미 IP가 설정되어 있기 때문에 뜨는 메시지
# 존재하는 IP를 삭제하고 다시 진행해야함
ip addrs # 현재 ip 테이블에 저장된 주소들을 출력
ip addrs flush '네트워크 인터페이스' # 해당하는 네트워크 인터페이스 주소를 모두 삭제
dhclient '네트워크 인터페이스' # dhcp 서버로부터 IP 재할당
```