---
기술:
  - Linux
---
[[Linux]] [[Linux Network Tool]] [[Network Port]]

# ss

- 소켓을 조회하는 유틸리티로 netstat보다 최신이다.
- 리눅스에서는 netstat보다 ss 사용을 권장한다.
- **Flag**
    - **-a**(all) : ss는 -a 플래그 없이 사용하면 Listening socket을 제외한 소켓만 출력한다. -a을 사용하면 모든 socket을 출력한다.
    - -f(family : 소켓의 유형을 지정합니다.
        - **unix**
        - **inet**
        - **inet6**
        - **link**
        - **netlink**
        - **vsock**
    - -t(tcp) : tcp 소켓 출력
    - -u(udp) : udp 소켓 출력
    - src(source) : 해당하는 포트 출력
        
        ```Bash
        ss src [포트번호]
        ```