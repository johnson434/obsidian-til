---
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
🛑첫날: "✏첫날 :"
🛑오늘: "⏰오늘 : 2024/10/28"
🛑첫학습후 몇일째?: 첫 학습 후 ❤일째❤
🛑14일후: "🥇14일뒤 :"
오늘1: "@2024년 10월 27일 오후 2:02"
오늘2: 2024/10/27
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[Section 21- Identity (1)]] [[AWS STS]]
# 단서 질문
- AWS STS란?
	- AWS Security Token Service의 약자로 AWS 리소스의 접근 가능한 토큰을 준다.

# 핵심 필기
## AWS STS - Security Token Service
- AWS 리소스에 접근 권한을 준다.
- 최대 1시간 유효하다. (새로 부여받아야 한다.)
- API를 통해서 다음과 같은 역할을 받을 수 있다.
	- AssumeRole
		- 자신의 계정에 적용하여 보안을 강화하기 위해서 사용하거나 Cross Account Access는 타겟 계정에서 특정 Action을 취할 수 있게 해준다.
	- AssumeRoleWithSaml
		- SAML로 로그인한 유저에게 credential을 리턴한다.
	- AssumeRoleWithWebIdentity
		- IdP(Facebook Login, Google Login, OIDC Compatible...)로 로그인한 유저들의 cred를 리턴한다.
		- AWS는 이 방법은 권장하지 않고 Cognito 사용을 권장한다.
	- GetSessionToken
		- MFA를 통해 로그인한 일반 유저나 루트 유저가 cred를 얻는 방법
## Using STS to Assume a Role
- 그림 ![[Pasted image 20241029105811.png]]
- 자신의 계정이나 교차계정(cross-account)에 IAM Role을 정의하세요.
- 해당 IAM Role에 누가 접근 가능한지 정의하세요.
- AWS STS에 API 요청을 통하여 cred를 받으세요.
- 임시 Cred는 15분에서 1시간 동안 유효합니다.

- Cross-Account with STS![[Pasted image 20241029110019.png]]

# 핵심 요약