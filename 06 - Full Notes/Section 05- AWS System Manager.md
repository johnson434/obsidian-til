---
⭕첫 학습날: 2024-09-12
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: true
복습: 장기기억
🛑첫날: "✏첫날 : 2024/09/12"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤45일째❤
🛑4일후: "🥉4일뒤 : 2024/09/16"
🛑7일후: "🥈7일뒤 : 2024/09/19"
🛑14일후: "🥇14일뒤 : 2024/09/26"
4일후: "@2024년 9월 16일"
4일후(text): 2024/09/16
7일후: "@2024년 9월 19일"
7일후(text): 2024/09/19
14일후: "@2024년 9월 26일"
14일후(text): 2024/09/26
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/09/12
오늘과 첫학습날 사이: "45"
사이: "45"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "1"
학습률: "0.8"
진행바: 🟩🟩🟩🟩🟩🟩🟩🟩⬜⬜ 80%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[AWS System Manager]]
### 단서 질문

- System Manager란?
    
    온프로미스와 EC2의 시스템 설정을 하거나 시스템의 상태를 확인하는데 사용된다.
    
- System Manager에 인스턴스를 등록하려면?
    
    인스턴스에 IAM Role(SSM Agent)을 부여
    
- Document란?
    
    특정 커맨드라인이나 명령어를 실행하기 위해 설정해둔 모음집
    
- Automation이란?
    
    Document를 자동화해서 실행하는 기능
    
- StateManager란?
    
    인스턴스가 정의된 State에서 벗어나지 않도록 유지하는 역할
    
- PatchManager란?
    
    소프트웨어 업데이트 등 Patch를 관리해주는 역할
    
- Inventory
    
    소프트웨어 버전 등 인스턴스의 메타 데이터 등을 저장하는 공간
    

### 핵심 필기

- 전체 내용 접기
    - Systems Manager Overview
        - AWS Systems Manager Overview
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0066.jpg]]
            
            - EC2와 온프로미스 시스템 확장(Scale)을 도와준다.
            - 인프라에 대한 운영 인사이트를 준다.(Get Operational Insight about the state of infrastructure)
            - 문제 발견이 쉽다.
            - 향상된 규정에 맞게 자동화를 수정한다.(Patching automation for enhanced compliance)
            - 윈도우와 리눅스 둘 다 동작한다.
            - CloudWatch metrics/dashboards와 통합된다.
            - AWS Config와 통합된다.
            - **무료다**
        - AWS Systems Manager Features
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0067.jpg]]
            
        - How Systems Manager works
            
            ![[image 41.png]]
            
            - SSM Agent를 인스턴스에 설치하면 SSM에서 관리가 가능하다.
            - SSM은 AMI 2와 AMI 2023에 기본적으로 설치된다.
            - 만약, SSM으로 컨트롤이 안되면 SSM Agent 이슈일 확률이 높다.
            - EC2 인스턴스는 SSM Action을 하기 위해선 적절한 IAM Role을 가져야 한다.
    - Start EC2 Instance with SSM Agent
        
        EC2 인스턴스를 실행할 때, IAM Role로 SSM Agent를 주면 SSM Agent가 실행되며 SSM의 Fleet Manager에서 해당 인스턴스를 확인할 수 있다.
        
    - AWS Tags & SSM Resource Groups
        - AWS Tags
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0069.jpg]]
            
            - 태그는 Key, Value로 이루어져있다.
            - 사용처는 아래 3가지다
                - Resource Group
                - Cost Allocation
                - Automation
            - 태그를 통해서 Resource Group을 나눌 수 있다.
                - e.g. key로 Environment value로 dev나 prod를 통해 개발을 위한 리소스인지 배포를 위한 리소스인지 그룹화 가능하다.
            - 태그는 많이 쓰는 게 적은 것보단 낫다
        - Resource Groups
            
            ![[image 1 14.png]]
            
            - 특정 목적을 위한 리소스들을 그룹화하는 것
            - Tag를 이용해서 그룹화한다.
            - 지역 서비스다.(Regional Service)
            - 서로 다른 계층의 어플리케이션도 하나의 논리적 그룹으로 묶을 수 있다.
                - e.g. Application, Different Layers of Application Stack, Production vs Development
            - DynamoDB, S3, Lambda, EC2 등에 사용할 수 있다.
    - Documents & SSM Run Command
        - SSM - Documents
            
            - 파라미터와 액션을 지정하여 특정 커맨드라인을 실행하기 위해 사용되는 서비스
            - ssh가 필요 없다.
            - JSON or YAML 형식으로 저장된다.
                
                ![[image 2 12.png]]
                
            - AWS에서 기본적으로 제공하는 Document들이 존재한다.
            
            ![[image 3 11.png]]
            
        - SSM - Run Command
            
            ![[image 4 11.png]]
            
            - EventBridge를 통해 실행되거나 직접 실행할 수 있다.
            - Place Group을 이용해서 여러 인스턴스에서 동시에 실행 가능하다.
            - Rate Control/Error Control이 가능하다.
                - Rate Control: 비율 조절로 Document를 동시에 실행할 인스턴스에 제한을 둔다.
                - Error Control: Document 실행 중에 에러가 발생한 인스턴스 개수가 특정 비율을 넘어서면 작업을 중단한다.
            - Document 실행 결과는 S3나 CloudWatchLogs에 기록할 수 있다.
            - Intergrated with IAM & CloudTrail
            - 진행 과정을 AWS SNS에 보낸다.(In Progrss, Success, Failed, …)
    - SSM Automations
        - SSM - Automation
            
            ![[image 5 9.png]]
            
            - 자동화 유형의 SSM Documents(SSM Documents of type Automation)
            - 유지, 보수, 배포를 자동화를 통해 간소화한다.(Simplifies common maintenance and deployment tasks of EC2 instances and other AWS resources)
                - e.g.
                    - Restart Instance
                    - Create AMI
                    - EBS Snapshot  
                          
                        
            - 리소스 그룹을 지정해서 자동화 작업이 가능하다.
            - 트리거 되는 방법은 아래와 같다
                - AWS Console, AWS CLI, AWS SDK
                - Amazon EventBridge
                - Maintenance Windows로 인한 스케쥴링
                - AWS Config의 환경 복원(By AWS Config for rules remediations)
    - SSM - Parameter Store
        - SSM - Parameter Store
            
            ![[image 6 9.png]]
            
            - 설정값과 시크릿을 저장하는데 사용된다.
            - 값을 버전 관리할 수도 있다.
            - Key, Value 형태로 데이터를 저장한다.
            - 데이터 저장 방식은 평문이거나 암호화할 수 있다.
            - 암호화 키가 없더라도 데이터를 받을 수 있다.
            - 암호화는 KMS를 통해서 사용한다.
            - 해당 KMS 키에 KMS 접근 권한이 없는 경우, Parameter Store로부터 키와 값을 가져올 수는 있지만 복호화는 할 수 없다.(복호화 시도 시에 권한이 없다고 나옴)
            - 서버리스, 확장성, 지속성, 쉬운 SDK를 가지고 있다.(serverless, scalable, durable)
            - IAM을 통해서 보안을 한다.
            - EventBridge를 통해서 알림(Notification)을 보낸다.
        - SSM - Parameter Store Hireachy
            
            ![[image 7 7.png]]
            
            - uri를 통한 계층화를 통해서 상태값을 저장할 수 있다.
        - Standard and advanced parameter tiers
            
            ![[image 8 7.png]]
            
        - Parameters Policies (for advanced parameters)
            
            ![[image 9 7.png]]
            
            - 파라미터를 통해서 TTL을 설정해서 강제 업데이트하거나 민감한 데이터를 삭제할 수 있다.
            - 한 번에 여러 개에 정책을 할당할 수 있다.
    - Inventory & State Manager
        - SSM - Inventroy
            - EC2 인스턴스나 온프로미스 환경으로부터 메타데이터를 수집한다.
            - 메타데이터는 소프트웨어, 설정, OS 드라이버, 업데이트 내역, 실행 중인 서비스 등을 포함합니다.
            - AWS Console을 통해 보거나 혹은 S3에 저장하여 Athena나 QuickSight를 통해 확인할 수 있다.
            - 데이터 저장 주기를 명시할 수 있다.(분, 시간, 일)
            - 여러 계정, 여러 리전에서 데이터를 쿼리할 수 있다.
            - Custom Inventory를 만들 수 있다.(e.g. rack location, 기타 커스텀한 내용)
        - SSM - StateManager
            - EC2와 온프로미스 모두 사용 가능하다.
            - 정의한 상태를 유지하도록 사용된다.
            - Use cases:
                1. bootstrap with software(운영체제 부팅 중에 특정 소프트웨어를 실행)
                2. 특정 포트 번호를 닫아놓는다.
                3. 설정이 적용 됐을 때 스케쥴을 특정하기(Specify a schedule when this configuration is applied.)
            - Uses SSM Documets to create an Association(e.g. Document for cloudwatch agent)
    - SSM PatchManager and Maintenance Windows
        - 개요
            - EC2와 온프로미스 둘 다 지원한다.
            - Linux, macOS, Window 모두 지원한다.
            - 패치를 자동화하는 역할이다.
            - OS 업데이트, 소프트웨어 업데이트, 보안 업데이트 등이 있다.
            - 직접 요구하거나 Maintenance Windows를 통해 스케쥴링 가능하다.(Patch on-demand or on a schedule using Maintenance Windows)
            - Scan instances and generate patch compliance report (missing patches)
            - Patch compliance report can be sent to S3
        - Baseline
            - Patch Baseline(수정 기준선?)
                - 어떤 패치가 인스턴스(ec2, on-premise)에 적용되어야 할지 기준 점
                - Ability to create custom Patch Baselines(specify approved/rejected patches)
                - 패치는 출시 후 몇일 이내에 자동으로 승인될 수 있습니다.(Patches can be auto-approved within days of their release)
                - 디폴트 설정으로는 중요한 패치나 보안 관련 이슈만 Baseline에 속합니다.(By default, install only critical patches and patches related to security)
            - Patch Group
                - 특정 패치가 적용되는 인스턴스의 그룹입니다.
                - 인스턴스는 단 하나의 Patch Group에만 속할 수 있습니다.
                - Patch Group은 단 하나의 Patch Baseline을 가집니다.
                - 사용 예시: 패치 그룹 for dev, prod
            - Pre-defined Patch Baseline
                - AWS에 의해서 사전 정의된 Baseline
                - AWS-RunPatchBaseline - AWS에서 제공하는 Document로 OS와 소프트웨어 업데이트를 실행하는 Document다.
            - Custom Patch Baseline
                - 사용자의 의해 정의 가능한 custom baseline
                - OS, 패치 허용, 패치 거부(Operating System, allowed patches, rejected patches, …)
                - 특정 저장소를 명시해서 해당 저장소로부터 업데이트 받을 수 있다.(Ability to specify custom and alternative patch repositories)
        - 흐름도
            
            ![[image 10 6.png]]
            
        - Maintenance Windows
            - 특정 시각에 작업이 필요한 것들은 Maintenance Windows를 통해서 작업이 가능하다.
            - Maintenance Window contains  
                • Schedule  
                • Duration  
                • Set of registered instances  
                • Set of registered tasks  
                
    - SSM Session Manager
        - SSM - Session Manager(1)
            
            ![[image 11 6.png]]
            
            - Allows you to start a secure shell on your EC2 and on- premises servers
            - Access through AWS Console, AWS CLI, or Session  
                Manager SDK  
                
            - Does not need SSH access, bastion hosts, or SSH  
                keys  
                
            - Supports Linux, macOS, and Windows
            - Log connections to your instances and executed  
                commands  
                
            - Session log data can be sent to S3 or CloudWatch Logs
            - CloudTrail can intercept StartSession events
        - SSM - Session Manager(2)
            
            ![[image 12 6.png]]
            
            - IAM Permissions
                - Control which users/groups can  
                    access Session Manager and which  
                    instances  
                    
                - Use tags to restrict access to only  
                    specific EC2 instances  
                    
                - Access SSM + write to S3 + write to  
                    CloudWatch  
                    
            - Optionally, you can restrict  
                commands a user can run in a  
                session  
                
        - SSH vs Session Manager
            
            ![[image 13 6.png]]
            

### 핵심 요약

- 핵심 요약 접기
    - SSM(AWS System Manager)는 온프로미스와 인스턴스들의 시스템 설정을 관리하는 역할
    - 온프로미스 환경에서도 SSM Agent를 설정하면 시스템 설정 관리가 가능
    - Tag를 통해서 리소스 그룹을 정의할 수 있다.(인스턴스 한정하지 않고 모든 리소스를 그룹화 가능)
    - 리소스 그룹의 스코프는 리전
    - Document는 시스템 설정을 위한 명령어의 집합
    - AWS Automation은 Document 실행의 자동화를 위한 도구(EventBridge 등 트리거 이벤트 정의 가능 혹은 AWS Console을 통해서도 실행 가능)
    - AWS Parameter Store는 Key, Value로 설정값을 저장(암호화 시에 KMS를 통해서 암호화)
    - AWS Inventory는 시스템의 메타데이터(소프트웨어 버전, OS 드라이버 등)를 저장
    - AWS StateManager는 노드가 특정 상태를 유지하도록 관리한다.(포트 열기, 프로세스 실행 등)
    - AWS PatchManager는 노드들의 특정 기능(OS 버전, 소프트웨어 버전 등) 업데이트를 관리한다. PatchManger로 그룹화 가능
    - AWS SessionManager을 통해 사용자가 secure shell로 접속할 수 있습니다. ssh를 사용할 필요가 없으므로 22번 포트를 열 필요가 없습니다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 