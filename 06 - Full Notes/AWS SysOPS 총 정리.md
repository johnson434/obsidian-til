---
⭕첫 학습날: 2024-10-01
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
🛑첫날: "✏첫날 : 2024/10/01"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤26일째❤
🛑4일후: "🥉4일뒤 : 2024/10/05"
🛑7일후: "🥈7일뒤 : 2024/10/08"
🛑14일후: "🥇14일뒤 : 2024/10/15"
4일후: "@2024년 10월 5일"
4일후(text): 2024/10/05
7일후: "@2024년 10월 8일"
7일후(text): 2024/10/08
14일후: "@2024년 10월 15일"
14일후(text): 2024/10/15
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/10/01
오늘과 첫학습날 사이: "26"
사이: "26"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[AWS]]

### 단서 질문

- AWS 리소스별 AZ, Region 스코프
    
    |   |   |   |   |   |
    |---|---|---|---|---|
    |**AWS 리소스**|**AZ 한정**|**Region 한정**|**추가 사항**|**역할 요약**|
    |**EC2 Instance**|Yes|No|AZ에서 실행되지만, EBS 스냅샷, AMI 등은 Region 내에서 사용 가능|가상 서버|
    |**Elastic Load Balancer (ELB)**|Yes (Classic, NLB)|Yes (ALB)|ALB는 여러 AZ에서 트래픽을 분산, NLB는 AZ 내에서 연결 관리 가능  <br>CrossZone 설정을 통해 여러 2개 이상 가용 영역에 로드밸런싱 가능|트래픽 분산|
    |**Elastic Block Store (EBS)**|Yes|No|AZ 내에서만 사용 가능하지만, EBS 스냅샷은 Region에 저장|EC2의 영구 스토리지|
    |**VPC (Virtual Private Cloud)**|No|Yes|Subnet은 AZ 한정, VPC 자체는 Region 한정|네트워크 격리|
    |**S3 (Simple Storage Service)**|No|Yes|S3는 Region 내에서 사용되며, 여러 AZ에 데이터 저장|객체 스토리지|
    |**RDS (Relational Database Service)**|Yes|Yes|멀티 AZ 배포 옵션 사용 가능|관계형 데이터베이스 관리|
    |**DynamoDB**|No|Yes|Global Table을 통해 여러 Region 간 복제 가능|비관계형 데이터베이스|
    |**Lambda**|No|Yes|람다 함수는 Region 단위로 배포되며, AZ에 걸쳐 실행 가능|서버리스 함수 실행|
    |**CloudFront**|No|No|전 세계 엣지 로케이션 사용|글로벌 CDN (콘텐츠 전송 네트워크)|
    |**Route 53**|No|No|전 세계 도메인 이름 관리|DNS 관리|
    |**Elasticache**|Yes|No|인스턴스는 AZ 내에서 실행, 멀티 AZ 지원 가능|인메모리 캐시 서비스|
    |**IAM (Identity and Access Management)**|No|No|글로벌 서비스로, Region에 구애받지 않음|사용자 및 권한 관리|
    |**CloudFormation**|No|Yes|템플릿 배포는 Region에 한정됨|리소스 자동화 배포|
    |**SNS (Simple Notification Service)**|No|Yes|멀티 AZ에 구애받지 않고 Region에서 사용 가능|메시징 서비스|
    |**SQS (Simple Queue Service)**|No|Yes|메시지 큐는 Region 단위로 사용|메시지 큐 관리|
    |**EKS (Elastic Kubernetes Service)**|Yes|Yes|클러스터는 AZ에 분산 가능하지만, 관리 기능은 Region 한정|Kubernetes 관리 서비스|
    |**CloudWatch**|No|Yes|모니터링은 Region 단위로 동작|모니터링 및 로깅 서비스|
    |AWS Config|No|Yes|Region 단위로 동작하지만 여러 Region을 통합할 수 있다.|시스템의 규약을 설정하고 해당 규약을 벗어나는(SSH 포트가 열려있거나 ALB 규칙이 변경) 이벤트가 발생하면 알림을 보낼 수 있다.|
    |**KMS (Key Management Service)**|No|Yes|키는 Region 한정으로 사용 가능|암호화 키 관리|
    |**Redshift**|Yes|Yes|클러스터는 AZ 내에서 실행되며, Region 간 복제 가능|데이터 웨어하우스|
    |**Aurora**|Yes|Yes|멀티 AZ 지원, Aurora 글로벌 데이터베이스로 Region 간 복제 가능|고성능 관계형 데이터베이스|
    |**ECR (Elastic Container Registry)**|No|Yes|Region에 한정된 컨테이너 이미지 관리|컨테이너 이미지 저장소|
    |**Elastic Beanstalk**|Yes|Yes|애플리케이션 배포는 AZ에서 실행되지만, 리소스는 Region에 배포됨|애플리케이션 배포 관리|
    |**Auto Scaling**|Yes|Yes|AZ에 걸쳐 EC2 인스턴스 자동 조정|자동화된 확장|
    |**Direct Connect**|No|Yes|여러 AZ에서 연결 가능, Region 단위로 데이터 전송|온프레미스와 AWS 네트워크 연결|
    |**Step Functions**|No|Yes|워크플로우는 Region 내에서 동작|서버리스 워크플로우 관리|
    
- Security Group vs NACL vs Firewall
    
    |   |   |   |   |
    |---|---|---|---|
    |특징|Security Group (SG)|Network ACL (NACL)|방화벽 (Firewall)|
    |**적용 범위**|개별 **EC2 인스턴스**나 **ENI(Elastic Network Interface)**에 적용|**서브넷** 수준에서 적용 (VPC의 모든 인스턴스에 적용 가능)|보통 네트워크 외부와 내부 사이에서 전체 네트워크에 적용|
    |**상태**|**Stateful**: 인바운드 트래픽이 허용되면 해당 세션의 아웃바운드 트래픽은 자동 허용|**Stateless**: 인바운드와 아웃바운드 트래픽을 별도로 설정해야 함|보통 Stateful, Stateless 모두 가능|
    |**허용/거부**|**허용 규칙**만 설정 가능. 명시적으로 허용한 트래픽만 허용|**허용 및 거부** 규칙 모두 가능. 명시적으로 거부할 수 있음|허용 및 거부 규칙을 모두 설정할 수 있음|
    |**적용 순서**|모든 규칙이 **동시에** 평가됨 (우선순위 없음)|규칙에는 **번호 순서**가 존재하며, 가장 낮은 번호부터 평가|방화벽 규칙은 보통 우선순위에 따라 평가됨|
    |**기본 허용 정책**|모든 인바운드 및 아웃바운드 트래픽은 기본적으로 차단됨|모든 인바운드 및 아웃바운드 트래픽은 기본적으로 허용됨|기본적으로 차단하거나 허용하는 정책이 다양함|
    |**주 용도**|EC2 인스턴스 수준의 세밀한 보안 설정|VPC의 서브넷에서 네트워크 트래픽을 제어|기업 내외부의 네트워크 전체에 대한 보호|
    

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 