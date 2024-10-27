---
기술:
  - Linux
  - Network
---
[[Linux]] [[03 - Tags/Network]] [[DNS]]
 **dig** : 도메인 네임 시스템에 질의응답하기 위해 사용되는 명령어

```Bash
# naver.com의 IP 주소를 반환
dig naver.com
# name server의 주소를 반환
dig naver.com ns
# 관련 메일 주소를 반환
dig naver.com mx
```


# DNS 서버 변경

/etc/resolv.conf 수정

```Bash
leftpad /etc/resolv.conf
# nameserver 10.0.2.3
```

# 고유의 IP 주소 매핑

웹브라우저에서 입력한 도메인을 IP 주소로 정할 수 있다.

```Bash
vim /etc/hosts
```