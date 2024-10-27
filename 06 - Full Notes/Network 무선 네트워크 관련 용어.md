---
기술:
  - Network
---
[[03 - Tags/Network]]
# 네트워크 용어

**액세스 포인트(access point, AP)** : 무선 사용자가 인터넷에 액세스하기 위해 연결하는 장치이다.

**확장 서비스 세트 식별자(extended service set identifier, ESSID)** : SSID와 같지만 무선랜의 여러 AP에 사용할 수 있다.

**기본 서비스 세트 식별자(Basic Service Set Identifier, BSSID)** : 각 AP의 고유한 식별자로 기기의 MAC 주소와 동일하다.

**채널(channel)** : 와이파이는 14개 채널(1-14) 중 하나에서 작동할 수 있다. 미국에서는 1~11로 제한.

**신호 강도(power)** : 강할수록 크래킹하기 쉬워진다.

**보안(Security)** : 와이파이 AP에서 사용하는 보안 프로토콜이다.

**WEP(Wired Equivalent Privacy)** : 유선 동등 프라이버시로 결함이 있어 쉽게 크랙 된다.

**WPA(Wi-Fi Protected Access)** : WEP에 비해 안전하다.

**WPA2-PSK** : 사전 공유키인 PSK(pre-shared key)를 사용하는 보안 방법.

**모드(Mode)** : 관리, 마스터, 모니터 세 가지 모드 중 하나를 사용 가능하다.

**Managed(관리 모드)** : AP에 연결할 준비가 되었거나 연결되었음을 의미하는 관리 모드

**Master(마스터 모드)** : AP로 작동하거나 이미 AP에 작동할 준비가 되었음을 의미하는 마스터 모드

**Monitor(모니터 모드)** :

**무선 범위(wireless range)** : 0.5와트의 상한선에서 신호를 합법적으로 브로드캐스트해야 한다. 이 전력에서 정상 범위는 약 100미터다. 고성능 안테나는 이 범위를 최대 20마일까지 확장 가능하다.

**주파스(frequency)** : 와이파이는 2.4GHz, 5GHz를 사용한다.

# 기본 무선 명령

**ifconfig** : 네트워크 명령

**iwconfig** : 무선 인터페이스를 위한 명령

```Shell
hwang@hwang:~$ iwconfig
lo        no wireless extensions.

wlo1      IEEE 802.11  ESSID:"iptime5G"  
          Mode:Managed  Frequency:5.18 GHz  Access Point: 5A:86:94:C4:8C:48   
          Bit Rate=-1.89307e+06 kb/s   Tx-Power=22 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=70/70  Signal level=-38 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:3616   Missed beacon:0
```

**iwlist** : 네트워크 카드가 연결할 수 있는 모든 무선 액세스 지점을 볼 수 있다.

```Shell
iwlist [네트워크 인터페이스] [동작]
iwlist wlo1 scan
```

**nmcli(network manager command line)** : 네트워크 관리자 명령줄 인터페이스

```Shell
# dev(device)
nmcli dev networktype
nmcli dev wifi
nmcli dev wifi connect [AP-SSID] password [AP 비밀번호]
```