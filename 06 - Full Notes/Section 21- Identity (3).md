---
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
🛑첫날: "✏첫날 :"
---
[[Section 21- Identity (2)]] 
[[AWS Cognito]] 
[[Authentication vs Authorization]]
# 단서 질문
- AWS Cognito란
	- 
- AWS User Pools vs AWS Identity Pools
	- Cognito User Pools는 Authentication으로 로그인과 같이 유저를 검증하는 절차
	- Cognito Identity Pools는 Authorization으로 리소스에 대한 권한을 부여하는 역할
# 핵심 필기
## Cognito User Pools (CUP) - User Features
- 유저를 위한 서버리스 데이터베이스를 만든다.
- 간단한 로그인: 유저명이나 이메일과 패스워드를 사용하여 로그인이 가능하다.
- 패스워드 리셋 제공
- Email & 전화번호 검증
- MFA
- Facebook, Google, SAML 등 다양한 통합 아이덴티티를 제공
- cred가 오염됐으면 해당 유저를 block한다.
- 로그인을 하면 JWT를 리턴
- 그림 ![[Pasted image 20241029111339.png]]

## Cognito User Pools (CUP) - Integrations
- CUP은 API Gateway와 ALB랑 통합됩니다.
- 그림 ![[Pasted image 20241029111607.png]]
1. 클라이언트가 Cognito에 cred를 요청 및 Cognito에서 응답
2. 클라이언트는 응답 받은 Token을 통해 Gateway/ALB에 요청
3. Gateway/ALB는 요청 받으면서 넘겨 받은 Token을 Cognito에서 verifying
4. verifying을 만족하면 Backend/Target Group으로 요청이 전달
## Cognito Identity Pools (Federated Identities)
- AWS credentions를 얻기 위해선 먼저 Identity를 유저가 얻어야 한다. 유저가 받은 Identity를 기반으로 cred를 받기 때문이다. 
- 유저가 Identity를 받을 수 있는 pool을 가리켜 Cognito Identity Pools라고 부른다.
- Identity Pool (e.g Identity source)는 다음과 같은 항목이 있다.
	- 퍼블릭 제공자 (Amazon, Facebook, Google, Apple)
	- Amazon Cognito User pool의 유저들
	- OpenID Connect Providers나 SAML Identity Providers
	- Cognito Identity Pools는 인증 받지 못한(unauthenticated) 게스트 접근도 허용한다.
- 유저가 Identity를 얻고 cred를 얻으면 AWS 서비스에 직접 접근하거나 API Gateway를 통해서 접근이 가능하다.
	- credentials에 적용되는 IAM 정책은 Cognito에 정의되어 있다.
	- 또한, user_id 기반으로 커스터마이징이 가능하다. (더욱 정밀한 조절을 위해서)
## Cognito Identity Pools - Diagram
- 그림 ![[Pasted image 20241029133205.png]]
1. 유저는 User Pools에 로그인을 요청한다. Token를 얻는다.
2. AWS 리소스 접근을 위해서 Token 변경을 Cognito Identity Pools에 요청한다.
3. Cognito Identity Pools는 User Pools에 해당 토큰을 검증 받는다.
4. Cognito Identity Pools에선 STS로부터 cred를 받아서 유저에게 리턴한다.
5. 유저는 해당 cred를 통해 AW 리소스에 접근한다.
## Cognito Identity Pools - Diagram with CUP
![[Pasted image 20241029134348.png]]
## Cognito Identity Pools - IAM Roles
- 인증 유저와 게스트 유저가 사용할 수 있는 Default IAM Role을 정의한다.
- user ID 기반으로 어떤 Role을 부여할지 정하는 Rule을 정의한다.
- Policy Variables를 통해 유저의 접근을 나눌 수 있다.(You can partition your users' access using policy variables)

- IAM credentilas은 Cognito Identity Pools가 STS를 통해서 얻습니다.
- 역할은 Coginito Identity Pools trust 정책이 설정되어 있어야 한다.
## Cognito Identity Pools - Guest User Example
- IAM 정책 - 게스트 유저 샘플![[Pasted image 20241029143137.png]]
- IAM 정책 - Policy variable on S3 ![[Pasted image 20241029143223.png]]
- IAM 정책 - DynamoDB ![[Pasted image 20241029143259.png]]

## Cognito User Pools vs Identity Pools
- **Cognito User Pools** (for Authentication = Identity verification)
	- 웹과 모바일 어플리케이션의 유저 데이터베이스
	- 통합 로그인(federate login)을 허용한다.
	- UI를 커스터마이징 가능
	- authentication 과정에서 AWS Lambda 트리거 가능
	- 로그인에 서로 다른 리스크 레벨을 설정 가능하다.
- Cognito Identity Pools (for Authorization = access control)
	- 사용자에게 AWS Cred를 부여하여 리소스에 접근 가능하게함(권한 부여)
	-  사용자는 Public Social 계정이나, OIDC, SAML & Cognito User Pools를 통해 로그인 가능.
	- 사용자는 게스트일 수 있다. (unauthenticated user)
	- 사용자는 IAM 역할과 정책들에 매핑되며 policy variables를 사용 가능하다.
- CUP + CIP = 인증 + 권한 부여를 AWS에서 모두 처리

# 핵심 요약
- Cognito User Pools는 AWS에서 제공하는 Serverless 유저 인증 서비스
- Cognito Identity Pools는 AWS에서 제공하는 AWS 권한 부여 서비스로 Credential을 리턴하고 해당 credential로 AWS의 리소스에 접근이 가능하다.

> [!important]  
> 