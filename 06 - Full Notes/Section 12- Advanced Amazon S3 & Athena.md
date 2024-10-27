---
⭕첫 학습날: 2024-10-07
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: false
🧠장기기억: false
복습: 14일 복습
🛑첫날: "✏첫날 : 2024/10/07"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤20일째❤
🛑4일후: "🥉4일뒤 : 2024/10/11"
🛑7일후: "🥈7일뒤 : 2024/10/14"
🛑14일후: "🥇14일뒤 : 2024/10/21"
4일후: "@2024년 10월 11일"
4일후(text): 2024/10/11
7일후: "@2024년 10월 14일"
7일후(text): 2024/10/14
14일후: "@2024년 10월 21일"
14일후(text): 2024/10/21
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/10/07
오늘과 첫학습날 사이: "20"
사이: "20"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[S3]] [[AWS Athena]]

### 단서 질문

- 질문1

### 핵심 필기

- 전체 내용 접기
    - S3 Lifecycle Rules (with S3 Analytics)
        - Moving Between Storage Classes
            
            ![[image 32.png]]
            
            **S3 - Moving Between Storage Classes**
            
            - Object를 Storage Classes 별로 전송 가능하다.
            - 자주 접근 되는 오브젝트는 Standard, IA
            - 아카이빙 오브젝트는 Glancier나 Glacier Deep Archive
            - Lifecycle Rules를 통해 오브젝트 이동은 자동으로 처리 가능
        - Lifecycle Rules
            
            ![[image 1 6.png]]
            
            **AWS S3 - Lifecycle Rules**
            
            - 전송 액션 - 오브젝트를 다른 Storage Class로 변경 가능
                - 예: object를 60일 후에 Standard IA class로 이동하라.
                - 6개월 후에 아카이빙을 위해 Glacier로 이동해라.
            - Expiration Actions - 기간이 지나면 Object 삭제
                - 예: Object의 이전 버전을 삭제
            - Lifecycle Rule은 특정 접두어를 위해 만들 수 있다. (ex: s3://mybucket/mp3/*)
            - Lifecycle Rule은 특정 태그를 위해 만들 수 있다.
        - Lifecycle Rules (Scenario 1)
            
            ![[image 2 6.png]]
            
              
            
              
            
        - Lifecycle Rules (Scenario 2)
            
            ![[image 3 5.png]]
            
              
            
        - Amazon S3 Analytics - Storage Class Analysis
            
            ![[image 4 5.png]]
            
              
            
    - S3 Event Notifications
        - S3 Event Notifications
            
            ![[image 5 5.png]]
            
            - S3 관련 이벤트(Object 생성, 조회, 복구 등)이 있다.
            - S3 이벤트를 수신하면 이벤트 브릿지를 통해서 다른 리소스로 트리거 가능
            - 이벤트 전송에 평균적으로 몇 초정도 걸리지만 가끔은 분 단위보다 길어질 수도 있다.
        - IAM Permissions
            
            ![[image 6 5.png]]
            
            - S3의 이벤트를 수신하기 위해서는 S3가 아닌 수신하는 리소스들에게 IAM 정책이 필요하다.
        - S3 Event Notifications with Amazon EventBridge
            
            ![[image 7 4.png]]
            
              
            
    - S3 Performance
        - ==**S3 - Baseline Performance**==
            
            ![[image 8 4.png]]
            
            - 프리픽스를 기준으로 초당 3,500 PUT/COPY/POST/DELETE나 5,500 GET/HEAD 리퀘스트를 보낼 수 있다.
        - ==**S3 Performance**==
            
            ![[image 9 4.png]]
            
            - 파일을 빠르게 전송하기 위한 2가지 방법이 있다.
            
              
            
            1. Multi-Part upload
                1. 파일 크기는 5GB를 넘어야 한다.
                2. 분할 파일 크기 > 100MB
                3. 총 크기 > 5GB
                4. 파일을 병렬적으로 동시에 전송한다.
            2. S3 Transfer Acceleration
                1. 파일을 수신자의 region 근처에 있는 AWS Edge Location에 캐싱하여 파일 전송을 빠르게 한다.
        - ==**S3 Performance - S3 Byte-Range Fetches**==
            
            ![[image 10 4.png]]
            
            - GET 요청을 병렬적으로 처리 가능하다.
            - 실패해도 회복력이 좋다.
            - File 전체를 병렬적으로 요청하거나 헤더만 부분 요청이 가능하다.
        - S3 Select & Glacier Select
            
            ![[image 11 4.png]]
            
              
            
    - S3 Batch Operations
        
        ![[image 12 4.png]]
        
        - 암호화되지 않은 오브젝트 암호화는 시험에 나올 수도 있음.
        - S3 Inventory를 사용해서 object 리스트를 조회한다.
        
          
        
    - S3 Inventory
        
        ![[image 13 4.png]]
        
        - S3 List API를 사용해서 Object를 모두 나열하는 것보다는 S3 Inventory를 통해서 메타데이터를 조회할 수 있다.
    - S3 Glacier Overview
        - Amazon S3 Glacier
            
            ![[image 14 4.png]]
            
            - 저비용 아카이빙 백업용 저장소
            - 데이터가 10년은 유지되어야 하는 것들
            - 온프로미스 마그네틱 하드드라이브의 대체품
            - 한달 0.004/GB - Standard | 0.00099/GB Deep Archive
            - Glacier의 저장소를 Vault라 하고 Vault에 저장되는 객체를 Archive라고 한다. Archive는 최대 40GB다.
            - 기본 설정으로 모든 데이터는 AES-256을 통해 암호화된다.
            - 만약, XXX일이 지난 후에 아카이빙이 필요하면 Glacier를 써라.
        - Amazon S3 Glacier Operations
            
            ![[image 15 4.png]]
            
            볼트에서 가능한 작업(Operation)은 3가지가 있다.
            
            - Create & Delete: 삭제는 볼트 내부가 비었을 때만 가능
            - Retrieving Metadata:
        - Valut Policies & Vault Lock
            
            ![[image 16 4.png]]
            
            - 볼트별로 access 정책과 lock 정책이 있다.
            - Vault Policy는 Bucket Policy와 비슷하다.(접근 유저 제한, 계정 권한)
            - Vault Lock Policy는 변경 불가능하다.
            
              
            
    - Glacier Vault Lock
        - Glacier - Notifications for Restore Operations
            
            ![[image 17 4.png]]
            
            - Vault Notification 설정을 통해서 Retrieve가 끝나거나 시작됐을 때 알림을 받을 수 있다.
    - S3 Multi-Part Upload Deep Dive
        
        ![[image 18 4.png]]
        
        - **라이프사이클 정책을 통해 자동으로 실패한 파일들을 삭제할 수 있다.**
    - Athena
        - Amazon Athena
            
            ![[image 19 4.png]]
            
            **S3 Anthena**
            
            - S3 데이터 분석을 위한 서버리스 쿼리서비스
            - 내부적으로 SQL을 사용하는 Presto Engine을 사용한다.
            - 요금은 5$ per TB
            - Amazon Quicksight를 이용해서 Athena로 수집한 데이터를 리포팅하고 대시보드화 시킬 수 있다.
            - S3 데이터 분석을 위한 서비스이지만 Federated Query 등을 사용해서 S3가 아닌 다른 리소스(AWS or 온프로미스)에서도 SQL을 사용해 검색이 가능하다.
        - Athena - Performance Improvement
            
            ![[image 20 4.png]]
            
            - columnar data를 사용한다. (컬럼 명시해서 더 적은 데이터 스캔)
                - Apache Parquet이나 ORC 형식을 사용한다.
                - 엄청 퍼포먼스가 많이 상승한다.
                - Parquet이나 ORC로 전환하는데 Glue를 사용해라
                - 데이터를 압축해라
                - 데이터셋을 이지쿼리로 파티션해라.
                - 더 큰 파일을 사용해라.
        - Amazon Athena - Federated Query
            
            ![[image 21 4.png]]
            
            - Federated(통합 연합?) Query
            - SQL을 관계형, 비관계형, 오브젝트, 커스템 데이터 소스 등에 사용할 수 있다.(AWS or on-premises)
            - Athena에서 AWS 람다를 호출하고 람다에서 Federated Queries를 사용한다.
            - 결과는 S3에 저장한다.

### 핵심 요약

- 핵심 요약 접기
    
    • S3 Lifecycle Rules: Automate moving objects between storage classes or deleting them after specified time periods.
    
    • S3 Event Notifications: Trigger actions in response to object-level operations in S3 buckets.
    
    • S3 Performance: Utilize Multi-Part upload and S3 Transfer Acceleration for faster file transfers.
    
    • S3 Batch Operations: Perform large-scale batch operations on S3 objects.
    
    • S3 Glacier: Low-cost storage for data archiving and long-term backup.
    
    • Athena: Serverless query service for analyzing data stored in S3 using SQL.
    
    • Athena Federated Query: Allows querying data from various sources beyond S3 using SQL.
    

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 