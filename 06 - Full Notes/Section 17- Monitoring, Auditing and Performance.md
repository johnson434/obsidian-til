---
⭕첫 학습날: 2024-10-09
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 7일 복습
🛑첫날: "✏첫날 : 2024/10/09"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤18일째❤
🛑4일후: "🥉4일뒤 : 2024/10/13"
🛑7일후: "🥈7일뒤 : 2024/10/16"
🛑14일후: "🥇14일뒤 : 2024/10/23"
4일후: "@2024년 10월 13일"
4일후(text): 2024/10/13
7일후: "@2024년 10월 16일"
7일후(text): 2024/10/16
14일후: "@2024년 10월 23일"
14일후(text): 2024/10/23
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/10/09
오늘과 첫학습날 사이: "18"
사이: "18"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0.4"
진행바: 🟩🟩🟩🟩⬜⬜⬜⬜⬜⬜ 40%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[Monitoring]]

### 단서 질문

- 질문1

### 핵심 필기

- 전체 내용 접기
    - CloudWatch Metrics
        - AWS CloudWatch Metrics
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0462.jpg]]
            
            **AWS CloudWatch Metrics**
            
            - CloudWatch는 AWS의 모든 서비스의 메트릭스를 제공한다.
            - Metric은 모니터링이 가능한 변수다. (CPU 사용량, 네트워크 트래픽)
            - Metrics는 네임스페이스(namespaces)에 속한다.
            - Dimension은 매트릭의 속성이다. (Instance ID, 환경, 기타)
            - 매트릭 당 최대 30개 디멘션이 있다.
            - 매트릭스들의 CloudWatch 대시보드를 만들 수 있다.
        - EC2 Detailed Monitoring
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0463.jpg]]
            
            EC2 Detailed Monitoring
            
            - EC2 인스턴스의 매트릭스는 5분 간격으로 수집됩니다.
            - Detailed monitoring을 사용하면 데이터를 1분마다 수집 가능합니다.(비용이 든다.)
            - ASG 스케일링은 모니터링을 기반으로 하므로 Detailed Monitoring을 통해 더 빠른 스케일링이 가능하다.
            - Free Tier는 10개 Detailed Monitoring 매트릭스를 허용한다.
            - Note: EC2 메모리 사용량은 디폴트로 매트릭에 포함되지 않는다.(커스텀 매트릭 설정을 통해 CloudWatch에 푸시해야 한다.)
    - CloudWatch Custom Metrics
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0464.jpg]]
        
        **CloudWatch Custom Metrics**
        
        - CloudWatch에서 기본으로 제공하는 메트릭스가 아닌 커스텀하게 제공할 수도 있다.
        - 커스텀 메트릭스의 예시:
            - RAM
            - disk 공간
            - 로그인 유저
        - PutMetricData API를 통해 CloudWatch에 푸시한다.
        - 매트릭스에 인스턴스 ID나 Environment.name을 통해 세분화가 가능하다.
        - 매트릭 해상도 (StorageResolution API엔 두 가지 파라미터가 올 수 있다.
            - Standard(1분 주기로 수집)
            - High Resolution(1/5/10/30초 주기로 수집: 높은 해상도로 높은 비용이 든다)
        - **중요:** 매트릭스는 과거 2주부터 미래 2시간까지 타임스탬프로 찍힌 데이터를 받는다.
        
        > [!important]  
        > 차원(dimension): 메트릭과 연관된 속성 또는 특징으로, 메트릭 데이터를 특정 기준에 따라 세분화하는 데 사용됩니다  
        
    - 225. CloudWatch Dashboards
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0465.jpg]]
        
        **CloudWatch DashBoards**
        
        - **대시 보드는 글로벌이다.**
        - **특정 Region에 한정되지 않으며 다른 계정의 그래프를 포함할 수도 있다.**
        - 대시보드에 Time zone은 변경 가능
        - 대시보드 리프레시 주기를 설정 가능하다. (10초, 1분, 2분, 5분, 15분)
        - AWS 계정이 없는 사람과도 공유가 가능하다. (AWS Congnito를 통해서)
        
          
        
        CloudWatch DashBoards 비용
        
        - 대시보드 3개에 최대 50개 매트릭스까지는 무료다. (매트릭스는 대시보드당 50개가 아니라 총 개수)
        - 이후엔 대시보드 하나 당 한달의 $3
    - 226. CloudWatch Logs
        - CloudWatch Logs
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0466.jpg]]
            
            **CloudWatch Logs**
            
            - Log Groups: 임의의 이름을 사용한다. 보통 어플리케이션 이름을 사용한다.
            - Log Stream: 어플레키이션의 인스턴스들, 로그파일들, 컨테이너들에서 로그 Stream이 발생한다. (Stream: 흐름 연속해서 로그가 발생하는 것을 스트림으로 표현?)
            - 로그 기한을 설정할 수 있다. (1일부터 10년 또는 삭제되지 않도록 만들 수 있다)
            - CloudWatch Logs는 로그를 다음과 같은 서비스에 보낼 수 있다.
                - S3
                - Kinesis Data Streams
                - Kinesis Data Firehose
                - AWS Lambda
                - OpenSearch
            - 로그는 디폴트로 암호화된다.
            - 자신이 설정한 키로 KMS 암호화 설정을 할 수 있다.
        - CloudWatch Logs - Sources
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0467.jpg]]
            
            **CloudWatch Logs의 소스들(로그가 발생하는 곳)**
            
            - SDK, CloudWatch Logs Agent, CloudWatch Unified Agent
            - Elastic Beanstalk: collection of logs from application
            - ECS: collection from containers
            - AWS Lambda: collection from function logs
            - VPC Flow Logs: VPC specific logs
            - API Gateway
            - CloudTrail based on filter
            - Route53: Log DNS queries
        - CloudWatch Logs Insights
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0468.jpg]]
            
            CloudWatch Logs Insights
            
            - 쿼링을 통해서 로그 검색이 가능하다.
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0469.jpg]]
            
            CloudWatch Logs Insights
            
            - CloudWatch Logs를 검색하고 분석할 수 있다.
            - 예시: 특정 IP 찾기, 로그에서 Error 발생 횟수 찾기
            - 쿼리를 위해 특화된 언어를 지원한다.
                - AWS 서비스와 JSON 로그 이벤트들에서 자동으로 필드를 발견한다.
                - 상태에 따라서 요구된 이벤트 필드를 추출한다.?
                - 쿼리를 저장하고 CloudWatch Dashboards에 추가 가능하다.
                - 다른 AWS 계정에 있는 로그 그룹에서 검색할 수도 있다.
                - 쿼리 엔진이며, 실시간 엔진이 아니다.
        - CloudWatch Logs - S3 Export
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0470.jpg]]
            
            CloudWatch Logs - S3 Export
            
            - 로그 데이터를 Export하기 위해선 최대 12시간이 걸린다.
            - CreateExportTask를 통해서 Export가 가능하다.
            - 실시간으로 Export가 불가능하다. 이를 실시간으로 구현하려면 Logs Subscriptions를 대신 써라.
        - CloudWatch Logs Subscriptions
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0471.jpg]]
            
            **CloudWatch Logs Subscriptions**
            
            - 로그 처리 및 분석을 위해서 실시간 로그 수집이 가능하다.
            - Subscriptions 필터를 통해 받은 로그를 Kinesis Data Streams, Kinesis Data Firehose, Lambda 등에 보내라
            - **Subscription Filter**: 도착지에 보낼 로그를 필터링하는 역할
        - CloudWatch Logs Aggregation Multi-Account & Multi Region
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0472.jpg]]
            
            **CloudWatch Logs Subscriptions를 통한 멀티 계정, 멀티 리전 로그 집약**
            
            - Subscription FIlter를 통해 받은 로그를 하나에 계정의 Kinesis Data Streams로 전송하면 단, 한 개의 어플리케이션에서 로그 집약이 가능하다.
        - CloudWatch Logs Subscriptions
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0473.jpg]]
            
              
            
    - 227. CloudWatch Logs - Hands On
    - 228. CloudWatch Logs - Live Tail - Hands On
    - 229. CloudWatch Alarms
        - CloudWatch Alarms
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0474.jpg]]
            
            **CloudWatch Alarms**
            
            - 특정 매트릭의 상태를 보고 알림(Notifications)을 트리거하기 위해 사용된다.
            - 다양한 옵션이 있다. (샘플링, 퍼센트, max, min, etc..)
            - Alarm 상태
                - OK: 알람을 울릴 준비가 된 것들
                - INSUFFICIENT_DATA: 알람 실행을 위한 데이터가 부족한 것들
                - ALARM: 알람 조건을 만족하여 알람이 울리는 상태 혹은 울리기 전
            - 기간
                - 매트릭을 평가해야하므로 몇초가 걸린다.
                - 높은 해상도 커스텀 매트릭도 알람 조건으로 사용 가능하다.
        - CloudWatch Alarm Targets
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0475.jpg]]
            
            **CloudWatch Alarm Targets**
            
            - EC2 인스턴스를 대상으로 알람을 통해 다음 작업을 할 수 있다.
                - Stop
                - Terminate
                - Reboot
                - Recover
            - AutoScaling 액션을 트리거할 수 있다.
            - 알림을 SNS에 보낼 수 있다.
        - CloudWatch Alarms - Composite Alarms
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0476.jpg]]
            
            **CloudWatch Alarms - Composite Alarms**
            
            - CloudWatch Alarm은 하나의 매트릭에 의해 동작합니다.
            - Composite Alarm은 여러 개의 알람을 모니터링합니다.
            - 다른 알람들이 동작하는지 AND와 OR 조건을 사용해서 동작합니다.
            - Alarm noise(알람이 너무 자주 울리는 일)를 피하기 위해 사용할 수 있습니다.(AND OR 조건으로 특정 조건에서만 알람이 울리게 설정)
            
              
            
        - EC2 Instance Recovery
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0477.jpg]]
            
            **EC2 Instance Recovery**
            
            클라우드 워치 알람을 통해 EC2 인스턴스의 상태를 확인(매트릭스를 통해서)하다가 이상이 발생하면 인스턴스를 리부트할 수 있습니다. 동시에 알람을 SNS 토픽에 보낼 수도 있습니다.
            
            - 상태 확인
                - 인스턴스 상태 = EC2 VM 확인
                - System Status =-
        - CloudWatch Alarm - Good to Know
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0478.jpg]]
            
            CloudWatch Alarm에 대해서 알아두면 좋을 사실들
            
            - 알람은 CloudWatch Logs에서 메트릭스 필터를 통해서도 만들 수 있습니다.
                - 예: 필터를 통해 로그에서 Error가 나오는 횟수를 측정 → n번 이상 나오면 알람
    - 230. CloudWatch Alarms Hands On
        
          
        
    - 231. CloudWatch Synthetics
        - CloudWatch Synthetics Canary
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0479.jpg]]
            
            **CloudWatch Synthetics Canary (인공 카나리)**
            
            - API, URL, 웹사이트를 모니터링하기 위해 작성하는 스크립트
            - 커스터머가 하는 행위를 프로그래밍으로 재현하여(인공적으로 위조) 이슈가 발생하는지 체크한다.
            - 엔드포인트의 가용성과 지연성을 체크하고 데이터 로드 속도와 UI 스크린샷을 찍어준다.
            - CloudWatch Alarm과 통합해서 사용할 수 있다.
            - 스크립트는 NodeJS나 파이썬으로 작성한다.
            - 헤드리스 구글 크롬 브라우저를 통해 동작한다.
            - 한 번만 실행하거나 주기적으로 실행할 수 있다.
        - CloudWatch Synthetics Canary Blueprints
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0480.jpg]]
            
            **CloudWatch Synthetics Canary Blueprints**
            
            - Heartbeat Monitor: URL 로딩, 스크린샷, HTTP 아카이브 파일 저장
            - API Canary: REST API 조회 작성 기능 테스트
            - Broken Link Checker: 잘못된 URL 링크가 있는지 확인
            - Visual Monitoring: 스크린샷을 통해 비교
            - Canary Recorder: 사용자의 액션을 기록했다가 해당 액션을 재연하는 스크립트를 짜준다.
            - GUI Workflow Builder: 웹페이지에서 발생하는 모든 액션 확인
            
              
            
    - 232. [SAA/DVA] Amazon EventBridge
        - Amazon EventBridge (formely CloudWatch Events)
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0481.jpg]]
            
            - 스케쥴링: Cron Job을 사용해서 특정 스케쥴마다 Event 트리거 가능
            - 이벤트 패턴: 서비스가 어떤 동작을 하면 Event 트리거 가능
            - 람다 Function을 트리거하거나 SQS/SNS에 메시지를 보낸다.
        - Amazon EventBridge Rules
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0482.jpg]]
            
            **Amazon EventBridge Rules**
            
            - 특정 리소스로부터 이벤트를 Filter Events로 필터링해서 받는다.
            - EventBridge는 이를 통해서 이벤트를 JSON 형식으로 바꾼 후에 Destinations로 전송한다.
        - Amazon EventBridge
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0483.jpg]]
            
            - Amazon EventBridge는 AWS 리소스에서 이벤트를 전송하는 이벤트 버스 역할을 합니다.
            - 서드파티로 DATADOG와 같은 이벤트 버스를 사용할 수도 있습니다.
            - 이벤트 버스는 리소스 기반 정책을 통해 다른 AWS 계정에서도 접근이 가능합니다.
            - 이벤트 버스로 통해 전송되는 이벤트들을 아카이브(기록) 가능합니다.(무기한 or 특정 기간동안)
            - 아카이브 된 이벤트는 다시 리플레이가 가능합니다.
        - Amazon EventBridge - Schema Registry
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0484.jpg]]
            
            **Amazon EventBridge - Schema Registry**
            
            - 스키마 레지스트리는 데이터의 구조를 정의하여 중앙에서 관리합니다.
            - 버저닝이 가능합니다.
        - Amazon EventBridge - 리소스 기반 정책
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0485.jpg]]
            
            **Amazon EventBridge - 리소스 기반 정책**
            
            - 특정 이벤트 버스를 위해 권한을 관리한다.
            - 예: 다른 계정이나 리전으로부터 이벤트를 수신하거나 거부한다.
            - 사용 예시: AWS Organization으로부터 이벤트를 집약하여 하나의 계정이나 리전에 저장한다.
    - 233. [SAA/DVA] Amazon EventBridge - Hands On
    - 234. EventBridge Content Filtering - Hands On
    - 235. EventBridge Input Transformation - Hands On
    - 236. Service Quotas Overview
        - Service Quotas CloudWatch Alarms
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0486.jpg]]
            
            **Service Quotas CloudWatch Alarms**
            
            - 서비스의 Quota(한계량)에 도달하기 전에 알림을 준다.
        - Alternative: Trusted Advisor + CW Alarms
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0487.jpg]]
            
              
            
    - 237. Service Quotas Hands On
    - 238. [SAA/DVA] CloudTrail
        - Cloud Trail
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0488.jpg]]
            
            **AWS CloudTrail**
            
            - AWS 계정에 대해 거버넌스, 컴플라이언스, 그리고 감사 기능을 제공한다
            - 기본적으로 활성화
            - 모든 이벤트와 API 호출을 기록한다.
            - CloudTrail 로그를 CloudWatch나 S3에 넣을 수 있다.
            - 모든 리전에 적용 가능(기본 설정)하며 리전 하나에만 적용도 가능하다.
            - 리소스가 삭제되면 CloudTrail을 먼저 체크하라.
        - CloudTrail Diagram
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0489.jpg]]
            
            - 만약, CloudTrail 기록이 90일보다 오래 가길 원한다면 CloudWatch나 S3 Bucket으로 보내면 된다.
        - CloudTrail Events
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0490.jpg]]
            
            CloudTrail이 다루는 이벤트는 3가지가 있다.
            
            - Management Events
                - AWS 리소스에서 수행되는 작업들
                - 예:
                    - 보안 설정 (IAM AttachRolePolicy)
                    - 라우팅 데이터를 위한 룰 설정 (Create Subnet)
                    - 로깅 설정(Create Trail)
                - 디폴트 설정으로 CloudTrail을 Management Events를 모두 로깅한다.
                - Read와 Write 로깅을 분리 가능하다.
            - Data Events
                - 디폴트 설정으로 Data Events는 로그를 남기지 않는다.
                - Amazon S3 Level Activity 이벤트들이 Data Events에 속한다.
                - AWS 람다 실행 횟수도 Data Events에 속한다.
        - CloudTrail Insights
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0491.jpg]]
            
            **CloudTrail Insights**
            
            - 비정상적인 행동이 발생을 감지하기 위해선 CloudTrail Insight를 계정에서 활성화하면 된다.
                - 예:
                    - 정확하지 않은 리소스 프로비저닝
                    - 서비스 리미트 히팅
                    - Bursts of AWS IAM Actions(IAM 관련 API 호출이 급격하게 많아질 때)
                    - Gaps in periodic Maintenance Activity(주기적으로 실행되는 유지 관리 작업이 일정 시간 중단되었거나 스킵된 경우)
            - 비정상적인 행동의 기준을 정하기 위해서 일반적인 매니지먼트 이벤트도 분석한다.
            - 정상적인 이벤트를 분석한 후에 발생하는 모든 이벤트를 분석한다.
                - CloudTrail Console에 비정상적인 이벤트가 발생했다고 뜨고
                - 이벤트가 S3에 보내진다.
                - 비정상적인 이벤트가 발생했을 때, 자동화를 통해 특정 작업을 하고 싶다면 EventBridge를 통해서 이를 처리할 수도 있다.
            
              
            
        - CloudTrail Events Retention
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0492.jpg]]
            
            **CloudTrail Events Retention**
            
            - 이벤트는 90일 저장된다.
            - 이벤트를 더 길게 보관하기 위해선 S3로 로그를 보내고 이를 Athena를 통해서 조회 가능하다.
    - 239. [CCP/SAA/DVA] CloudTrail - Hands On
    - 240. [SAA/DVA] CloudTrail - EventBridge Integration
        - Intercept API Calls
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0493.jpg]]
            
              
            
        - Amazon EventBridge + CloudTrail
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0494.jpg]]
            
              
            
    - 241. CloudTrail for SysOps
        - Log File Integrity Validation
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0495.jpg]]
            
            CloudTrail - Log File Integrity Validation (로그 파일 통합 유효성 검사)
            
            - Digest Files
                - 로그파일들을 해시하여 레퍼런스하고 있다.
                - 로그 파일과 동일한 버킷의 다른 폴더에 저장된다.
            - 해싱 값을 통해서 로그 파일이 수정됐는지 확인 가능하다.
            - 해싱은 SHA-256을 통해 이뤄지며, RSA와 같이 SHA-256을 써서 디지털 서명을 한다.
            - CloudTrail을 IAM으로 보호 가능하다.
            
            > [!important]  
            > SHA-256이란? 해시 함수로, 입력된 데이터를 고정된 256비트 길이의 해시 값으로 변환합니다. 주로 데이터의 무결성 검증에 사용되며, 같은 입력에 대해 항상 동일한 해시 값을 생성하지만, 작은 변경만 있어도 완전히 다른 해시 값이 나옵니다. 암호화 목적으로는 사용되지 않고, 비밀번호 저장, 데이터 무결성 체크 등에 많이 쓰입니다.  
              
            > [!important]  
            > RSA란? 비대칭 암호화 알고리즘입니다.공개키와 개인키라는 두 개의 키를 사용하여 데이터를 암호화하고 복호화합니다. 공개키로 데이터를 암호화하면, 오직 해당 공개키에 대응하는 개인키로만 복호화할 수 있습니다.주로 데이터 암호화와 디지털 서명에 사용되며, 보안 통신의 중요한 부분입니다.  
              
            > [!important]  
            > Digest란? 전체 메시지에서 암호화 해쉬 함수에 의해 생성된 작은 값입니다.  
            
        - Integration with EventBridge
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0496.jpg]]
            
            **CloudTrail과 EventBridge 통합**
            
            - 사용자의 계정에서 발생하는 모든 API 호출에 반응하기 위해 사용된다.
            - **CloudTrail은 실시간이 아니다.**
                - API 호출 이벤트 전달엔 15분이 걸린다.
                - S3 Bucket에 로그파일 전달은 5분 마다 실행된다.
        - Organizations Trails
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0497.jpg]]
            
            CloudTrail - 조직 Trails
            
            - 동일한 AWS Organization에 속한 계정들이 CloudTrail을 공유한다.
            - 모든 계정들은 동일한 이름을 가진 CloudTrail을 가진다. (그림에선 MyOrganizationTrail)
            - 계정들은 CloudTrail을 볼 수는 있지만 수정을 불가하다.
    - 242. [SAA] AWS Config Overview
        - AWS Config
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0498.jpg]]
            
            **AWS Config**
            
            - AWS 리소스의 설정을 모니터링하고 규정 준수 상태에 있는지 확인합니다.
            - AWS Config를 통해서 해결 가능한 질문들
                - 모든 곳에서 SSH로 접속 가능하게 설정되어 있나?
                - 내 버킷에 퍼블릭 액세스 접근이 있나?
                - ALB 설정이 어떻게 변했나?
            - 변경에 대해서 SNS로 알림을 받을 수 있다.
            - AWS Config는 리전 서비스다.
            - 서로 다른 리전과 계정의 로그를 하나에 집약할 수 있다.
            - configuration 데이터를 S3에 저장할 수 있다. (Athena를 통해 분석 가능)
        - Config Rules
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0499.jpg]]
            
            **Config Rules**
            
            - AWS에서 매니지하는 Config Rule이 있다.
            - 커스텀 Config Rule을 만들 수도 있다. (AWS Lambda를 통해서 설정)
                - ex: EBS Volume Type이 gp2
                - ex: EC2 인스턴스의 타입이 t2 micro
            - Rule은 다음과 같은 상황에 평가된다.
                - 설정 값이 변경됐을 때
                - And / or: 특정 시간 주기
            - AWS Config Rule은 액션 자체를 막진 않는다.
            - 비용: 프리티어가 없다. 리전의 하나의 아이템 레코드마다 $0.003이며 리전에서 config 평가가 일어날 때마다 $0.001이 든다.
        - AWS Config Resource
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0500.jpg]]
            
            - **특정 AWS 리소스의 API 호출 기록을 시간에 따라 확인**하는 기능
        - Config Rules - Remediations
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0501.jpg]]
            
            **Config Rules - Remediations(교정)**
            
            - 규정에 맞지 않는 리소스를 SSM Automation Documents를 통해 교정이 가능하다.
            - AWS에서 관리하는 Documents나 custom Documets를 사용한다.
                - Lambda를 호출하는 custom Documents를 실행하는 것도 방법
                - Remediation 횟수 제한도 걸 수 있다.
        - Config Rules - Notifications
            
            ![[AWS_Certified_SysOps_Slides_v31_page-0502.jpg]]
            
              
            
    - 243. [SAA] Config Hands On
    - **244. Config - Aggregators(Test 중요!!)**
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0503.jpg]]
        
        **AWS Config - Aggregators**
        
        - Aggregator 계정을 만들어서 CloudFormation 데이터를 중앙화할 수 있다. (모든 데이터를 Aggregator에서 본다)
        - 여러 계정이나 리전으로부터 Rule 리소스, 기타 등등 상태를 수집한다.
        - AWS Organization의 계정을 사용하면 해당 조직의 데이터는 아무 권한 없어도 수집이 가능하다.
        - 만약, 조직을 사용하지 않으면 수집할 계정에서 authorize Aggregator를 해야 한다.
        - Rule은 각 계정에서 만들어진다.
        - CloudFormation StackSets을 통해서 Rule을 여러 계정에 배포 가능하다.
    - **245. [SAA] CloudWatch vs CloudTrail vs Config(Test 중요!!)**
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0504.jpg]]
        
          
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0505.jpg]]
        
          
        
    - 퀴즈 16: Monitoring, Auditing, and Performance Quiz
        
          
        

### 핵심 요약

- 핵심 요약 접기
    
    - CloudWatch Metrics
    - CloudWatch Custom Metrics
    - CloudWatch Dashboards
    - CloudWatch Logs
    - CloudWatch Logs - Live Tail
    - CloudWatch Alarms
    - CloutWatch Synthetics
    - Amazon EventBridge
        - Amazon EventBridge - Schema Registry
            
              
            
            infer 추론하다.
            
        - Amazon EventBridge - Resource-based Policy
    - EventBridge Content Filtering
        
          
        
    - EventBridge Input Transformation
    - Service Quotas Overview
        
          
        
        Quotas 할당량
        
        - Serivce Quotas는 여러 리소스에 사용할 수 있다.
    - CloudTrail
        
        CloudTrail에 기록된 로그는 90일이 지나지 않은 기록만 사용 가능하고 이 이상 시간이 지난 애들은 S3에 저장하거나 CloudWatch로 보내야 보존이 가능하다.
        
    - CloudTrail - EventBridge Integration
    - CloudTrail for SysOps
    - Config Overview
    - Config Aggregators
    - CloudWatch vs CloudTrail vs Config
    
      
    

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 