---
⭕첫 학습날: 2024-08-30
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: true
복습: 장기기억
🛑첫날: "✏첫날 : 2024/08/30"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤58일째❤
🛑4일후: "🥉4일뒤 : 2024/09/03"
🛑7일후: "🥈7일뒤 : 2024/09/06"
🛑14일후: "🥇14일뒤 : 2024/09/13"
4일후: "@2024년 9월 3일"
4일후(text): 2024/09/03
7일후: "@2024년 9월 6일"
7일후(text): 2024/09/06
14일후: "@2024년 9월 13일"
14일후(text): 2024/09/13
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/08/30
오늘과 첫학습날 사이: "58"
사이: "58"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "1"
학습률: "0.8"
진행바: 🟩🟩🟩🟩🟩🟩🟩🟩⬜⬜ 80%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[EC2]]

### 단서 질문

- Spot Instance란?
    
    max cost 설정을 통해서 해당 지역의 인스턴스 대여 비용이 max cost보다 낮으면 해당 AZ에서 인스턴스를 생성한다.
    
- Spot Instance에서 실행하면 좋은 작업들
    
    중단되어도 괜찮은 작업들이 여기에 속한다. batch 작업,
    
- Spot Fleets란?
    
    Spot과 onDemand(선택사항)로 인스턴스를 구축한다.
    
- Busrtable Instance란?
    
    CPU 사용량이 100%를 초과해도 해당 초과분만큼 사용을 허용한다. 초과하는 시간동안 CPU Credit이 소모되며 모두 소모하면 CPU의 처리 속도가 느려진다.
    
    T2/T3 Unlimited가 있는데 이는 크레딧 카드 제한이 없이 무제한으로 CPU 사용량을 계속 더 사용할 수 있다.
    
- Elastic IP
    
    AWS에서 제공하는 고정 IP로 서버와 고정되어 있으면 요금을 부과하지 않는다.
    
- CloudWatch란?
    
    AWS 인스턴스의 로그와 매트릭스를 수집하는 역할을 한다. 단, CloudWatch는 메모리 사용량은 제공하지 않는다.
    
    CloudWatch로 로깅을 기록하고 싶은 인스턴스는 CloudWatch Agent를 실행해야 하며 IAM Role로 CloudWatchAgent가 있어야 한다.
    
    온프로미스 환경에서도 Agent를 실행하면 CloudWatch로 수집이 가능하다.
    
    SSM을 통해 Parameter Store에 CloudWatchAgent 설정값을 저장할 수 있다.
    

### 핵심 필기

- 전체 내용 접기
    - [SAA] Spot Instances & Spot Fleet
        - EC2 Spot Instance Requests
            - 온디맨드에 비해 90프로 저렴
            - max spot price를 정하고 current spot price < max이면 인스턴스 사용 가능
                - spot price는 가용자원량과 offer에 따라 변한다.
                - 만약, max price보다 spot price가 비싸지면 stop하거나 terminate 중에 선택해야 한다. 시간은 2분 준다.
            - Spot Block
                - spot 뺏기는 것을 특정 시간동안 방지
                - 단, 설정해도 뺏기는 경우도 생김
                - 현재 사라진 기능
            - batch, 데이터분석, 실패해도 되는 워크로드(workloads that are resilient to failure)
            - 중요한 작업엔 사용 불가
        - **How to terminate Spot Instances(시험 가능성)**
            
            ![[image.S462S2.png]]
            
            ![[image.LWKUS2.png]]
            
              
            
            - 인스턴스를 제거하기 전에 Spot Requests를 먼저 제거해야한다. 안그러면 Spot Request가 다시 인스턴스를 생성한다.
            - Spot Request를 설정하면 max price보다 가격이 낮아졌을 때, 인스턴스를 생성한다.
            - 인스턴스가 Interrupt 받았을 때 Request Type이 persistent면 재생성하고 one-time이면 그대로 인스턴스를 제거하고 유지한다.
        - **Spot Fleets(시험 가능성)**
            - Spot과 onDemand(선택사항)로 인스턴스를 구축하는 방식
            - Spot Fleet는 가격과 Capacity를 만족하는 타겟을 찾는다.
                - 인스턴스 생성 가능한 풀을 정의: 인스턴스 타입, OS, AZ
                - 인스턴스 생성 풀(launch pool)을 여러 개 가질 수 있다.
                - max cost에 도달했거나 capacity에 도달하면 인스턴스를 그만 만든다.
            - Spot Instance 전략
                - lowest Price: 제질 저렴한 pool을 사용(비용 최적화, 짧은 작업(short workload))
                - diversified: 여러 풀을 사용한다.(great for availability, long workloads)
                - capacityOptimized: capacity 개수에 맞는 풀을 생성
                - priceCapacityOptimized(recommended): 가장 capacity가 높은 풀을 선택하고 그 중에서 가장 가격이 적은 풀을 선택한다.
    - Burstable Instances
        
        - T2/T3는 Burstable 인스턴스다.
        - CPU 사용량을 초과해도 순간적으로 초과 CPU만큼 사용을 허용한다.
        - 부하급증으로(a spike in load) CPU 사용량을 초과하더라도 버스트를 통해 CPU 상태가 정상적으로 돌아간다.
        - 버스트 되면 “burst credits”를 사용한다.
        - 크레딧을 다 사용하면 CPU는 다시 BAD 된다.
        - 버스트를 멈추면 다시 크레딧이 누적된다.
        
        ![[image 43.png]]
        
          
        
        ==**T2/T3 Unlimited**==
        
        - 버스트 크레딧 카드를 무제한으로 사용하는 서비스
        - 초과된 vCPU만큼 금액 부과
        - 제한이 없으므로 CPU 헬스를 모니터링해야한다.
    - Elastic IP
        
        - AWS에서 제공하는 고정 공인 IPv4 주소
        - 인스턴스와 매핑할 수 있다.
        - 서버와 고정되어 있는 Elastic IP는 요금을 부과하지 않는다.
        - 서버와 고정되지 않은 Elastic IP는 요금을 부과한다.
        - 인스턴스 실패나 소프트웨어 오류가 났을 때, Elastic IP를 정상적인 인스턴스로 리맵핑을 하면 이슈가 생겼는지 소비자가 모르게 가릴 수 있다.(mask=가리다)
        - 계정당 5개를 제공한다.(요청을 통해 늘릴 수 있다)
        
          
        
        ==**Elastic IP 사용을 피하기**==
        
        고정 IP를 사용하면 당연히 편리하겠지만 꼭 필요하지 않으면 굳이 사용하지 않는 게 좋다.
        
        피하는 방법으로는 아래 방법들이 있다.
        
        - 도메인 구입 후에 DNS를 통해 서비스 제공
        - 로드밸런서와 정적 호스트 네임(static hostname)을 같이 사용
    - CloudWatch Metrics for EC2
        
        Metric을 설정하는 방법은 두 가지가 존재한다.
        
        하나는 AWS에서 제공하는 AWS Provided Metrics로 설정할 필요 없이 AWS에서 제공한다.
        
        두번째는 Custom Metrics로 인스턴스에 CloudWatchAgent 설치를 하고 API를 통해 CloudWatch에 로그를 보낸다.
        
        1. **AWS Provided Metrics (AWS pushes them):**
            1. Basic Monitoring(default): 5분 간격으로 매트릭스 수집
            2. Detailed Monitoring(paid): 1분 간격으로 매트릭스 수집
            3. 수집 내용: CPU, DISK, NETWORK, Status Check
        2. **Custom Metrics(yours to push)**
            1. Basic Resolution: 1 minute interval
            2. High Resolution: 1sec interval
            3. 수집 내용: RAM, 어플리케이션 레벨 매트릭스
            4. IAM 롤을 인스턴스에 설정해서 CloudMetricsAgent 권한을 가지고 있어야 한다.(해당 권한을 가지고 있어야 CloudWatchAgent를 인스턴스에서 실행하고 API 호출을 통해 CloudWatch에 로그를 보낼 수 있다.)
        
        EC2에 포함된 매트릭스들
        
        - CPU: CPU 사용량 + 크레딧 사용량 / Balance
        - 네트워크: Network In / Out
        - Status Check:
            - Instance Status = check the EC2 VM(It will check the os)
            - System Status = check the underlying hardware(It will check the physical device or software which installed in the device)
            - ==**RAM은 포함 안된다!!**==
        
        **메모리 사용량은 AWS 메트릭에서 제공 안한다!! 시험에 무조건 나옴**
        
    - CloudWatch - Unified CloudWatch Agent - Overview
        - 개요
            
            ![[image 1 16.png]]
            
            - 가상 서버를 위한 Agent e.g EC2 instance, on-premises servers
            - 시스템 레벨 매트릭스를 수집 가능하다. e.g Ram, Processes, Used Disk Space, etc
            - CloudWatch에 로그를 보내기 위해서 로그를 수집한다.
                - CloudWatch Agent를 사용해야만 CloudWatch에 로그를 보낼 수 있다.
            - SSM의 파라미터 스토어에 설정을 저장해서 중앙화한다.(Centralized configuration using SSM Parameter Store)
            - CloudWatch Agent를 사용하는 IAM의 롤을 부여받아야 한다.
                - CloudWatchAgentAdminPolicy: SSM에 CloudAgent의 설정값을 저장할 수 있다.
                - CloudWatchAgentServerPolicy: SSM으로부터 설정값을 받을 수는 있지만 설정값을 저장할 수 없다.
            - EC2가 아닌 ==온프로미스 서버에서 CloudWatch로 로그를 보내려면== **접근키**를 온프로미스 서버에 설정해놔야한다.
        - procstat Plugin
            - 매트릭스를 수집하고 프로세스별 시스템 자원을 모니터링한다.(Collect metrices and monitor system utilization of individual processes)
            - 지원 운영체제: Linux, Window
            - 수집데이터 예시: CPU, 메모리 사용량 등
            - 모니터링할 프로세스를 선택하는 방법은 3가지다.
                - pid_file: PID를 통해 수집
                - exe: 프로세스명을 통해 수집
                - pattern: 프로세스를 실행하는데 사용된 커맨드 라인
            - procstat 플러그인을 통해 수집된 매트릭스는 접두사로 “procstat”이 온다.
                - e.g procstat_cpu_time, procstat_cpu_usage
    - CloudWatch - Unified CloudWatch Agent - Hands On
        
          
        
    - EC2 Instance Status Checks
        - Status Checks - CW Metrics & Recovery
            - 개요
                - CloudWatch Metrics(1분 간격)
                    - StatusCheckFailed_System: EC2가 실행되는 하드웨어나 네트워크 문제를 확인한다.
                    - StatusCheckFailed_Instance: 인스턴스의 설정. OS, 소프트웨어 이슈를 통한 문제가 발생했는지 확인한다.
                    - StatusCheckFailed(for both): 둘 다 체크한다.
            - Recovery 방법
                1. **CloudWatch Alarm**
                    
                    ![[image 2 14.png]]
                    
                    1. CloudWatch에서 EC2 인스턴스로부터 Failed 상태를 받으면 알람을 트리거한다.
                    2. 알람을 통해 EC2 인스턴스를 Recovery한다.
                    3. 알람에서 AWS SNS를 이용해서 알림을 보낼 수도 있다.
                2. **AutoScailing Group**
                    
                    ![[image 3 13.png]]
                    
                    1. EC2 인스턴스가 오토스케일링 그룹에 속하면 자동으로 인스턴스를 숫자에 맞게 재생성한다.
                    2. 단, 이는 회복이 아닌 재생성이므로 동일한 IP를 사용하지 않는다.
                    3. 자동화를 통해 Elastic IP를 할당해줄 수는 있다.
    - EC2 Instance Status Checks - Hands On
        
        EC2 인스턴스에서 Create Action을 통해 실습한다.
        
        Alarm의 Action Type 중에 Recover는 EC2 인스턴스 중단 후 재시작한다. 따라서, 물리장치가 바뀐다.(하드웨어 이슈일 때)
        
        Action Type 중에 Reboot는 운영체제를 재시작한다. OS나 응용 소프트웨어 이슈일 때 사용한다.
        
        커맨드라인으로 Alarm 조건을 만족하지 않아도 알람을 트리거할 수 있다. set-alarm-state 커맨트를 통해 가능하다.
        
    - EC2 Instance Status Checks - MUST KNOW
        
        These can be the focus of **2 to 3 questions at the exam**, therefore know the differences:
        
        ### **SYSTEM status checks**
        
        System status checks monitor the _AWS systems_ on which your instance runs
        
        - Problem with the underlying host. Example:
            - Loss of network connectivity
            - Loss of system power
            - Software issues on the physical host
            - Hardware issues on the physical host that impact network reachability
        - Either wait for AWS to fix the host,
        - OR Move the EC2 instance to a new host = STOP & START the instance (if EBS backed)
        
        ### **INSTANCE status checks**
        
        Instance status checks monitor the software and network configuration of _your individual instance_
        
        - Example of issues
            - Incorrect networking or startup configuration
            - Exhausted memory
            - Corrupted file system
            - Incompatible kernel
        - Requires your involvement to fix
        - Restart the EC2 instance, OR
        - Change the EC2 instance configuration
        
          
        
    - [SAA] EC2 Hibernate
        - EC2 Hibernate
            - 인스턴스가 중지된 경우
                - Stop: 기억장치(EBS)의 데이터는 그대로 남아 있는다.
                - Terminate: EBS 볼륨과 destroyed로 설정한 셋업도 삭제된다.
            - EC2 인스턴스의 Start 절차는 아래와 같다.
                - 첫 시작일 때(First Start): OS가 부팅되고 EC2 유저 데이터 스크립트가 실행된다.
                - 첫 시작이 아닐 때(Following starts): OS가 부팅된다.
                - 이후에 어플리케이션이 실행되고, 캐시가 웜업된다.
            - EC2 Hibernate란?
                - 주기억장치의 내용들이 EBS 볼륨에 저장한다.
                - 이후에 부팅 시엔 EBS 볼륨에 저장 내용을 RAM으로 읽어서 마치 OS가 정지하지 않은 것처럼 동작한다.
                - root EBS는 암호화(Encrypted) 되어야 한다.
            - 사용 케이스
                
                ![[image 4 13.png]]
                
                - 오랜 시간이 필요한 작업(Long-running processes)
                - RAM 상태 저장이 필요한 경우
                - 초기화하는데 시간이 걸리는 서비스(Service that take time to initialize)
        - EC2 Hibernate - Good to Know
            - 지원 인스턴스 패밀리: C3, C4, C5, I3, M3, M4, R3, R4, T2, T3, …
            - Instance Ram Size - 150GB보다 작아야 한다.
            - Instance Size: not supported for bare metal instances
            - AMI: Amazon Lunux2, Linux AMI, Ubuntu, RHEL, CentOS, winndows…
            - Root Volume: EBS, encrypted, not instance store, and large
            - On-Demand, Reserved, Spot에 가능
            - 60일 이상 hibernated 불가
    - [SAA] EC2 Hibernate Hands On
        
          
        

### 핵심 요약

- 핵심 요약 접기
    
    ### Spot Instances
    

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 