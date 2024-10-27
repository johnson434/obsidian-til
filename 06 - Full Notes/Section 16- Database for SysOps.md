---
⭕첫 학습날: 2024-09-25
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 1일 복습
🛑첫날: "✏첫날 : 2024/09/25"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤32일째❤
🛑4일후: "🥉4일뒤 : 2024/09/29"
🛑7일후: "🥈7일뒤 : 2024/10/02"
🛑14일후: "🥇14일뒤 : 2024/10/09"
4일후: "@2024년 9월 29일"
4일후(text): 2024/09/29
7일후: "@2024년 10월 2일"
7일후(text): 2024/10/02
14일후: "@2024년 10월 9일"
14일후(text): 2024/10/09
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/09/25
오늘과 첫학습날 사이: "32"
사이: "32"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[Database]]

### 단서 질문

- RDS
    - AWS에서 제공하는 관계형 데이터베이스
    - Postgres, MYSQL, Aurora(AWS가 만듬) 등 다양한 DB 제공

### 핵심 필기

- 전체 내용 접기
    - RDS Overview
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0414.jpg]]
        
        - RDS는 관계형 데이터베이스로 AWS에서 제공한다.
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0415.jpg]]
        
        - RDS는 매니지드 서비스다.
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0416.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0417.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0418.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0419.jpg]]
        
          
        
    - RDS Multi AZ vs Read Replicas
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0420.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0421.jpg]]
        
          
        
    - RDS Multi AZ - Failover Conditions
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0422.jpg]]
        
          
        
          
        
          
        
    - RDS Proxy
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0423.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0424.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0425.jpg]]
        
        - RDS Proxy는 Public Subnet 혹은 Private Subnet 둘 다 위치 가능하다.
        - RDS Proxy를 Private Subnet에 배포하고 싶으면 AWS Lambda 또한, Private Subnet에 배포해야한다.
        
          
        
    - RDS Parameter Groups
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0426.jpg]]
        
          
        
    - RDS Backups and Snapshots
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0427.jpg]]
        
        - Incremental after the first snapshot의 뜻은 첫 번째 snapshot은 데이터베이스의 전체 내용을 저장하고 이후엔 변경된 부분만 저장된다는 뜻이다.
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0428.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0429.jpg]]
        
          
        
    - RDS Events and Logs
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0430.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0431.jpg]]
        
          
        
          
        
          
        
    - RDS & CloudWatch
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0432.jpg]]
        
        - 시험 문제는 매트릭스를 기반으로 퍼포먼스 예측이나 트러블 슈팅이 나옴
        
          
        
    - RDS Performance Insights
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0433.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0434.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0435.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0436.jpg]]
        
          
        
          
        
          
        
    - **Amazon Aurora (시험문제 많이 나오는 중)**
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0440.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0437.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0438.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0439.jpg]]
        
        - **Reader Endpooint (시험 가능성 높음)**: Reader Endpoint로 요청하면 Read Replica로 로드밸런싱이 일어난다. (Statement 레벨이 아니라 Connection 레벨에서 일어남 << 뭔소린지 이해 안감)
        
          
        
    - Amazon Aurora - Backups
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0441.jpg]]
        
          
        
    - RDS & Aurora Security
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0444.jpg]]
        
          
        
    - **Amazon Aurora for SysOps**
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0442.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0443.jpg]]
        
          
        
    - ElasticCache Overview
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0445.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0446.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0447.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0448.jpg]]
        
          
        
    - LeasticCache Redis Cluster Modes
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0449.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0450.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0451.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0452.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0453.jpg]]
        
          
        
    - **ElasticCache Redis for SysOps**
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0454.jpg]]
        
        - Redis Scaling - Cluster Mode를 비활성 상태
        - Horizontal: read Replicas 개수를 조절
        - Vertical: 새로 노드 그룹을 만들고 해당 노드를 가리키도록 DNS 업데이트한다.
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0455.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0456.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0457.jpg]]
        
          
        
    - **ElasticCache Memcached for SysOps**
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0458.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0459.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0460.jpg]]
        
          
        

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 