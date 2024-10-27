---
⭕첫 학습날: 2024-09-28
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
⭕학습정도: 🤔중
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: false
복습: 추가 복습
🛑첫날: "✏첫날 : 2024/09/28"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤29일째❤
🛑4일후: "🥉4일뒤 : 2024/10/02"
🛑7일후: "🥈7일뒤 : 2024/10/05"
🛑14일후: "🥇14일뒤 : 2024/10/12"
4일후: "@2024년 10월 2일"
4일후(text): 2024/10/02
7일후: "@2024년 10월 5일"
7일후(text): 2024/10/05
14일후: "@2024년 10월 12일"
14일후(text): 2024/10/12
오늘1: "@2024년 10월 27일 오후 1:59"
오늘2: 2024/10/27
첫학습날text: 2024/09/28
오늘과 첫학습날 사이: "29"
사이: "29"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[AWS Lambda]]

### 단서 질문

- EC2 vs Lambda
    1. EC는 지속적으로 서버에서 돌아가지만 Lambda는 함수를 한 번 실행할뿐 서버를 점유하고 있지 않는다.
    2. Lambda는 시간 제한이 있다.
    3. Lambda는 오토스케일링이 자동으로 된다.
- Lambda의 CPU 스펙을 향상 시키는 방법은?
    
    RAM 사이즈를 키우면 CPU와 네트워크 성능이 알맞게 향상된다.
    
- Lambda는 어떻게 실행되는가?
    
    해당 코드가 실행될 컨테이너(JS면 NodeJS, Python이면 Python)에서 해당 코드가 실행됩니다.
    
- Lambda를 사용할 수 없는 경우는?
    
    함수 실행 시간이 15분 이상인 경우. (최대 시간 제한이 15분임)
    
- EventBridge란?
    
    EventBridge란 이벤트 버스 역할을 하며 서로 다른 AWS 서비스끼리 유기적으로 동작하게 만듭니다. 예를 들어, S3의 파일이 업로드 되면 EventBridge가 이 이벤트를 관찰하고 있다면 특정 행동(Lambda를 호출, SQS로 메시지 전달)이 트리거 됩니다.
    
- DynamoDB란?
    
    **DynamoDB**는 AWS에서 제공하는 **서버리스 기반 Key-Value NoSQL 데이터베이스**입니다.
    
    **DynamoDB**를 사용하면 높은 성능과 비용적인 측면에서 이점을 가져올 수 있습니다.
    
- AWS X-Ray란?
    
    분산 애플리케이션의 성능 추적을 위한 **서비스**로 함수 호출 시간, 실행에 걸리는 시간 등을 측정해서 CloudWatch에 제공한다.
    
- Lambda Execution Context란?
    
    Lambda 실행 환경(Runtime Environment)입니다. Lambda의 실행되기 전에 해당 함수가 다시 호출되면 WarmStart로 해당 Execution Context 재사용이 가능합니다.
    
- Lambda 함수를 처음 호출할 때 Latency를 줄이는 방법은?
    1. Lambda 함수를 주기적으로 실행해서 Cold Start를 방지
    2. **Provisioned Concurrency 설정을 통해 미리 Lambda를 예약해놓는다.**

### 핵심 필기

- 전체 내용 접기
    - Lambda - Overview
        - Why AWS Lambda
            
            ![[image 6.png]]
            
            **EC2**
            - Cloud의 가성 서버다.
            - RAM과 CPU가 제한된다.
            - EC2는 서버가 계속 돌아가는 상태다.
            - 스케일링은 서버의 개수를 조절하는 것
            
            **Lambda**
            
            - 가상 함수로 서버를 관리할 필요가 없다.
            - 시간 제한이 있다.
            - On-Demand로 실행된다.
            - 스케일링이 자동이다. (EC2는 ASG 그룹을 통해서 지원)
        - Benefits of AWS Lambda
            
            ![[image 1 3.png]]
            
            - 쉬운 가격 정책
                - 리퀘스트와 Compute time으로 요금 청구
            - 많은 AWS 서비스와 통합해서 사용 가능하다.
            - 많은 프로그래밍 언어와 통합해서 사용 가능하다.
            - RAM 크기를 증가시키면 CPU와 네트워크도 향상된다.
        - AWS Lambda Language support
            
            ![[image 2 3.png]]
            
            **AWS Lambda 지원 언어**
            
            - Python, Java 등 다양한 언어
            - Lambda Container Image
                - Lambda Runtime API를 구현하는 Container Image를 사용 가능하다.
                - 단, 임의의 Docker Image 실행하는데는 보통 ECS/Fargate가 선호된다.
        - AWS Lambda Integrations Main ones
            
            ![[image 3 2.png]]
            
              
            
        - Example: Serverless Thumbnail creation
            
            ![[image 4 2.png]]
            
              
            
        - Example: Serverless CRON Job
            
            ![[image 5 2.png]]
            
            - EventBridge는 AWS의 리소스들을 이벤트를 통해 연결
        - AWS Lambda Pricing: example
            
            ![[image 6 2.png]]
            
            - Lambda의 비용 정책은?
                - 호출 마다
                    - 1,000,000회는 무료이며 이후부턴 백만 번마다 $0.20 비용이 든다.
                - 지속 시간으로
                    - 한 달에 400,000 GB-seconds는 무료다.
                    - 만약, 1GB면 400,000초 호출 가능
                    - 만약, 128mb면 3,2000,000초
                    - 무료 사용이 끝나면 600,000GB-seconds당 $1.00
    - Lambda & CloudWatch Events / EventBridge
        - CloudWatch Events / EventBridge
            
            ![[image 7.png]]
            
            - CRON이나 Rate로 EventBridge Rule을 설정해서 특정 주기로 Lambda 실행하기
            - CodePipeline을 관찰하다가 변경되면 Lambda 실행하기
    - Lambda & S3 Event Notifications
        - S3 Events Notifications
            
            ![[image 8.png]]
            
            - 만약, Non-versioned object에 2개 이상 파일 쓰기 요청이 들어오면 이벤트가 한 개만 전달 될 수도 있다.
            - 이러한 동일한 오브젝트에 쓰기 요청이 성공할 때마다 이벤트를 전달하고 싶으면 S3 Bucket에서 Object Versioning 옵션을 활성화해라. (파일의 버전이 생성됨)
        - Simple S3 Event Pattern - Metadata Sync
            
            ![[image 9.png]]
            
              
            
    - Lambda Permissions - IAM Roles & Resource Policies
        - Lambda Execution Role (IAM Role)
            
            ![[image 10.png]]
            
            - 람다에게 AWS 서비스나 리소스에 접근할 수 있는 권한을 부여
            - 제일 좋은 설정 방법은 Lambda 별로 Execution Role을 하나씩 주는 것입니다.
            - 이벤트 소스 매핑을 사용하여 람다를 호출할 때 람다는 event data를 읽기 위해 Execution Role을 사용합니다.
        - Lambda Resource Based Policies
            
            ![[image 11.png]]
            
            - IAM Principal이 Lambda 함수에 접근하려면:
                - **IAM 정책**이 해당 Principal에게 접근을 허용해야 하거나
                - **리소스 기반 정책**이 Lambda 함수에 대해 해당 Principal 또는 다른 AWS 서비스를 허용해야 합니다.
    - Lambda Monitoring & X-Ray Tracing
        - Lambda Logging & Monitoring
            
            ![[image 12.png]]
            
            - CloudWatch Logs
                - 람다 실행 로그는 CloudWatch Logs에 기록된다.
                - 람다가 로그를 작성하기 위해선 CloudWatch Execution Role이 있어야 한다.
            - CloudWatch Metrics
                - 호출, 지속시간, 동시 실행, 에러 횟수, 성공 비율, Throttle이 포함된다.
                - Async Delivery Failures: 비동기 호출 실패
                - Iterator Age: 반복 주기
            
            > [!important]  
            > Throttle이란? 엔진 등의 과부하를 막기 위해서 출력을 조절하는 것을 스로틀링이라고 한다. AWS Lambda에선 여러 번 호출되는 함수를 특정 시간동안 함수의 호출을 멈춰서 함수의 실행 횟수를 조절한다.  
            
        - Lambda Tracing with X-Ray
            
            ![[image 13.png]]
            
            - X-Ray는 함수 호출 시간, 실행에 걸리는 시간 등을 측정하는 서비스다.
                - Lambda 설정에서 Active Tracing을 켜는 것으로 사용 가능
                - X-Ray SDK를 Lambda 코드 내에 작성해야 합니다.
    - Lambda Function Performance
        - Lambda Function Configuration
            
            ![[image 14.png]]
            
            RAM
            
            - 128MB부터 10GB까지 1MB 단위로 늘릴 수 있다.
            - RAM의 크기를 늘리면 vCPU와 네트워크가 향상된다.
            - 1,792MB는 vCPU 1개와 동일하다.
            - 따라서, 만약 1,792MB 이상 램을 사용하면 멀티스레딩 사용이 효율적일 수 있다.
            
            시간제한
            
            - 3초부터 15분까지
        - Lambda Execution Context
            
            ![[image 15.png]]
            
            - Execution Context는 람다 함수를 호출하는 런타임 환경입니다.
            - DB 커넥션이나 HTTP Client 설정, SDK Client 설정을 한다.
            - Lambda 함수 호출이 다시 될 것을 예상해서 환경의 값을 유지하기도 합니다.
            - Lambda가 다시 호출되면 이전 Context를 재사용할 수 있습니다.
            - Execution Context엔 /tmp 디렉터리가 포함됩니다.
        - Initialize outside the handler
            
            ![[image 16.png]]
            
            - Lambda를 사용할 때는 커넥션과 같은 유지되어야 할 설정들은 Top Level에 정의할 것
        - Lambda Functions /tmp space
            
            ![[image 17.png]]
            
            - 최대 크기는 10GB
            - /tmp 디렉터리를 암호화하기 위해서는 KMS Data Keys를 사용하세요
    - Lambda Concurrency
        - Lambda Concurrency and Throttling
            
            ![[image 18.png]]
            
            - 동시에 1000개 실행 가능
            - reserved concurrency 설정이 가능하다.
            - 제한을 넘는 호출은 Throttle을 호출한다.
            - Throttle이 발생했을 때 처리 방식
                - Lambda 함수가 동기라면 ⇒ ThrottleError를 던진다.
                - Lambda 함수가 비동기라면 ⇒ SQS의 DLQ로 간다.
        - Lambda Concurrency Issue
            
            ![[image 19.png]]
            
            - 만약, Limit를 넘는 요청이 들어오면 다른 유저들은 Throttle을 겪는다.
        - Concurrency and Asynchronous Invocations
            
            ![[image 20.png]]
            
            - 실패한 람다함수는 최대 6시간동안 재시도된다.
            - 재시도 주기는 1초부터 5분까지다.
        - Cold Starts & Provisioned Concurrency
            
            ![[image 21.png]]
            
            AWS 람다는 컨테이너 기반으로 동작한다. 첫 호출이 오면 컨테이너를 만들고 람다를 실행한다.
            
            - Cold Start
                - 새로 인스턴스를 생성하면 코드가 메모리에 올라가고 handler 바깥 부분이 실행된다. (init)
                - 따라서, 첫번째 요청은 지연성이 크다.
            - Warm Start
                - 람다 함수가 실행이 끝나기 이전에 재호출되는 경우에 handler 내부에 부분만 실행된다.
            - Provisioned Concurrency
                - 람다 함수가 호출되기 전에 람다를 준비시켜 놓는다.
                - 따라서, Cold Start는 발생하지 않으므로 낮은 Latency를 가진다.
            - Note
                - VPN 내에서 Cold Start는 2019년 이후로 확 줄었다.
        - Reserved and Provisioned Concurrency
            
            ![[image 22.png]]
            
            - Reserved Concurrency는 동시성에 Limit 제한 설정
            - Provisioned Concurrency는 Cold Start를 방지하기 위해 미리 Lambda 프로비저닝을 해놓는 것
    - Lambda Monitoring - Extras
        - CloudWatch Metrics
            
            ![[image 23.png]]
            
              
            
            ![[image 24.png]]
            
              
            
        - Lambda Monitoring - CloudWatch Alarms
            
            ![[image 25.png]]
            
              
            
        - CloudWatch Logs
            
            ![[image 26.png]]
            
              
            
        - CloudWatch Logs Insights
            
            ![[image 27.png]]
            
              
            
            ![[image 28.png]]
            
              
            
              
            
        - Lambda Insights
            
            ![[image 29.png]]
            
              
            
              
            

### 핵심 요약

- 핵심 요약 접기
    - 람다는 요청 시에 컨테이너를 생성 후에 함수를 실행한다.
    - 함수가 실행을 끝마치고 종료되면 컨테이너가 제거됩니다.
    - 컨테이너가 제거 되기 이전에 람다 함수를 다시 한 번 호출하면 해당 컨테이너를 제거하지 않고 해당 컨테이너를 재사용합니다.(Warm Start)
    - 탑 레벨에 선언한 요소들은 다시 호출되지 않으며, 함수 내부만 다시 호출됩니다.
    - 만약, 컨테이너가 제거 되었다면 다시 컨테이너를 재생성하므로 속도가 느립니다.(Cold Start)
    

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 