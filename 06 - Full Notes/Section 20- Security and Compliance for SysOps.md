---
⭕첫 학습날: 2024-10-24
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 1일 복습
🛑첫날: "✏첫날 : 2024/10/24"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤3일째❤
🛑4일후: "🥉4일뒤 : 2024/10/28"
🛑7일후: "🥈7일뒤 : 2024/10/31"
🛑14일후: "🥇14일뒤 : 2024/11/07"
4일후: "@2024년 10월 28일"
4일후(text): 2024/10/28
7일후: "@2024년 10월 31일"
7일후(text): 2024/10/31
14일후: "@2024년 11월 7일"
14일후(text): 2024/11/07
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/10/24
오늘과 첫학습날 사이: "3"
사이: "3"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[AWS Security]]

### 단서 질문

- 질문1

### 핵심 필기

- 전체 내용 접기
    - **Shared Responsibility Model (최소 2~3개 문제 나옴)**
        - Shared Responsibility Model
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0546.jpg]]
            
            AWS Shared Responsibility Model
            
            - AWS의 책임 - 클라우드의 보안
                - AWS 서비스를 돌리는 인프라 구조를 보호한다.
                - 관련 서비스로는 S3, DynamoDB, RDS 등이 있다.
            - 소비자의 책임 - 클라우드 내부의 보안
                - EC2를 예시로 들면 게스트 OS, 방화벽, 네트워크 설정 IAM은 소비자가 책임진다.
                - 어플리케이션 데이터 암호화도 사용자의 책임이다.
            - Shared Controls:
                - Patch, 설정은 소비자와 AWS 모두 Control이 있으므로 각자 책임이다.
        - Example, for RDS
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0547.jpg]]
            
            RDS 책임 예시
            
            - AWS
                - 기반이 되는 EC2 인스턴스의 SSH disable
                - DB 업데이트 자동
                - OS 업데이트 자동
                - 기반이 되는 인스턴스와 함수 실행을 보장
            - 소비자의 책임
                - 포트, sg 확인
                - 데이터베이스의 유저 생성과 권한
                - public access 허용 여부
                - Parameter group이나 DB가 SSL 접속만 허용하기
                - 데이터베이스 암호화 설정
        - Example, for S3
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0548.jpg]]
            
            S3 책임 예시
            
            - AWS 책임
                - 무제한 용량을 보장
                - 암호화 보장
                - 다른 사용자와 데이터 분리를 보장
                - AWS 직원은 S3에 접근 불가능
            - 소비자 책임
                - 버켓 설정
                - 버켓 정책과 public 설정
                - IAM 사용자와 역할 설정
                - 암호화 설정
        - Shared Responsibility Model
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0549.jpg]]
            
              
            
    - [CCP] DDoS, AWS Shield and AWS WAF
        - What’s a DDOS Attack
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0550.jpg]]
            
            DDoS란 Distributed Denial-of-Service로 공격자가 수많은 마스터 노드로부터 수많은 봇을 사용하여 서버를 공격한다. 서버는 트래픽이 넘치고 이는 일반 사용자에게 Denial of Service라는 에러 메시지를 받게 한다.
            
        - DDoS Protection on AWS
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0551.jpg]]
            
            DDoS Protection on AWS
            
            - AWS Shield Standard: 웹사이트와 어플리케이션의 DDoS 방지를 해준다. 추가비용x
            - AWS Shiled Advanced: 매일 DDoS 공격을 막는다.
            - AWS WAF: 특정 패킷을 필터링한다.
            - CloudFront and Route53:
                - Global Edge 네트워크를 사용해서 가용성 보호가 가능하다.
                - AWS 쉴드랑 조합해서 Edge에서 공격을 완화할 수 있다.
            - DDoS를 대비해서 오토스케일링을 해야 한다.
        - AWS DDoS 방지 아키텍처
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0552.jpg]]
            
              
            
        - AWS Shield
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0553.jpg]]
            
            **AWS Shield**
            
            - **AWS Shield Standard:**
                - 모든 사용자에게 무료
                - SYN/UDP 플러드, 리플렉션 공격, L3/L4 계층 공격으로부터 보호한다.
            - **AWS Shield Advanced:**
                - 옵션으로 디도스 완화 서비스를 제공합니다. (조직 한 달 당 $3,000)
                - EC2, ELB, CloudFront, AWS Global Accelerator, Route53 서비스를 향한 정교한 공격도 막아줍니다.
                - 24/7 DDoS response team과 연결 가능합니다.
                - DDoS 공격으로 인해 발생하는 spike 트래픽으로 인한 높은 비용으로부터 막아줍니다.
        - AWS WAF - Web Application Firewall
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0554.jpg]]
            
            **AWS WAF - Web Application Firewall**
            
            - 웹 취약점으로부터 웹어플리케이션을 보호합니다.
            - L7 Http, L4 TCP입니다.
            - HTTP 프로토콜을 사용하므로 HTTP 프로토콜 친화적인 ALB, API Gateway, CloudFront에서 사용 가능합니다.
            
              
            
            - Web ACL을 정의합니다.
                - IP 주소, HTTP 헤더, HTTP body, URL 문자열을 통해서 접근을 제한 가능합니다.
                - SQL Injection고 XSS 공격을 방지합니다.
                - 요청 사이즈 제한과 지역을 제한이 가능합니다.
                - 평가 기반 규칙 (시간당 요청 개수 등) - DDoS 방지용
        - Penetration Testing on AWS Cloud
            - Penetration Testing on AWS Cloud (1)
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0555.jpg]]
                
                  
                
            - Penetration Testing on AWS Cloud (2)
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0556.jpg]]
                
                  
                
            - 시험에 나오는 부분
                
                - AWS는 침입 테스트를 몇몇 리소스에 허용한다.
                - 단, DDoS와 같은 몇몇 특정 테스트는 금지됐다. 허가 받고 진행해야함.
                
                  
                
        - Amazon Inspector
            
            - Amazon Inspector
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0557.jpg]]
                
                Amazon Inspector
                
                - 보안 평가 자동화
                - EC2 인스턴스에서 평가할 때는
                    - AWS System Manager (SSM) agent를 이용한다.
                    - 의도되지 않은 네트워크 접근이 가능한지 분석한다.
                    - 실행되는 OS의 취약점을 분석한다.
                - ECR에 등록되는 Container Image 평가할 때는
                    - 푸시되는 Container 이미지를 평가한다.
                - Lambda 평가할 때는
                    - 코드와 의존 패키지에 취약점을 분석한다.
                    - 람다가 배포될 때 검사합니다.
                
                  
                
                - 보고 & 통합은 Security Hub와 진행한다.
                - 결과물을 Amazon EventBridge로 전달한ㄷ.
            - What does Amazon Inspector evaluate?
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0558.jpg]]
                
                **Amazon Inspector가 검사하는 항목들**
                
                - **중요!!** EC2 인스턴스, Container Image, 람다
                - 필요할 때 인프라의 지속적 스캔
                
                  
                
                - CVE(Common Vulnerabilities and Exposure) 데이터베이스 내용을 통해서 패키지 취약점을 검사합니다.
                - EC2의 네트워크 reachability
            
              
            
        - Logging in AWS
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0559.jpg]]
            
            **Logging in AWS for security and compliance**
            
            - 규정 준수를 돕기 위해서 AWS에선 서비스 특화 로그와 검사 로그를 제공합니다.
            - 다양한 서비스 로그를 지원합니다.
        - Amazon GuardDuty
            
            - Amazon GuardDuty (1)
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0560.jpg]]
                
                  
                
            - Amazon GuardDuty (2)
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0561.jpg]]
                
                  
                
            
              
            
        - AWS Macie
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0562.jpg]]
            
              
            
        - Trusted Advisor
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0563.jpg]]
            
              
            
        - Encryption 101
            - Why encryption? Encryption in flight (TLS / SSL)
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0564.jpg]]
                
                  
                
            - Why encryption? Server-side encryption at rest
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0565.jpg]]
                
                  
                
            - Why encryption? Client-side encryption
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0566.jpg]]
                
                  
                
        - KMS
            
            - a
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0567.jpg]]
                
                - **CloudTrail로 KMS Key 사용처를 검사할 수 있다. (시험 가능성 높음)**
                
            - b
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0568.jpg]]
                
                  
                
            - c
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0569.jpg]]
                
                  
                
            - d
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0570.jpg]]
                
                  
                
            - e
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0571.jpg]]
                
                  
                
            
              
            
            - f
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0572.jpg]]
                
                  
                
        - KMS Key Rotation
            - KMS Automatic Key Rotation
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0573.jpg]]
                
                  
                
            - KMS On-Demand Key Rotation
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0574.jpg]]
                
                  
                
            - KMS Manual Key Rotation (Customer-Managed Symmetric KMS Key & Imports)
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0575.jpg]]
                
                  
                
            - KMS Alias Updating
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0576.jpg]]
                
                  
                
            - KMS for SysOps
                
                - a
                    
                    ![[AWS_Certified_SysOps_Slides_v31_page-0577.jpg]]
                    
                      
                    
                - b
                    
                    ![[AWS_Certified_SysOps_Slides_v31_page-0578.jpg]]
                    
                      
                    
                - c
                    
                    ![[AWS_Certified_SysOps_Slides_v31_page-0579.jpg]]
                    
                      
                    
                - d
                    
                    ![[AWS_Certified_SysOps_Slides_v31_page-0580.jpg]]
                    
                      
                    
                
                  
                
        - CloudHSM
            
            - CloudHSM
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0581.jpg]]
                
                **CloudHSM**
                
                - KMS는 소프트웨어 암호화를 관리한다면 CloudHSM은 암호화 하드웨어를 제공합니다.
                - 암호화를 위한 Key는 KMS와 달리 사용자가 관리합니다.
                - SSE-C 암호화를 사용할 때 고려할만한 좋은 방법이다.
            - CloudHSM Diagram
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0582.jpg]]
                
                  
                
            - CloudHSM - HA
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0583.jpg]]
                
                  
                
            - CloudHSM - Integration with AWS Services
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0584.jpg]]
                
                  
                
            - CloudHSM vs KMS
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0585.jpg]]
                
                  
                
                ![[AWS_Certified_SysOps_Slides_v31_page-0586.jpg]]
                
                  
                
                  
                
            
              
            
        - AWS Artifact Overview
    - 이미지
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0587.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0588.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0589.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0590.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0591.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0592.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0593.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0594.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0595.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0596.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0597.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0598.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0599.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0600.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0601.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0602.jpg]]
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0603.jpg]]
        
          
        

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 