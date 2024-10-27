---
⭕첫 학습날: 2024-09-15
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
⭕학습정도: 😡하
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: true
복습: 추가 복습
🛑첫날: "✏첫날 : 2024/09/15"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤42일째❤
🛑4일후: "🥉4일뒤 : 2024/09/19"
🛑7일후: "🥈7일뒤 : 2024/09/22"
🛑14일후: "🥇14일뒤 : 2024/09/29"
4일후: "@2024년 9월 19일"
4일후(text): 2024/09/19
7일후: "@2024년 9월 22일"
7일후(text): 2024/09/22
14일후: "@2024년 9월 29일"
14일후(text): 2024/09/29
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/09/15
오늘과 첫학습날 사이: "42"
사이: "42"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "1"
학습률: "0.8"
진행바: 🟩🟩🟩🟩🟩🟩🟩🟩⬜⬜ 80%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[High Availability]]
### 단서 질문

- ASG란?
    
    ASG란 AutoScaling Group의 약자로 ASG를 생성하면 해당 그룹을 통해 인스턴스의 생성이나 제거를 할 수 있습니다.
    
- ASG 스케일링 기법들
    
    1. Dynamic Scheduling
        1. 동적 스케쥴링 기법으로 매트릭스 기반으로 인스턴스의 개수를 조절합니다.
            1. Target Tracking Scaling
                1. 원하는 목표치를 설정하면 해당하는 상태에 맞게 오토스케일링
                2. ex: CPU 사용량 40%
            2. Simple / Step Scaling
                1. 클라우드 워치 알람이 트리거되면(CPU > 70%) 인스턴스를 2개 추가
                2. 클라우드 워치 알람이 트리거되면(CPU < 30%) 인스턴스를 1개 제거
    
      
    
- AWS DynamoDB(AWS에서 제공하는 NOSQL 서버리스 DB)와 AWS Aurora(AWS에서 제공하는 RDS)가 AutoScaling이랑 무슨 연관이 있나?
    
    두 서비스 모두 오토스케일링을 지원
    

### 핵심 필기

- 전체 내용 접기
    - [SAA/DVA] Auto Scaling Groups(ASG) Overview
        - What’s an Auto Scaling Group?
            
            ![[image 38.png]]
            
            - 실생활에선 웹사이트나 어플리케이션에 부하량이 달라질 수 있습니다.
            - 클라우드에선 서버를 순식간에 만들고 제거가 가능합니다.
            
              
            
            - Auto Scaling Group(ASG)의 목표
                - Scale out (EC2 인스턴스 추가)
                - Scale in (EC2 인스턴스 제거)
                - 최소한이면서 최대의 EC2 인스턴스 개수를 실행하고 있는지 보장
                - 자동으로 로드밸런서에 인스턴스를 등록
                - 인스턴스의 상태가 좋지 않을 경우 재생성 (ex: unhealthy)
            - ASG는 무료입니다. (인스턴스 사용량만큼만 비용을 낸다)
        - Auto Scaling Group in AWS
            
            ![[image 1 11.png]]
            
        - Auto Scaling Group Attributes
            
            ![[image 2 9.png]]
            
    - [SAA/DVA] Auto Scaling Groups - Scaling Policies
        - Auto Scaling - CloudWatch Alarms & Scaling
            
            ![[image 3 8.png]]
            
            - CloudWatch Alarms를 통해서 ASG 스케일링이 가능합니다.
            - Alarm은 매트릭을 모니터링합니다. (평균 CPU 사용량이나 Custom Metric 등)
            - 평균 CPU 사용량은 ASG에 속한 모든 인스턴스의 평균 사용량입니다.
            - Alarm을 기반으로 다음과 같은 정책 설정이 가능합니다:
                - scale-out 정책
                - scale-in 정책
        - Auto Scaling Groups - Scaling Policies
            
            ![[image 4 8.png]]
            
            ![[image 5 7.png]]
            
            - 동적 스케일링
                - 타켓 스케일링: 목표하는 수치를 정해놓는 스케쥴링 기법 (ex: CPU 사용량 40% 이하)
                - 간단 스케일링: 이벤트에 대한 인스턴스 수치를 정의 (ex: CPU 사용량 70% 이상이면 인스턴스 2개 증가, CPU 사용량 30% 이하면 인스턴스 1개 감소)
            - 스케쥴 스케일링: 어플리케이션 사용 환경에 따른 사용량을 예측해서 인스턴스 개수를 예상
                - ex: 금요일 5시 이후에 인스턴스 개수 증가
            
            ![[image 6 7.png]]
            
            - 예측 스케일링
                - 지속적으로 현재 사용량을 모니터링하여 사전에 인스턴스 개수를 늘리는 방법
        - Good metrics to scale on
            
            ![[image 7 5.png]]
            
        - Auto Scaling Groups - Scaling Cooldowns
            
            ![[image 8 5.png]]
            
            - 스케일링 액션이 일어나면 쿨다운 상태에 들어간다.(default 설정은 5분)
            - 쿨다운 상태에선 인스턴스에 추가/삭제가 일어나지 않는다. (Metrics 안정화를 기다림)
            - Advice: AMI를 사용하면 환경이 셋업 되어 있기 때문에 cooldown 기간을 줄일 수 있다.
    - ASG for SysOps
        - ASG - Lifecycle Hooks
            
            ![[image 9 5.png]]
            
            - ASG 내에 인스턴스가 시작되면 InService 상태가 됩니다.
            - Pending 상태에서 인스턴스가 InService 상태가 되기 전에 추가적으로 작업을 할 수 있습니다.
                - Pending 상태 내에 인스턴스 시작하면 실행할 스크립트를 정의하세요.
            - Terminating 상태에서 인스턴스가 제거(Terminated)되기 전에 몇 가지 작업을 할 수 있습니다.
                - Terminating 상태에서 인스턴스가 제거 되기 이전에 트러블 슈팅을 할 수 있습니다.
            - 사용 예
                - 클린업(인스턴스가 제거 되기 전에 환경을 클린)
                - 로그 추출
                - 특별한 헬스 체크
            - EventBridge, SNS, SQS와 통합해서 사용 가능합니다.
            
              
            
        - Launch Configuration vs Launch Template
            
            ![[image 10 5.png]]
            
            - 공통점
                - AMI, 인스턴스 타입, 키페어, Security Group 및 인스턴스를 실행하기 위한 여러 매개변수들(tags, EC2 user-data)
                - 둘 다 수정은 불가능
            - Launch Configuration (Legacy):
                - 매 번 재생성해야함
            - Launch Template (Newer):
                - 여러 버전 사용 가능
                - **파라미터 부분 집합**을 만들어 놓으면, 여러 설정들을 재사용하고, 필요할 때마다 기존 템플릿을 상속받아 유사한 환경을 쉽게 구성할 수 있다는 의미입니다.
                - Spot이나 On-Demand를 통해 프로비저닝(인스턴스 생성) 가능
                - AWS에서 현재 지원중
        - SQS with Auto Scaling Group (ASG)
            
            ![[image 11 5.png]]
            
            - SQS의 Queue Length를 기반으로 AutoScaling 하는 방법
            - SQS의 Queue Length가 커지면 CloudWatch Alarm을 트리거해서 AutoScaling 그룹에 Scale 이벤트를 호출할 수 있다.
        - ASG Health Checks
            
            ![[image 12 5.png]]
            
            - 높은 가용성을 확신하기 위해선 최소 2개 인스턴스가 최소 2개 AZ에서 실행되어야 합니다.
            - 헬스 체크
                - EC2 Status Checks
                - ELB Health Checks
                - 커스텀 Health Checks: AWS CLI 또는 AWS SDK를 사용해서 인스턴스의 상태를 ASG에 송신합니다.
            - ASG는 건강하지 않은(unhealthy) 인스턴스를 제거하고 새로운 인스턴스를 실행합니다.
            - ASG는 건강하지 않은 인스턴스를 재시작(reboot)하지 않습니다.
            - CLI에 대해서 알면 좋은 것
                - set-instance-health: custom health checks를 하는 데 사용됩니다.
                - terminate-instance-in-auto-scaling-group: 인스턴스를 ASG에서 제거합니다.
        - Troubleshooting ASG Issues
            
            ![[image 13 5.png]]
            
    - CloudWatch for ASG
        
        ![[image 14 5.png]]
        
        - CloudWatch를 통해서 ASG 매트릭스를 1분마다 수집 가능(Max Size, Min Size, etc…)
    - Auto Scaling Overview
        
        ![[image 15 5.png]]
        
        - AWS DynamoDB와 AWS Aurora
            
            ### 1. **Amazon DynamoDB (Table 또는 Global Secondary Index) - WCU & RCU**
            
            **DynamoDB**는 AWS에서 제공하는 NoSQL 데이터베이스입니다. 데이터의 처리량을 관리하기 위해 **WCU**(Write Capacity Units)와 **RCU**(Read Capacity Units)라는 개념이 사용됩니다.
            
            - **WCU (Write Capacity Unit)**: DynamoDB 테이블에 데이터를 쓸 때의 처리량을 나타냅니다. 1 WCU는 초당 1KB 이하의 데이터를 하나의 아이템으로 기록할 수 있는 용량입니다. 예를 들어, 만약 테이블에 초당 10KB 크기의 데이터를 쓰려면 10 WCU가 필요합니다.
            - **RCU (Read Capacity Unit)**: DynamoDB 테이블에서 데이터를 읽을 때의 처리량을 나타냅니다. 1 RCU는 초당 강력한 일관성(Strong Consistency) 읽기 기준으로 4KB 이하의 데이터를 하나의 아이템으로 읽을 수 있는 용량입니다. 만약 캐시된 데이터를 읽는 Eventually Consistent 방식이라면 1 RCU로 두 배인 8KB 데이터를 읽을 수 있습니다.
            - **Global Secondary Index (GSI)**: 테이블의 기본 키 외에도 다른 속성을 기준으로 쿼리할 수 있게 해주는 보조 인덱스입니다. GSI는 독립적으로 WCU와 RCU를 설정할 수 있습니다. 즉, 테이블과 별도로 GSI에 대한 읽기와 쓰기 용량을 설정할 수 있습니다.
            
            이 개념을 통해 DynamoDB는 예상되는 트래픽에 맞춰 읽기와 쓰기 용량을 미리 설정할 수 있고, 이 용량을 초과할 경우 성능 저하가 발생하거나 비용이 추가될 수 있습니다.
            
            ---
            
            ### 2. **Amazon Aurora - Dynamic Read Replicas Auto Scaling**
            
            **Amazon Aurora**는 MySQL과 PostgreSQL과 호환되는 AWS의 고성능 관계형 데이터베이스 서비스입니다. Aurora는 데이터베이스 성능을 확장할 수 있는 기능들을 제공하는데, 그 중 하나가 **동적 읽기 복제본 자동 확장** 기능입니다.
            
            - **Read Replicas**: Aurora에서는 데이터베이스의 읽기 작업을 분산 처리하기 위해 **읽기 복제본(Read Replicas)**을 만들 수 있습니다. 이를 통해 읽기 성능을 확장할 수 있습니다. 예를 들어, 하나의 마스터 인스턴스에 다수의 읽기 복제본을 추가하면, 읽기 요청을 여러 복제본에 분산시켜 데이터베이스의 성능을 높일 수 있습니다.
            - **Dynamic Auto Scaling**: **동적 자동 확장**은 AWS의 **Auto Scaling** 기능을 사용하여 Aurora의 읽기 복제본을 자동으로 추가하거나 제거하는 기능입니다. 즉, 데이터베이스에 대한 읽기 요청이 많아지면 Aurora는 읽기 복제본을 자동으로 더 생성하여 부하를 분산시키고, 읽기 요청이 줄어들면 불필요한 복제본을 제거하여 비용을 절감할 수 있습니다.
            
            이 기능을 통해, 사용자나 애플리케이션의 트래픽 변동에 맞춰 Aurora 데이터베이스가 자동으로 확장 및 축소되므로, 사용자는 데이터베이스의 성능에 대해 걱정할 필요 없이 비즈니스 로직에 집중할 수 있습니다.
            
            ---
            
            정리하자면:
            
            - **DynamoDB**에서는 WCU와 RCU를 사용하여 처리량을 관리하며, 읽기와 쓰기 용량을 설정해 성능과 비용을 조정합니다.
            - **Aurora**에서는 읽기 복제본을 동적으로 자동 확장하는 기능을 통해 읽기 성능을 최적화하고 필요에 따라 비용을 절감할 수 있습니다.
            
            이 개념들이 **AWS Auto Scaling Group (ASG)**과 연결되는 이유는, 두 서비스 모두 트래픽의 변화에 따라 자동으로 리소스를 확장하거나 축소할 수 있는 **Auto Scaling** 기능을 제공하기 때문입니다.
            

### 핵심 요약

- 핵심 요약 접기
    - Auto Scaling Group (ASG)은 EC2 인스턴스의 수를 자동으로 조정하는 AWS 서비스입니다.
    - ASG는 Launch Template을 사용하여 인스턴스를 생성하며, 이는 여러 버전을 지원하고 재사용이 가능합니다.
    - ASG는 EC2 상태 확인, ELB 헬스 체크, 커스텀 헬스 체크를 통해 인스턴스의 상태를 모니터링합니다.
    - SQS의 대기열 길이를 기반으로 ASG를 조정할 수 있습니다.
    - CloudWatch는 ASG의 성능을 모니터링하고 지표를 제공합니다.
    - DynamoDB는 WCU와 RCU를 통해, Aurora는 동적 읽기 복제본 자동 확장을 통해 Auto Scaling을 구현합니다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 