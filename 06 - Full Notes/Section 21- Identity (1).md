---
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
🛑첫날: "✏첫날 :"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤일째❤
🛑4일후: "🥉4일뒤 : "
🛑7일후: "🥈7일뒤 : "
🛑14일후: "🥇14일뒤 : "
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[Ultimate AWS Certified SysOps Administrator Associate 2024]] 
[[Section 20- Security and Compliance for SysOps]] 
[[AWS Cognito]]
# 단서 질문
- AWS Cognito란?
	- 웹 및 모바일 앱을 위한 자격 증명 플랫폼
# 핵심 필기
## IAM Security Tools
IAM Security Tools
- IAM Credentials Report (계정 레벨)
	- 계정의 모든 유저와 credentials 정보를 리스트업한다.
- IAM Access Advisor (유저 레벨)
	- 특정 서비스에 대한 접근 권한과 해당 서비스에 마지막으로 접근한 시점을 보여준다.
	- Access Advisor 정보를 보고 정책을 편집하는데 사용할 수 있다.
## IAM Acess Analyzer
- IAM Aceess Analyzer
- 어떤 리소스가 외부에 공유되는지 찾아낸다.
- Zone of Trust를 정의하고 해당 영역을 벗어나면 findings에 명시된다.
## Identity Federation with SAML & Cognito
**What's Identity Federation**
- 연합은 AWS 외부에 사용자가 AWS에 접근할 수 있게 일시적으로 역할(Role)을 부여하는 것을 말합니다.
- 유저는 서드파티 인증 형식을 취한 Federation으로부터 acess Role을 부여받습니다.
- Federation은 LDAP와 같은 서드파티 인증을 취합니다.

**SAML Federation For Enterprises**
- [[SSO(Single Sign On)]]
- Active Directory / ADFS with AWS 통합하기 위해서 SAML Federation을 사용합니다.
- 일시적 cred로 AWS Console이나 CLI로 접근을 허가
- Client 앱을 통한 접근 방법![[Pasted image 20241029092656.png]]
- Console을 통한 접근 방법![[Pasted image 20241029092855.png]]
**Custom Identity Broker Application For Enterprises**
- Identity Provider가 SAML 2.0과 호환되지 않을 때만 사용해라
- Identity Broker는 적절한 IAM을 가져야 한다.![[Pasted image 20241029093520.png]]
**AWS Congnito - Federated Identity Pools For Public Applications**
- 목표
	- 클라이언트에서 AWS 리소스에 바로 접근이 가능하게
- 어떻게
	- Federated Identity Provier에 로그인하거나 익명으로 
	- Federated Identity Pool에서 일시적으로 AWS credential을 얻는다.
	- credential은 사전 정의된 IAM 정책 상태와 권한이다.
- 예
	- Facebook Login을 통해서 S3 쓰기 권한 일시적으로 얻기
- 노트
	- Web Identity Federation은 Coginito에 대안이지만 AWS에선 권장하지 않습니다.
- 자료 화면 ![[Pasted image 20241029102531.png]]
### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 