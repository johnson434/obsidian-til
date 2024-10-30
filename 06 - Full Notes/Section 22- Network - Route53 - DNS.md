---
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
🛑첫날: "✏첫날 :"
---
[[AWS]] 
[[Ultimate AWS Certified SysOps Administrator Associate 2024]] 
[[Route53]]
# 단서 질문
- CNAME과 Alias의 차이점은?
	- CNAME은 Non Root Domain(app.example.com)만 가능하지만 Alias는 Root와 Non Root Domain 둘 다 사용 가능합니다.
	- Alias는 무료다.
	- Alias를 통해서 헬스체크가 가능하다.

# 핵심 필기
## 297. [SAA/DVA] What is a DNS?
### What is DNS?
- Domain Name System로 호스트네임을 IP로 번역하는 서비스
### DNS Terminologies (DNS 전문 용어들)
- Domain Registrar(도메인 등록처): Amazon Route 53, GoDaddy, ...
- DNS Records: A, AAAA, CNAME, NS, ...
- Zone File: DNS Records를 포함하는 파일
- Name Server: DNS 쿼리를 처리하는 서버 (Authoritative or Non Authoritative)
- Top Level Domain(TLD): .com, .us, .in
- Second Level Domain(SLD): amazon.com, google.com
- 이미지 ![[Pasted image 20241030064053.png]]
### How DNS Works
- 이미지 ![[Pasted image 20241030064516.png]]
- 요청 순서는 아래와 같습니다.
	- 클라이언트에서 Local DNS 서버의 example.com 요청을 보냅니다.
	- Local DNS 서버에선 해당 DNS와 매칭되는 IP 주소가 있다면 해당 IP 주소를 클라이언트에게 리턴합니다.
	- Local DNS 서버에선 해당 DNS와 매칭되는 IP 주소가 없다면 먼저 Root DNS 서버에 도메인을 물어봅니다.
	- Root DNS는 탑레벨 도메인 서버의 주소를 리턴합니다.
	- Local DNS 서버에선 탑레벨 도메인 서버로 다시 도메인을 물어봅니다.
	- TLD DNS 서버에선 세컨드 레벨 도메인 서버에 주소를 리턴합니다.
	- Local DNS 서버에선 세컨드 레벨 도메인 서버로 다시 도메인을 물어봅니다.
	- 세컨드 레벨 도메인 서버는 해당하는 도메인의 주소를 리턴합니다.
	- Local DNS 서버는 도메인의 주소를 IP와 같이 캐싱하여 보관합니다. (도메인 서버에 매 번 요청하지 않기 위해서)
	- Local DNS 서버는 도메인과 일치하는 IP 주소를 클라이언트에 리턴합니다.
# 핵심 요약

> [!important]  
> 