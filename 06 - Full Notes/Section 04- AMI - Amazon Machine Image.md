---
⭕첫 학습날: 2024-08-25
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: true
복습: 장기기억
🛑첫날: "✏첫날 : 2024/08/25"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤63일째❤
🛑4일후: "🥉4일뒤 : 2024/08/29"
🛑7일후: "🥈7일뒤 : 2024/09/01"
🛑14일후: "🥇14일뒤 : 2024/09/08"
4일후: "@2024년 8월 29일"
4일후(text): 2024/08/29
7일후: "@2024년 9월 1일"
7일후(text): 2024/09/01
14일후: "@2024년 9월 8일"
14일후(text): 2024/09/08
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/08/25
오늘과 첫학습날 사이: "63"
사이: "63"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "1"
학습률: "0.8"
진행바: 🟩🟩🟩🟩🟩🟩🟩🟩⬜⬜ 80%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[AMI]]

### 단서 질문

- AMI가 뭐야?
    - Amazon Machine Image로 패키지가 이미 세팅(pre-packed)되었으므로 부팅 속도와 설정 속도가 빠릅니다.
- 인스턴스를 다른 AZ로 옮기는 방법
    
    인스턴스로부터 AMI를 새로 만들고 인스턴스를 중단한 후에 이전한 AZ에 AMI를 사용하여 인스턴스를 생성한다.
    
- AMI를 백업하는 방법
    1. AWS Backup을 사용
    2. EventBridge를 통해서 AWS Lambda를 트리거 → AWS Lambda가 AMI 이미지 백업 호출 → 백업 시작
- EC2 Image Builder란?
    
    가상 머신이나 컨테이너를 위해 사용되는 이미지를 만드는 자동화 시스템
    
- EC2 Image Builder의 동작 방식
    
    EC2 인스턴스를 생성 → 정의한 설정에 맞게 인스턴스를 초기화 → 해당 인스턴스로부터 AMI를 생성 → AMI 생성된 후에 인스턴스 종료 → 만들어진 AMI를 사용해서 인스턴스 생성 → 정상적으로 동작하는지 테스트
    

### 핵심 필기

- 전체 내용 접기
    - [CCP/SAA/DVA] AMI Overview
        - AMI = Amazon Machine Image
        - A Customization of an EC2 Instance
            - configure your own setting e.g software, configuration, os, monitoring…
            - **Faster** **boot / Configuration time** because all your software is pre-packed.
        - AMI are built for **specific region**(can be copied from region to region)
        - Youn can lanch EC2 instances from:
            - A Public AMI: AWS provided
            - Your own AMI
            - An AWS Marketplace AMI
    - AMI Process (from an EC2 instance)
        
        - Start EC2
        - Customize Setting
        - Stop instance (this is for data integrity 데이터 무결성)
        - Build AMI(This will also create EBS snapshots)
        
        ![[image 39.png]]
        
    - AMI No-Reboot Option
        
        ![[image 1 12.png]]
        
        - AMI 셧다운 하지 않고 AMI를 만들 수 있다.
        - 기본적으로 No-Reboot Option은 설정 안됐음
    - AWS Backup Plans to create AMI
        
        - 방법1. AWS BackUp
            - no-reboot 설정되어 있는 경우엔 EC2는 스냅샷을 찍을 때, 인스턴스가 종료된 상태가 아니므로 파일 시스템 무결성(File System Integridty)을 보장하지 못함.
        - 방법2.
            - EventBridgeRule을 통해 AMI 스케쥴링을 한다.
            - 이벤트가 호출되면 Lamda Function을 호출한다.
            - Lamda Function을 통해 리부팅할 때 reboot 옵션을 걸어서 재부팅을 하면 파일 무결성을 보장 가능하다.
        
        ![[Screenshot_from_2024-08-26_10-28-30.png]]
        
    - EC2 Instance Migration to difference AZ
        - 개요
            
            ![[image 2 10.png]]
            
            - 서로 다른 AZ 간에 이동은 아래와 같다.
                - 이동할 인스턴스로부터 AMI 이미지 생성
                - 이동할 인스턴스 제거
                - 다른 AZ에서 AMI 이미지로부터 인스턴스 생성
        - Cross-Account AMI Sharing
            
            ![[image 3 9.png]]
            
            - 서로 다른 계정과 AMI 공유가 가능합니다.
            - AMI를 공유해도 ownership엔 영향 없습니다.
            - 공유할 AMI는 EBS가 암호화되지 않았거나 암호화에 사용된 CMK(Customer Management Key)를 타겟에게 넘겨줘야 합니다.
        - AMI Sharing with KMS Encryption
            
            ![[image 4 9.png]]
            
            암호화되지 않은 볼륨을 사용한 AMI는 CMK를 사용할 IAM 권한을 타겟 계정에 부여해야 합니다.
            
            부여할 권한
            
            - kms: DescribeKey
            - kms: CreateGrant
            - kms: Decrypt
            - kms: GenerateDataKey
            - kms: ReEncrypt
            
        - Cross-Account AMI Copy
            
            ![[image 5 8.png]]
            
            - 공유되는 AMI를 복사(copy)하면 복사한 AMI의 소유자가 됩니다.
            - 복사를 하기 위해선 원본 AMI 소유권자가 해당 AMI가 저장된 EBS에 접근 권한을 줘야 합니다.
            - 원본 AMI가 암호화되었다면 공유와 동일하게 CMK 키를 공유해야 합니다.
            - 복사하는 동안에 자신만의 CMK 키로 다시 AMI를 재암호화할 수 있습니다.
            
            ![[image 6 8.png]]
            
    - [CCP] EC2 Image Builder
        
        ![[image 7 6.png]]
        
        - 컨테이너 이미지나 가상머신 생성의 자동화를 위한 서비스입니다.
        - EC2 ImageBuilder는 특정 스케쥴(e.g weekly, 패키지가 업데이트 되었을 때, …)마다 인스턴스를 만들고 해당 인스턴스를 통해 AMI 이미지를 만듭니다.
        - 또한, AMI 이미지가 만들어진 이후엔 인스턴스를 새로 만들어서 해당 이미지를 테스트합니다.
        - 테스트가 끝나면 해당 이미지를 Region에 배포합니다.
    - AMI in Production
        
        - IAM 정책들(Policies)을 통해 유저가 특정 AMI(특정 태그를 가진 AMI)만 사용하게 강제할 수 있다.
        
        ![[image 8 6.png]]
        
          
        
        - AWS Config를 사용해서 Non-approve AMI를 사용한 인스턴스들을 찾을 수 있다.
        
        ![[image 9 6.png]]
        

### 핵심 요약

- 핵심 요약 접기
    - AMI(Amazon Machine Image)는 EC2 인스턴스가 사용할 수 있는 커스터마이징 이미지다.
    - AMI는 리전에 종속된다.
    - Reboot 옵션을 설정하지 않으면 인스턴스를 중지하지 않고 AMI를 만들 수 있다.
    - 단, Reboot하지 않으면 파일 시스템 무결성을 보장하지 않는다.
    - 인스턴스 AZ 변경은 AMI를 만들고 해당 이미지로 새로운 AZ에서 인스턴스를 생성하면 된다.
    - EC2 Image Builder는 가상머신이나 컨테이너 이미지를 만들기 위해 사용되는 서비스다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 