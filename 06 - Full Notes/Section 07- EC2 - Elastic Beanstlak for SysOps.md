---
⭕첫 학습날: 2024-09-25
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: false
복습: 추가 복습
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
오늘1: "@2024년 10월 27일 오후 2:02"
오늘2: 2024/10/27
첫학습날text: 2024/09/25
오늘과 첫학습날 사이: "32"
사이: "32"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[Elastic Beanstalk]]

### 단서 질문

- Elastic Beanstalk란?
    
    개발자 관점에서 AWS 어플리케이션 배포의 자동화를 진행
    
- Elastic Beanstalk 비용은?
    
    사용한 리소스에 대한 금액만 낼뿐. Beanstalk 자체는 무료.
    

### 핵심 필기

- [SAA/DVA] Beanstalk Overview
    - Typical architecture: Web App 3-tier
        
        ![[image 66.png]]
        
          
        
    - Developer problems on AWS
        
        ![[image 1 18.png]]
        
        개발자 입장에서 AWS 사용 시 문제점
        
        - 인프라 관리
        - 코드 배포
        - DB, LB를 일일이 설정
    - Elastic Beanstalk - Overview
        
        ![[image 2 16.png]]
        
        Elastic Beanstalk란?
        
        - 개발자 관점에서 AWS의 어플리케이션을 배포합니다.
        - 매니지드 서비스
            - 자동으로 capacity 프로비저닝, 로드밸런싱, 스케일링, 어플리케이션 모니터링, 인스턴스 설정을 핸들링합니다.
            - 개발자는 코드만 작성하면 됩니다.
    - Elastic Beanstalk - Components
        
        ![[image 3 15.png]]
        
        Elastic Beanstalk - 구성요소
        
        - Application
        - Application 버전
        - 환경
            - 특정 어플리케이션을을 서비스하는 AWS Resource의 집합
            - 티어: Web Server Tier, Worker Tier
            - 여러 환경을 만들 수 있다. (dev, test, prod 등)
    - Elastic Beanstalk - Supported Platforms
        
        ![[image 4 15.png]]
        
          
        
    - Web Server Tier vs Worker Tier
        
        ![[image 5 12.png]]
        
        - Worker Environment로 Elastic Beanstalk를 생성하면 SQS Queue가 같이 만들어지고 해당 큐로 메시지가 전송되어 트래픽을 처리합니다.
    - Elastic Beanstalk Deployment Modes
        
        ![[image 6 12.png]]
        
          
        

### 핵심 요약

- 핵심 요약 접기
    - Elastic Beanstalk은 AWS에서 애플리케이션 배포를 자동화하는 개발자 친화적인 서비스입니다.
    - 사용된 AWS 리소스에 대해서만 비용이 청구되며, Elastic Beanstalk 자체는 무료입니다.
    - Web Server Tier와 Worker Tier 두 가지 환경 유형을 제공합니다.
    - 다양한 프로그래밍 언어와 플랫폼을 지원합니다.
    - 애플리케이션, 버전, 환경의 개념으로 구성되어 있습니다.
    - 개발, 테스트, 프로덕션 등 여러 환경을 생성할 수 있습니다.
    - 인프라 관리, 코드 배포, 로드 밸런서 설정 등을 자동화하여 개발자의 부담을 줄입니다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 