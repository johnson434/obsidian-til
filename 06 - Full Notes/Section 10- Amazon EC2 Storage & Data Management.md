---
⭕첫 학습날: 2024-10-02
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
⭕학습정도: 😀상
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: false
복습: 장기기억
🛑첫날: "✏첫날 : 2024/10/02"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤25일째❤
🛑4일후: "🥉4일뒤 : 2024/10/06"
🛑7일후: "🥈7일뒤 : 2024/10/09"
🛑14일후: "🥇14일뒤 : 2024/10/16"
4일후: "@2024년 10월 6일"
4일후(text): 2024/10/06
7일후: "@2024년 10월 9일"
7일후(text): 2024/10/09
14일후: "@2024년 10월 16일"
14일후(text): 2024/10/16
오늘1: "@2024년 10월 27일 오후 1:59"
오늘2: 2024/10/27
첫학습날text: 2024/10/02
오늘과 첫학습날 사이: "25"
사이: "25"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024 ]] [[EC2]]

### 단서 질문

- 인스턴스 부팅 볼륨으로 사용 가능한 볼륨은 뭐가 있을까?
    - gp2/gp3
    - io1/io2
- EBS 볼륨 사이즈 조절은 가능한가?
    
    크기를 늘릴 수만 있다.
    
- EBS Volume gp2와 gp3의 차이점은?
    
    gp3는 IOPS와 throughput 스펙을 별개로 설정할 수 있다.
    
- EBS Volume snapshot을 빨리 사용할 수 있는 방법은?
    
    snapshot은 S3에 저장되며 처음 접근은 지연이 발생한다. 따라서, dd 명령어나 fio 명령어로 인위적으로 block을 활성화하거나 FSR 옵션을 켜서 활성화한다. 단, FSR은 비쌈(분당 요금)
    
- EFS vs EBS vs Instance Store
    - EFS와 EBS 모두 네트워크 드라이브 반면에, Instance Store은 실제로 물리적 하드디스크를 대여
    - EFS는 여러 AZ에서 동시에 사용 가능

### 핵심 필기

- 전체 내용 접기
    - EBS Overview
        - What’s an EBS Volume
            
            ![[image 30.png]]
            
            **EBS Volume이란?**
            
            - 인스턴스에 붙일 수 있는 네트워크 드라이브다.
            - 인스턴스가 제거되더라도 EBS 내용은 유지된다.
            - 동시에 여러 EC2 인스턴스에 붙일 수 있다.
            - 특정 AZ에 묶여있다. (서브넷 내에서 네트워크 통신을 통해 제공되므로)
            
              
            
            - 프리티어: 30GB SSD 사용 가능
        - EBS Volume
            
            ![[image 1 4.png]]
            
            - 네트워크 드라이브다. (물리적 드라이브가 아니다)
                - 인스턴스와 네트워킹을 통해 연결된다. → Latency가 있다.
            - 특정 AZ 존에 고정되어 있다.
                - 볼륨을 옮기려면 스냅샷을 찍고 새로 만들어야 한다.
            - 프로비저닝된 Capacity가 있다.
                - 프로비전된 용량만큼 요금이 부과된다.
        - EBS Volume - Example
            
            ![[image 2 4.png]]
            
              
            
    - EC2 Instance Store
        
        ![[image 3 3.png]]
        
        - EBS Volume은 네트워크 드라이브로 괜찮은 성능이지만 한계가 있다. 그럴 땐 EC2 Instance Store를 사용하라
        
          
        
        EC2 Instance Store
        
        - 네트워크 드라이브가 아닌 EC2에 직접 부착된 물리 드라이브다.
        - I/O 성능이 더 좋다.
        - EC2 Instance Store가 멈추면 데이터를 잃는다. (임시데이터)
        - 버퍼, 캐시, 데이터 스크래치, 임시 컨텐츠에 좋다.
        - 하드웨어가 실패하면 데이터를 잃을 수 있다.
        - 백업이랑 Replication은 당신의 책임이다.
        
        ![[image 4 3.png]]
        
          
        
    - EBS Volume Types Deep Dive
        
        - EBS Volume Types
            
            ![[image 5 3.png]]
            
            - 부팅 볼륨으로는 gp2/gp3와 io1/io2만 사용 가능하다.
        - EBS Volume Types Use cases **General Purpose SSD (e.g. gp3, gp2)**
            
            ![[image 6 3.png]]
            
              
            
        - EBS Volume Types Use cases **Provisioned IOPS (PIOPS) SSD (e.g. io1, io2)**
            
            ![[image 7 2.png]]
            
            - iops 퍼포먼스가 중요한 앱에서 사용한다.
            - 16,000 IOPS 이상을 요구하는 앱에서 사용한다.
            - 데이터베이스 작업에 좋다.
            - 멀티 attach 가능
        - EBS Volume Types Use cases **Hard Disk Drives HDD (e.g. st1, sc1)**
            
            ![[image 8 2.png]]
            
            - 부트 볼륨으로 사용 불가능
            - 처리량 최적화 HDD (st1)
                - 빅데이터, 데이터웨어하우스, 로그 작업
                - 최대 처리량은 500 MiB/s - max IOPS 500
            - Cold HDD (sc1)
                - 드물게 접근되는 데이터들을 저장
                - 비용이 제일 적은 시나리오에서 사용
                - 최대 처리량은 250 MiB/s - max IOPS 250
        
        ![[image 9 2.png]]
        
    - EBS Multi Attach
        
        ![[image 10 2.png]]
        
        - io1/io2를 여러 인스턴스에 동시에 부착하는 것
        - 사용 예시:
            - 고가용성 클러스터 리눅스 어플리케이션
            - 동시에 쓰기가 필요한 어플리케이션
        - 최대 16개 인스턴스에 붙일 수 있다.
        - cluster-aware 파일시스템을 써야한다.
    - EBS Operation: Volume Resizing
        
        ![[image 11 2.png]]
        
        - EBS Volume은 size랑 IOPS를 늘릴 수만 있다.
        - 사이즈를 늘린 후에는 리파티션이 필요하다.
        - 리사이즈 후에는 Volume은 Optimisation 상태에서 오랜 시간이 걸린다. 단, 볼륨은 이 중에도 사용이 가능하다.
        - 볼륨 크기를 줄이기 위해서는 더 작은 볼륨을 만들고 데이터를 이전해야 한다.
    - EBS Operation: Snapshots
        - EBS Snapshots
            
            ![[image 12 2.png]]
            
            - Volume을 Detach 하지 않고도 snapshot을 찍을 수 있다.
        - Amazon Data Lifecycle Manager
            
            ![[image 13 2.png]]
            
            **Amazon Data Lifecycle Manager**
            
            - EBS snapshot과 EBS-backed AMI 제어를 라이프사이클에 따라 자동화한다.
            - 백업, 스냅샷을 다른 계정으로부터 복제, 기한 지난 백업을 삭제 등을 **스케쥴링**한다.
            - DLM 외부에서 만들어진 snapshot과 AMI는 관리하지 못한다.
            - EC2 Instance-Store backed AMI는 관리하지 못한다.
        - Fast Snapshot Restore (FSR)
            
            ![[image 14 2.png]]
            
            Fast Snapshot Restore (Fast Snapshot Restore)
            
            - EBS 스냅샷은 S3에 저장됩니다.
            - 디폴트 설정으로 입출력 작업을 처음 할 때(각 블록에 처음 접근할 때)는 지연(latency)가 발생합니다. (Block을 S3로부터 Pull해야 하므로)
            - 해결책: dd나 fio 명령어로 init하거나 FSR 옵션을 킨다.
                - dd와 fio는 볼륨 성능을 측정하는 커맨드로 실행하면 전체 볼륨에 한번씩 접근이 일어난다.
            - FSR은 초기화된 snapshot을 사용해서 볼륨을 만듭니다. (블록이 초기화를 통해 i/o latency를 없앱니다.)
            - 특정 AZ에 있는 snapshot에서 사용 가능합니다. (분당 요금을 청구하며 굉장히 비쌉니다.)
                - snapshot 자체는 특정 Region에 저장되며, FSR 활성화도 Region에서 진행하지만 FSR 활성화는 특정 AZ에서 진행됩니다.
                - 왜냐하면 실제로 사용할 저장장치를 초기화 해놓아야 하는데 이는 실제 기기를 사용하므로 특정 AZ에 종속 되는 것입니다. (만약, Region이 범위가 되려면 해당 Region 전체에 초기화된 볼륨이 있어야 하므로 비용이 말도 안되게 비쌀 거다.)
            - DLM을 통해 만들어진 snapshot에서 FSR을 활성화할 수 있습니다.
        - EBS Snapshots Features
            
            ![[image 15 2.png]]
            
            **EBS Snapshots 특징**
            
            - EBS Snapshot Archive
                - Archive Tier는 일반 Snapshot보다 75% 저렴하다.
                - 아카이브 된 스냅샷을 되찾는데는 24~72시간이 걸린다.
            - Recycle Bin for EBS Snapshots
                - 삭제해도 일정 기간동안 snapshot이 남아있는다.
                - 기간을 설정 가능하다. (1일~1년)
    - EBS Operation: Volume Migration
        
        ![[image 16 2.png]]
        
          
        
    - EBS Operation: Volume Encryption
        
        ![[image 17 2.png]]
        
        **EBS Encryption**
        
        - 암호화된 EBS Volume을 만들면 다음과 같은 내용이 따라온다.
            - Volume 내에 데이터는 암호화된다.
            - 볼륨에서 인스턴스끼리 데이터를 주고 받을 때 데이터들은 암호화된다.
            - 모든 스냅샷은 암호화된다.
            - 모든 볼륨은 스냅샷을 통해 만들어진다.
        - 암호화와 복호화는 자동으로 핸들링된다. (사용자가 설정할 필요x)
        - 암호화는 지연성에 영향을 최소한으로 준다.
        - EBS Encryption은 KMS 키를 통해 진행된다.
        - 암호화되지 않은 스냅샷을 암호화할 수 있다.
        
        ![[image 18 2.png]]
        
        - 스냅샷을 만든다.
        - 스냅샷의 복사본을 만든다. (암호화 옵션을 키고)
        - 스냅샷으로부터 볼륨을 만든다.
        - 볼륨을 인스턴스에 붙인다.
        - 쨘! 암호화된 EBS Volume을 사용하는 인스턴스가 된다.
        - 쇼트컷으로는 snapshot에서 create volume from snapshot으로 volume을 만들 때 암호화 옵션만 걸면 된다.
    - Amazon EFS
        - Elastic File System (1)
            
            ![[image 19 2.png]]
            
            Amazon EFS (Elastic File System)
            
            - 여러 EC2 인스턴스에 동시에 마운트 가능한 관리형 NFS (Network File System)이다.
            - EFS는 멀티 AZ에서 동작한다.
            - 높은 가용성, 확장성, 비용 3x gp2 (General Purpose SSD의 3배), 사용한 만큼 비용을 낸다.
        - Elastic File System (2)
            
            ![[image 20 2.png]]
            
            - EFS 사용 예
                - content Management
                - web serving
                - data sharing
                - Wordpress
            - NFSv4.1 프로토콜을 사용한다.
            - EFS 접근 제어엔 Security Group을 사용한다.
            - KMS를 통해 암호화한다.
            
              
            
            - 스탠다드 파일 API를 가지는 POSIX file System (~Linux)을 사용한다.
            - 파일시스템은 자동으로 확장하고, 공간 설정이 없다. 또한, 사용한 만큼 비용을 낸다.
        - Performance & Storage Classes
            
            ![[image 21 2.png]]
            
            **EFS - Performance & Storage Classes**
            
            - EFS Scale
                - 동시에 1000개 NFS Client를 가지며 10GB+/s 대역폭을 가진다.
                - 페타바이트 크기까지 늘어날 수 있다.
            - 퍼포먼스 모드 (EFS 만들 때 설정한다.)
                - General Purpose (default): 지연성에 민감한 경우의 사용한다. (web server, CMS, etc…)
                - Max I/O: 더 높은 지연성, 대역폭, 높은 병렬성 (빅데이터, 미디어 처리)
                    - 병렬 처리에 중점을 두기 위해서 I/O를 높인다. 따라서, 지연성이 더 클 수도 있다.
            - 처리량 모드
                - Bursting: 50MB/s ~ 100MB/s
                - Provisioned:
                - Elastic: 처리량이 자동으로 설정된다.
        - EFS - Storage Classes
            
            ![[image 22 2.png]]
            
            **EFS - Storage Classes**
            
            - Storage Tiers (Lifecycle Management feature - move file after N days)
                - Standard: 자주 접근되는 파일용
                - Infrequent access (EFS-IA): 파일 복구에 돈이 든다. 대신 저장 비용이 더 저렴하다.
                - Archive: 아주 가끔 접근되는 데이터들 (년에 몇 번), 50% 저렴하다.
                - 라이프사이클 정책을 통해서 파일들의 Storage Tier를 변경 가능하다.
            - Availability and Durability
                - Standard: 멀티AZ
                - One Zone: One AZ에 저장한다. dev 환경에 사용하며 백업은 자동으로 된다. IA랑 같이 사용 가능하다. (EFS One Zone-IA)
            - Storage Class를 통해 90%까지 비용을 아낄 수 있다.
    - EFS vs EBS
        - EBS vs EFS - Elastic Block Storage(1)
            
            ![[image 23 2.png]]
            
            **EBS vs EFS**
            
            - EBS volumes
                - 인스턴스 1개 (단, io1/io2는 멀티 attach 가능)
                - 특정 AZ에 한정된다.
                - gp2: 디스크 사이즈가 증가하면 IO도 증가한다.
                - gp3 & io1: io를 독립적으로 증가시킬 수 있다.
            - 인스턴스의 Root EBS Volumes은 기본적으로 EC2 인스턴스가 제거 되면 제거된다.
            - 여러 AZ에 존재하는 인스턴스에 동시에 마운트가 가능하다.
        - EBS vs EFS - Elastic Block Storage(2)
            
            ![[image 24 2.png]]
            
            EFS의 장점
            
            - Region 스코프이므로 여러 AZ에 최대 100개 인스턴스에 붙일 수 있다.
            - Linux 인스턴스만 사용 가능하다.(POSIX 파일시스템을 사용하므로)
            - EFS는 EBS보다 비싸지만 비용 절감이 가능하다.
    - EFS Access Points
        
        ![[image 25 2.png]]
        
        **EFS - Access Points**
        
        - NFS 환경에 접근하는 어플리케이션들을 관리할 수 있다.
        - Access Points를 통해 접근하는 어플리케이션에 POSIX 유저와 그룹을 강제할 수 있다.
        - 접근 가능한 디렉터리를 제한하고 루트 디렉터리를 변경 가능하다.
        - NFS Client에서 IAM Policies를 통해 접근 제어가 가능하다.
    - EFS - Operations
        
        ![[image 26 2.png]]
        
        **EFS - Operations**
        
        - 이전(Migration)이 필요하지 않은 작업들
            - Lifecycle Policy (enable IA or change IA settings)
            - 처리량 모드와 Provisioned 처리량 개수 조절 가능
            - EFA Access Points
        - Data Sync를 통해 이전해야만 사용할 수 있는 작업들
            - EFS 암호화를 위해서 이전
            - 퍼포먼스 모드로 변경(e.g. Max IO)
    - EFS - CloudWatch Metrics
        
        ![[image 27 2.png]]
        
        **EFS - CloudWatch Metrics**
        
        - PercentIOLimit
            - I/O Limit에 얼마나 근접한지
            - 만약, 100%면 Max I/O 옵션으로 이전하세요.
        - BurstCreditBalance
            - 더 높은 대역폭 처리를 위해
        - Storage Bytes
            - 파일 시스템의 사이즈

### 핵심 요약

- 핵심 요약 접기
    - Amazon EC2 Storage와 Data Management에 대한 주요 내용:
    - EBS (Elastic Block Store)
        - EC2 인스턴스용 네트워크 드라이브로, 한 번에 하나의 인스턴스에 연결 가능 (io1/io2 제외)
        - 특정 AZ에 종속되며, 스냅샷을 통해 백업 가능
        - gp2/gp3, io1/io2, st1, sc1 등 다양한 볼륨 유형 제공
    - EFS (Elastic File System)
        - 여러 EC2 인스턴스에 동시 마운트 가능한 관리형 NFS
        - 멀티 AZ 지원, 높은 가용성과 확장성 제공
        - 다양한 성능 모드와 처리량 모드 지원
        - 스토리지 클래스를 통해 비용 최적화 가능
    - EBS와 EFS의 주요 차이점
        - EBS는 단일 인스턴스, EFS는 여러 인스턴스에 동시 연결 가능
        - EBS는 AZ 종속적, EFS는 리전 범위로 사용 가능
        - EFS는 Linux 인스턴스만 지원 (POSIX 파일 시스템)
    - 핵심 개념:
        - EBS: EC2 인스턴스용 네트워크 드라이브, 주로 단일 인스턴스에 연결
        - EFS: 여러 EC2 인스턴스에 동시 마운트 가능한 관리형 NFS
        - 성능과 확장성: EFS는 높은 확장성과 다양한 성능 모드 제공
        - 비용 최적화: EFS가 더 비용이 높지만 스토리지 클래스와 라이프사이클 관리를 통해 비용 절감 가능
        - 가용성: EBS는 AZ 종속적, EFS는 멀티 AZ 지원으로 높은 가용성 제공
        - 사용 사례: EBS는 부팅 볼륨에 적합, EFS는 대규모 파일 공유와 데이터 처리에 적합

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 