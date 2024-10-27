---
⭕첫 학습날: 2024-10-01
⭕과목: Argo CD
⭕학습정도: 🤔중
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: false
복습: 추가 복습
🛑첫날: "✏첫날 : 2024/10/01"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤26일째❤
🛑4일후: "🥉4일뒤 : 2024/10/05"
🛑7일후: "🥈7일뒤 : 2024/10/08"
🛑14일후: "🥇14일뒤 : 2024/10/15"
4일후: "@2024년 10월 5일"
4일후(text): 2024/10/05
7일후: "@2024년 10월 8일"
7일후(text): 2024/10/08
14일후: "@2024년 10월 15일"
14일후(text): 2024/10/15
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/10/01
오늘과 첫학습날 사이: "26"
사이: "26"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[DevOps]] [[CI CD]]

### 단서 질문

- 웹훅(Web Hook)이란?
    
    일반적인 API는 클라이언트 측에서 서버에게 요청하는 방식으로 동작(Polling)하지만, 웹 훅의 경우에는 서버에서 특정 이벤트가 발생했을 때 서버에서 클라이언트로 요청을 보내는 방식입니다. 따라서, 역방향 API라고도 말합니다. 웹 훅은 서버 측에서 클라이언트에게 요청을 보내야 하기 때문에 주소가 필요합니다. 이를 Callback URL이라고 합니다.
    
    ![[image 34.png]]
    
- Argo CD의 구성 요소 3가지
    1. API Server
    2. Repository Server
    3. Application Controller

### 핵심 필기

- 전체 내용 접기
    
    ![[image 1 8.png]]
    
    - Argo CD API Server
        
        쿠버네티스 클러스터 내에서 존재하며 Web UI, CLI, CI/CD 시스템에 의해 ArgoCD API 서버의 API 호출이 일어난다.
        
        - 어플리케이션을 전체적으로 관리하는 역할을 한다.
        - 어플리케션의 상태를 체크하며 sync, rollback 등의 역할을 한다.
        - 레포지토리와 Credential을 K8S 내에 Secret으로 관리한다.
        - 인증과 외부 프로바이더에게 인증 위임을 할 수 있다.
        - Git Web Hooks의 Listener이며 forwarder이다.
    - Argo CD Repository Server
        
        깃허브 레포지토리와 연결되어 K8S의 Manifest를 생성하고 리턴하는 역할을 한다.
        
        레포지토리 URL, Branch, Tag, Params, Application Path 등을 통해서 K8S Manifest를 만든다.
        
    - Argo CD Application Controller
        
        실행되고 있는 Application과 레포지토리의 상태를 비교합니다.
        
        만약, 현재 실행 되는 Application과 레포지토리의 상태가 일치하지 않으면(OutOfSync) 유저가 정의한 액션을 수행합니다.
        
        Github에서 WebHook을 통해서 API 서버에 코드 업데이트가 됐다고 알림을 주고 업데이트를 트리거하지만 네트워크 문제 등으로 실제 업데이트가 되지 않을 수도 있습니다. 따라서, Application Controller를 통한 실시간 코드 모니터링이 필요합니다. 이 역할을 하는 것이 Application Controller입니다.
        

### 핵심 요약

- 핵심 요약 접기
    - Argo CD는 쿠버네티스 클러스터를 위한 선언적 GitOps 연속 전달 도구입니다.
    - 주요 구성 요소로는 API Server, Repository Server, Application Controller가 있습니다.
    - API Server는 애플리케이션 관리, 상태 체크, 인증 등을 담당합니다.
    - Repository Server는 Git 저장소와 연결되어 쿠버네티스 매니페스트를 생성합니다.
    - Application Controller는 실행 중인 애플리케이션과 저장소 상태를 비교하고 동기화합니다.
    - 웹훅을 통해 코드 업데이트 알림을 받지만, 실시간 모니터링도 수행합니다.
    - 이 아키텍처를 통해 Argo CD는 지속적인 배포와 애플리케이션 상태 관리를 효과적으로 수행합니다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 