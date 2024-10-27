---
⭕첫 학습날: 2024-10-22
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 1일 복습
🛑첫날: "✏첫날 : 2024/10/22"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤5일째❤
🛑4일후: "🥉4일뒤 : 2024/10/26"
🛑7일후: "🥈7일뒤 : 2024/10/29"
🛑14일후: "🥇14일뒤 : 2024/11/05"
4일후: "@2024년 10월 26일"
4일후(text): 2024/10/26
7일후: "@2024년 10월 29일"
7일후(text): 2024/10/29
14일후: "@2024년 11월 5일"
14일후(text): 2024/11/05
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/10/22
오늘과 첫학습날 사이: "5"
사이: "5"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[High Availability]] [[Disaster Recovery]]

### 단서 질문

- 질문1

### 핵심 필기

- 전체 내용 접기
    - AWS DataSync
        - AWS DataSync
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0538.jpg]]
            
            **AWS DataSync**
            
            - 대용량 데이터를 이전하는 방법
                - 온프로미스 / 클라우드: 에이전트가 온프로미스나 클라우드 둘 중에 하나라도 있어야 한다.(데이터를 지속적으로 이전하기 위해서)
                - AWS 서비스 ↔ 다른 AWS 서비스: 에이전트가 필요 없다.
            - 다음과 같은 서비스에 동기화가 가능하다.
                - Amazon S3
                - Amazon EFS
                - Amazon FSx
            - 데이터 복제 작업은 지속적으로 동작하지 않으며 매 시간, 매일, 매주 간격으로 스케쥴링 된다.
            - 파일 권한이랑 메타데이터가 보존되는 유일한 서비스임 (NFS POSIX, SMB…)
            - 에이전트의 최대 대역폭은 10Gbps이며 대역폭 제한을 둘 수 있다.
        - AWS DataSync NFS / SMB to AWS (S3, EFS, FSx…)
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0539.jpg]]
            
            **AWS DataSync NFS / SMB to AWS**
            
            - 온프로미스에서 AWS에 데이터를 이전하기 위해선 AWS DataSyncAgent를 설치해야 합니다.
            - 온프로미스의 NFS 서버 ↔ AWS DataSyncAgent ↔ AWS DataSync Service ↔ AWS Storage Resources
        - AWS DataSync Transfer between AWS Storage Services
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0540.jpg]]
            
              
            
    - AWS Backup
        - AWS Backup (1)
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0541.jpg]]
            
            **AWS Backup**
            
            - 완전 관리형 서비스
            - 중앙 관리 자동화가 된다.
            - 직접 스크립트를 작업하거나 프로세스를 만들 필요가 없다.
            - 지원하는 서비스 목록
                - EC2 / EBS
                - S3
                - RDS (모든 DB 엔진) / Aurora / DynamoDB
                - Document DB / Neptune
                - EFS / FSx (Lustre & Window File Server)
                - AWS Storage Gateway (Volume Gateway)
            - cross-region 백업 지원
            - cross-account 백업 지원
        - AWS Backup (2)
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0542.jpg]]
            
            **AWS Backup**
            
            - PITR(Point In Time Recovery)을 지원한다.
            - 요청 시나 스케쥴링 시에 백업 가능하다.
            - 태그 기반으로 백업 정책 설정 가능하다.
            - Backup Plans는 백업 계획으로 이 정책을 통해 백업이 가능하다.
                - 백업 주기
                - 백업 윈도우 (백업 작업이 실행 되는 시간 창을 의미한다. 예: 오후 10시 ~오전 6시 가이)
                - 트랜지션 to Cold Storage (백업 데이터를 비용이 저렴한 저장소로 전송)
                - 리텐션 기간(백업 데이터를 얼마나 오래동안 유지할지)
        - AWS Backup Flow
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0543.jpg]]
            
              
            
        - AWS Backup Vault Lock
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0544.jpg]]
            
            **AWS Backup Vault Lock**
            
            - AWS Backup Vault에 들어간 백업들은 WORM 상태를 강제 당한다.
            - 방어를 위한 추가 레이어가 백업을 다음과 같은 상황에서 지켜준다.
                - 부주의하거나 악의있는 삭제 작업
                - 백업 보유 기간을 줄이거나 변경하는 일
            - 루트 유저도 Vault Lock이 걸려 있으면 삭제할 수 없다.

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 