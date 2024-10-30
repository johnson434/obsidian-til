---
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
🛑첫날: "✏첫날 :"
---
[[Section 22- Network - Route53 - DNS]]
# 단서 질문
- 질문1

# 핵심 필기
## 298. [SAA/DVA] Route 53 Overview
### Amazon Route 53
- 높은 가용성, 확장성, 완전 관리형 권한 DNS입니다.
	- Authoritative 뜻은 사용자가 DNS Records를 업데이트할 수 있다(권한이 있다)는 뜻입니다.
- Route53 is also a Domain Registrar
- 리소스의 헬스 체크를 합니다.
- AWS에서 유일한 100% 서비스 레벨 가용성을 보장합니다.
- 53은 DNS 서버의 포트를 의미합니다.
### Route53 - Records
- 도메인 요청을 위해 트래픽 라우팅을 하는 방법
- 각 레코드는 다음 내용을 포함합니다.
	- Domain/subdomain Name: e.g. example.com
	- Record Type: e.g. A or AAAA
	- Value: e.g. 12.34.56.78
	- Routing 정책: DNS 쿼리에 대해서 Route53이 어떻게 반응할지
	- TTL: DNS Resolvers에 record가 캐시되는 총 시간
- Route 53은 다음과 같은 DNS Record Type을 지원합니다.
	- (시험에 나올 가능성 높음) A / AAAA / CNAME / NS
	- (advanced) CAA/ DS / MX / NAPTR / PTR / SOA / TXT / SPF / SRV
#### Route53 - Record Types
- A - hostname을 IPv4와 매핑
- AAAA - hostname을 IPv6와 매핑
- CNAME - hostname을 다른 hostname에 매핑
	- 타켓 도메인은 A나 AAAA 레코드를 가지고 있어야 한다.
	- Can’t create a CNAME record for the top node of a DNS namespace (Zone Apex)
	- 예: example.com은 못만들지만 www.example.com은 만들 수 있다.
- NS: Hosted Zone을 위한 Name 서버들
	- 도메인을 위해 트래픽이 어떻게 라우팅 될지 조절한다.
### Route53 - Hosted Zones
- 도메인과 서브 도메인에 트래픽을 어떻게 라우팅할지 정의하는 **레코드를 담고있는 컨테이너**다.
- Public Hosted Zones - 인터넷의 트래픽을 어떻게 라우팅할지 지정하는 레코드를 담은 컨테이너 (퍼블릭 도메인 네임) (e.g. application1.mypublicdomain.com)
- Private Hosted Zones - 한 개 이상의 VPC에서 트래픽을 어떻게 라우팅할지 지정하는 레코드를 담은 컨테이너 (e.g. application1.company.internal)
- Hosted Zone은 한 달의 $0.50
- 이미지 ![[Pasted image 20241030205141.png]]
- Public Hosted Zone은 인터넷과 VPC을 포함한 모든 네트워크에서 DNS 쿼리가 가능하지만 Private Hosted Zone은 VPC 내부에서만 요청이 가능합니다.
## 302. [SAA/DVA] Route 53 - TTL
### Route 53 - Records TTL (Time To Live)
- Route53에서 응답할 때 TTL을 넘겨주고 TTL을 받은 유저는 해당 기간만큼만 레코드를 캐싱한다.
- 해당 기간동안은 Route53에 다시 요청을 보내지 않아도 되고 이를 통해 트래픽을 조절할 수 있다.
- 이미지 ![[Pasted image 20241030205936.png]]
- Client에서 Route53에 도메인과 일치하는 IP를 요청한다.
- Route53에선 IP 주소와 함께 TTL을 리턴한다.
- Client에서 다시 도메인 주소로 요청을 할 때, 아직 TTL을 통해 설정된 유효기간을 지나지 않았다면 캐싱된 레코드를 이용하고 아니면 Route53으로 다시 DNS query를 진행한다.
- High TTL - e.g. 24hr
	- Route53에 적은 트래픽
	- 만료된 레코드를 사용할 가능성이 있다.
- Low TTL - e.g. 60sec
	- Route53에 더 많은 트래픽이 간다.
	- 만료된 레코드를 사용할 가능성이 적다.
	- 레코드 변경이 쉽다. (TTL이 금방 만료되므로 사용자에게 문제 발생할 가능성 거의x)
- 별칭 레코드(Alias Records)를 제외하곤 TTL을 DNS 레코드에 필수다.

## 303. [SAA/DVA] CNAME vs Alias
### CNAME vs Alias
- AWS 리소스(LoadBalancer, CloudFront...)들은 AWS hostname을 노출합니다
	- lb1-1234.us-east-2.elb.amazonaws.com을 myapp.mydomain.com 도메인으로 매핑하고 싶을 수 있습니다.
- CNAME:
	- 호스트네임이 다른 호스트네임을 가리킵니다. (app.domain.com => blabla.anything.com)
	- 단, Non Root Domain만 가능합니다. (예: something.mydomain.com이 있으면 mydomain.com은 안된다.)
- Alias
	- 호스트네임이 AWS의 리소스를 가리킵니다. (app.domain.com => blabla.anything.com)
	- **Root Domain과 Non-Root Domain 둘 다 사용할 수 있습니다.**
### Route 53 Alias Records
- 호스트네임을 AWS 리소스와 매핑
- Root, Non Root Domain 모두 사용 가능
- DNS 기능의 추가 기능이다. (An extension to DNS functionality)
- AWS 리소스 IP의 변화를 자동으로 감지한다.
- Alias Record는 항상 A/AAAA(IPv4/IPv6) 타입이다.
- TTL은 Route 53에서 설정해주므로 직접 설정할 수 없습니다.
- 이미지 ![[Pasted image 20241030215142.png]]
### Route 53 - Alias Records Targets
![[Pasted image 20241030215558.png]]

# 핵심 요약

> [!important]  
> 