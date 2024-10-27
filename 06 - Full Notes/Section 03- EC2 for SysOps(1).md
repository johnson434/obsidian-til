---
⭕첫 학습날: 2024-08-21
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
⭕학습정도: 🤔중
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: true
복습: 장기기억
🛑첫날: "✏첫날 : 2024/08/21"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤67일째❤
🛑4일후: "🥉4일뒤 : 2024/08/25"
🛑7일후: "🥈7일뒤 : 2024/08/28"
🛑14일후: "🥇14일뒤 : 2024/09/04"
4일후: "@2024년 8월 25일"
4일후(text): 2024/08/25
7일후: "@2024년 8월 28일"
7일후(text): 2024/08/28
14일후: "@2024년 9월 4일"
14일후(text): 2024/09/04
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/08/21
오늘과 첫학습날 사이: "67"
사이: "67"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "1"
학습률: "0.8"
진행바: 🟩🟩🟩🟩🟩🟩🟩🟩⬜⬜ 80%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]]

### 단서 질문

- EC2에서 키페어는 뭐냐?
    
    ssh를 통해 접근하기 위해 사용되는 키를 의미한다. 키페어를 만들면 .pem 파일을 다운로드 받는데 이 pem 파일을 키로 이용해서 ssh로 EC2에 접속이 가능하다.
    
    ```JavaScript
    ssh -i 키페어.pem ec2-user@IP주소
    ```
    
- VPC란 뭐냐?
    
    Virtual Private Cloud로 클라우드의 네트워크를 고립시키기 위해 사용된다.
    
    리눅스 네트워크 네임스페이스의 확장판 느낌. 리눅스 네트워크 네임스페이스가 하나의 커널에서 네트워크를 고립시킨다면 VPC는 수많은 물리머신이나 서비스를 위한 고립 네트워크다.
    
- AZ란?
    
    Availability Zone
    

### 핵심 필기

- 전체 내용 접기
    - **수직 스케일링 하기**
        
        **필요 조건**
        
        - EBS backed Instance여야 한다.
        
        > [!important]  
        > EBS는 Elastic Block Storage로 EC2가 사용 가능한 영구지속저장장치를 의미한다. EBS는 EC2와 1대1 대응 되지만 다른 인스턴스에 사용도 가능하다.  
        
        **방법**
        
        - 인스턴스 멈추기
        - 인스턴스 설정에서 인스턴스 타입 바꾸기
        
        인스턴스를 변경하더라도 EBS를 사용하므로 하드웨어는 변경되지만 저장 데이터는 변경되지 않는다.
        
    - **Enhanced Networking**
        - SR-IOV and EFA
            
            ENA와 EFA 모두 네트워크 향상을 위해 제공하는 가상 네트워크 인터페이스다.
            
            ### ==**ENA**==
            
            1. **EC2 Enhanced Networking(SR-IOV)**
            
            - 높은 대역폭, 높은 PPS(Packet Per Second), 낮은 지연속도(latency)
            - Option1: Elastic Network Adapter(**ENA**) 100Gbps
            - Option2: Intel 82599 VF 10Gbps - Legacy
            - Works for newer generation EC2 Instances(옛날 인스턴스는 지원 안함)
            - t2는 구버전이라 ENA로 설정되어 있다.
                
                ```Shell
                modinfo ena
                
                ethotool -i enX0 # 아마존 구버전(amazon 2023이전)은 eth0임.
                driver: vif # 현재 사용하는 EC2인 t2 구타입이므로 ENA가 아닌 vif 사용
                						# t3부터는 ENA 사용함
                version: 6.1.102-111.182.amzn2023.x86_64
                firmware-version: 
                expansion-rom-version: 
                bus-info: vif-0
                supports-statistics: yes
                supports-test: no
                supports-eeprom-access: no
                supports-register-dump: no
                supports-priv-flags: no
                ```
                
            
            > [!important]  
            > SR-IOV(Single Route I/O Virtualization): 단일 루트 IO 가상화란? 여러 파티션이 동시에 실행되어 PCIe 장치를 공유할 수 있도록 하는 방법  
            
              
            
            1. **Elastic Fabric Adapter(EFA)**
            
            - HPC(High Performance Computer)를 위한 ENA 향상판으로 리눅스에서만 동작한다.
            - Great for inter-node communication, tightly coupled workloads
            - Message Passing Interface(MPI)에 영향을 끼친다.
            - 리눅스의 커널을 우회해서 어플리케이션끼리 직접 통신하므로 더 빠르다.
                - 일반적으로 NIC를 통해서 통신을 하는데 EFA는 이를 이용하지 않는다.
    - **[SAA] EC2 Placement Groups**
        
        EC2 인스턴스의 배치 전략을 정하는 그룹
        
        - Cluster
            
            ![[image 40.png]]
            
            - 단일 AZ에 인스턴스를 구축 → low latency
            - 장점: Enhanced Networking이 설정되어 있어 인스턴스 간에 10Gbps 대역폭을 가진다.
            - 단점: AZ이 다운되면 전체 다운
            - 사용처: low latency and high network throughput
        - Spread
            
            ![[image 1 13.png]]
            
            - **장점**
                - **서로 다른 하드웨어로 분산**하여 위험 방지 → 중요한 App
                - 여러 AZ 사용 가능
            - **단점**
                - 그룹별로 최대 7개까지 가능
            - UseCase
                - 중요한 다운되면 안되는 App
                - 높은 가용량(High availability)이 필요한 App
        - Partitioning
            
            ![[image 2 11.png]]
            
            - 파티션이라는 그룹에 EC2를 넣는 것
            - 파티션끼리는 서로 독립적으로 서로 다른 랙을 사용한다.
            - AZ 하나에 7개의 파티션을 배치 가능하다.
            - AZ는 여러 개 사용 가능하다.
            - 서로 다른 파티션에 위치한 EC2 인스턴스는 서로 다른 랙에 위치한다.(AZ가 같더라도)
            - 파티션 하나에 EC2 100개까지 배치 가능
            - 파티션 하나가 실패하면 많은 EC2 인스턴스에 영향을 끼칠 순 있지만(EC2는 최대한 서로 다른 랙에 배치되어 생산되니까) 다른 파티션엔 영향을 끼치지 않는다.(서로 다른 파티션이므로 서로 다른 랙이므로)
            
            **usecase**
            
            - 카프카와 같이 분산 처리 가능한 App
            - HDFS
            - HBase
            - 카산드라
            
              
            
    - **EC2 Shutdown Behavior & Termination Protection**
        
        EC2의 인스턴스에서 CLI를 통해 `shutdown`을 입력하면 두 가지 액션이 일어날 수 있습니다.
        
        1. shutdown(default): 인스턴스가 종료
        2. terminate: 인스턴스가 제거됨.
        
          
        
        **시험 팁**
        
        1. shutdown 설정을 terminate로 설정 후에 terminate Protection을 킨다
        2. OS에서 shutdown하면 무슨 일이 일어날까?
        
        ⇒ 인스턴스가 제거된다. 왜일까? terminate Protection은 AWS CLI나 AWS SDK를 통해 종료하는 것을 방지할뿐이지 OS내의 shoutdown을 통한 terminate를 방지하지 못한다.
        
    - **Troubleshooting EC2 Launch Issues**
        
        **시험에 백퍼 나오는 파트**
        
        ==**# InstanceLimitExceeded**==
        
        - 원인: vCPU 사용량 한계에 도달함을 의미한다.
        - 발생 예시: (A,C,D,H,I,M,R,T,Z) 인스턴스 타입들을 돌려서 총합 vCPU가 64를 넘을 때(64는 default 값) vCPUS 제한은 region별로 있다.
        - 해결 방법
            - 방법1. 인스턴스를 다른 리전에서 실행
            - 방법2. 인스턴스 제한 증가 시키기
                - Service Quotas 들어가서 설정 가능
        
        ==**# InsufficientInstanceCapacity**==
        
        - **원인**: AWS의 가용 자원이 모자람. AWS의 잘못으로 사용자 잘못이 아님
        - 해결 방법
            - 방법1. 기다렸다가 재요청
            - 방법2. 리퀘스트 취소 후에 요청하기. 여러 개 요청 시에 한 번에 리퀘스트로 요청해라
            - 방법3. 너무 급하면 **다른 인스턴스 타입 요청**하기. 나중에 리사이즈하면 됨
        
          
        
        ==**# Instance Terminates Immediately**==
        
        - 가능한 원인들:
            - EBS 제한 초과
            - EBS 스냅샷이 오염됨
            - root EBS가 암호화 되어 있는데 복호화를 위해 사용할 키가 저장되어 있는 KMS(Key Management System)에 접근 권한이 없어서
            - 인스턴스 실행을 위한 AMI에 필수 파일이 없어서
        - 정확한 원인을 찾는 방법:
            - AWS EC2 콘솔 - 인스턴스 - Description 탭
    - **EC2 SSH troubleshooting**
        - SSH 이슈 주요 발생 원인들
            
            - private key 파일이 400 권한을 가지고 있어야 한다. 아닐 시 `Unprotected private key file` 에러가 발생한다.
            - username 확인하기. 리눅스는 ubuntu AMI는 ec2-user임. `Host key not found` 나 `Permission denied` 나 `Connection closed by [instance] port22` 에러가 발생한다.
            - `Connection timed out` 이 발생하는 이유는 아래와 같다.
                1. SG(Security Group)이 제대로 설정되지 않음.
                2. NACL이 잘못 설정됨
                3. 인스턴스의 CPU 과부하
                4. 인스턴스의 공인 IP가 없음
            
            > [!important]  
            > NACL(Network Access Control List)은 VPC(가상 사설 클라우드) 내에서 서브넷(subnet) 수준에서 인바운드(inbound)와 아웃바운드(outbound) 트래픽을 제어하기 위한 보안 계층입니다. NACL을 사용하면 허용(allow)하거나 거부(deny)할 트래픽을 규칙으로 정의할 수 있으며, 이러한 규칙은 서브넷에 연결된 모든 인스턴스에 적용됩니다.  
            
        - SSH vs EC2 Instance Connect
            
            ![[image 3 10.png]]
            
            SSH 연결의 경우, SG에서 열어준 포트와 허용한 IP를 통해서 shell을 통해 복호화 키를 사용하여 접속합니다.
            
            EC2 Instance Connect는 AWS 대시보드에서 제공하는 접근 방법으로 60초동안 접근 가능한 복호화 키를 발급하여 이를 통해 접속합니다.
            
            단, EC2 Instance Connect도 SSH 연결과 마찬가지로 SG에서 허용하지 않은 IP나 포트를 통해 접속하면 접속이 불가능합니다.
            
    - **EC2 Instance Purchasing Options**
        - **On-Demand**
            - 사용한만큼 낸다.
                - 리눅스 or 윈도우: 초당 청구
                - 다른 OS: 시간당 청구
            - 제일 비싸지만 선불 결제가 없다.
            - 장기간 계약(long-term commitment)이 없다.
            - 짧은 작업(short term)이나 지속적으로 동작(uninterrupted workloads)에 적합하다.
        - **EC2 Reserved Instances(**==**RI**==**)**
            
            - On-demand에 비해 72% 쌉니다.
            - 사양을 예약합니다.(인스턴스 타입, 지역, 테넌시, OS)
            - 예약 기간: 1년 or 3년
            - 지불 옵션: 후불, 부분선불, 전체선불
            - 예약 범위(Reserved Instance’s Scope): Regional or Zonal
            - 꾸준히 사용되는 어플리케이션에 용이 eg.Database
            - Reserved Instance 마켓플레이스에서 되팔거나 사기 가능
            - Convertible Reserved Instance(전환 가능한 RI)
                - 인스턴스 타입, 인스턴스 패밀리, OS, Scope, Tenancy 변경 가능
                - 66% 할인(일반 RI보다 비쌈)
            
            > [!important]  
            > 테넌시란? EC2 인스턴스가 물리적으로 저장되는 방식  
            
        - **Saving Plans**
            - 장기간 사용을 예상하고 할인(최대 72%)
            - 사용량에 따라 계약 가능하다(10$/hour이 할인 최대폭이다. 로 1년시간or 3년)
                - 자세한 설명
                    
                    10$/hour이 이해가 안갔는데 이건 사용 요금이 시간당 10$인 게 아니라 할인폭이 10$/hour인거다.
                    
                    즉, EC2를 100대를 사용해서 한 시간에 15달러가 나왔다? 10달러 요금까지는 Saving Plans만큼 할인 받고(최대 기준 72%) 나머지 5달러는 EC2 onDemand 요금으로 내는 거다.
                    
                    시간당 최소 10달러는 쓰는 회사에서만 사용 가능할듯.
                    
            - Saving Plan 할인 금액을 넘는 금액은 On-Demand로 청부
            - 특정 인스턴스 패밀리나 AWS **Region에 고정**된다. (eg. M5 in us-east-1)
            - 유연하다
                - Instance Size(e.g m5.xlarge → m5.x2Large)
                - OS (eg. Linux, Windows)
                - Tenancy (Host, Dedicated, Default)
        - **Spot Instances**
            - 온디멘드에 비해 최대 90프로 저렴하다.
            - max price가 현재 spot 가격보다 저렴하면 인스턴스를 뺏긴다.
            - 제일 저렴하다.
            - 실패해도 좋은 작업들에 좋다.
                - Batch Jobs
                - Data Analysis
                - Image Processing
                - Any distributed workloads
                - Workloads with a flexible start and end time
            - 중요한 작업이나 DB에는 적합하지 않다. → 당연히 중간에 죽을 수 있는데 놓으면 바보지
        - **Dedicated Hosts**
            - 물리적 서버를 통째로 빌립니다.
            - 복잡한 요구사항을 따를 수 있게 하고 고정 서버 방식의 소프트웨어 라이선스를 재사용 가능합니다.(Allows you address compliance requirements and use your existing server- bound software licenses)
            - 결제 옵션
                - 온디멘드: 초당 결제
                - Reserved: 1년, 3년
            - 제일 비쌈
            - 복잡한 레이센스를 가진 소프트웨어에 유용하다.(eg. BYOL)
            - 규제가 심한 회사(외부에 데이터 반입 불가)에서 사용 가능
        - **Dedicated Instances**
            - 특정 하드웨어를 사용하며 해당 하드웨어에서만 인스턴스를 생성한다.
            - 같은 계정에서 만든 인스턴스들이 해당 하드웨어를 사용할 수 있다.
            - 인스턴스 배치에 대한 제어 없음
        - **Capacity Reservations**
            - 특정 AZ에 온디맨드 인스턴스들을 예약함.
            - 언제든 EC2에 접근 가능
            - 시간 계약이 없다.(create/cancel anytime), 할인도 없다.
            - Regional Reserved Instances와 Saving Plans를 결합해서 할인 받을 수는 있다.
            - 인스턴스를 실행하든 안하든 On-Demand 요금 부과한다.
            - 짧은 기간, 방해받으면 안되는 작업(short term, uninterrupted workloads)이며 특정 AZ에 있어야 하는 작업이 적합하다.
        - **Dedicated Hosts vs Dedicated Instances**
            
            - **일반 인스턴스**: 같은 물리적 서버에서 여러 AWS 고객이 인스턴스를 실행할 수 있는 **멀티 테넌시 구조**.
            - **Dedicated Instance**: 물리적 서버(노드)를 **오직 하나의 고객**만 사용하며, 다른 고객의 인스턴스는 같은 서버에서 실행되지 않음.
            - **랙 전체는 공유 가능**: 한 랙에는 여러 물리적 서버가 있으므로, **같은 랙 내 다른 서버들은 여전히 다른 고객이 사용할 수 있음**.
            
            ![[image 4 10.png]]
            
            **랙**: 서버를 수직으로 쌓아올린 프레임
            
            **물리적 서버**: 실제로 물리적으로 돌아가는 하드웨어 컴퓨팅 단위. 노드라고 부를 수도 있다.
            
            **인스턴스**: 물리적 서버에서 돌아가는 OS의 개수. 멀티 테넌시 구조면 하나의 서버에 여러 인스턴스가 올라간다. ==일반적으로== 우리가 사용하는 인스턴스는 **다른 사용자들과 동일한 물리적 서버를 공유**한다.
            
              
            

### 핵심 요약

- 핵심 요약 접기
    - EC2는 EBS를 사용하면 Instance Type을 바꿔도 EBS에 데이터가 저장되므로 데이터 손실이 발생하지 않는다.
    - EBS는 Elastic Block Storage로 EC2 데이터를 저장하는데 사용
    - EC2 Placement Groups는 EC2 배치 전략을 정하는 그룹이다. Cluster(단일 AZ), Spread(하드웨어 분산, AZ별로 최대 7개 인스턴스 생성 가능, 서로 다른 AZ 사용 가능), Partitioning(서로 다른 파티션은 서로 다른 랙에 존재하며 AZ 하나에 그룹을 7개밖에 사용 못한다 그룹엔 인스턴스 100개까지 허용 가능)
    - EC2 shutdown 옵션은 기본적으로 shutdown이지만 terminate로 설정 가능하다. 이는 OS 내에서 shutdown 사용 시 동작 방식이다.
    - Terminate Protection을 걸더라도 shutdown을 걸면 terminate 된다. Terminate Protection은 AWS 대시보드나 API, SDK를 위한 보호 기능이지 OS 내부엔 아무 영향을 끼치지 않는다.
    - EC2 에러 원인은 여러 가지가 있다.
    - InstanceLimitExceec는 **Region에** vCPU 개수 초과 시 발생
    - InsufficientInstanceCapacity는 **AZ에** AWS에 사용 가능한 자원이 없음
    - Instance Terminates Immediately EBS 용량 초과, OS Image 오염, EBS 접근을 위한 KMS 접근 권한 없음
    - SSH 접근은 유저명과 IP를 제대로 명시해라
    - AWS에서 제공하는 EC2 인스턴스 커넥션은 일회용 복호화 키를 사용해서 접속하는 방식이다.
    - Dedicated Host는 서버 자체(랙)를 물리적으로 빌리고 Dedicated Instance는 인스턴스를 위한 하드웨어를 물리적으로 빌린다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 