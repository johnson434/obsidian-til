---
⭕첫 학습날: 2024-09-20
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 1일 복습
🛑첫날: "✏첫날 : 2024/09/20"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤37일째❤
🛑4일후: "🥉4일뒤 : 2024/09/24"
🛑7일후: "🥈7일뒤 : 2024/09/27"
🛑14일후: "🥇14일뒤 : 2024/10/04"
4일후: "@2024년 9월 24일"
4일후(text): 2024/09/24
7일후: "@2024년 9월 27일"
7일후(text): 2024/09/27
14일후: "@2024년 10월 4일"
14일후(text): 2024/10/04
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/09/20
오늘과 첫학습날 사이: "37"
사이: "37"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[S3]] [[AWS Security]]

### 단서 질문

- 질문1

### 핵심 필기

- 전체 내용 접기
    - S3 Encryption
        
        ![[image 33.png]]
        
        - 암호화는 4가지 방법이 있다.(현재 DSSE-KMS도 추가되어 5개)
        - Server Side Encryption (SSE)
        - Client Side Encryption (CSE)
        
        ![[image 1 7.png]]
        
        - AWS가 key를 관리한다. 우리는 key에 제어권이 없다.
        - 요청 헤더에 명시한다.
        - 버켓이나 오브젝트를 새로 만들면 디폴트 설정임
        
        ![[image 2 7.png]]
        
        - KMS를 이용하여 해당 키를 통해 암호화한다.
        - Key에 제어권이 있다는 장점이 있다.
        - CloudTrail을 통해서 누가 키를 사용했는지 확인이 가능하다.
        
          
        
        ![[image 3 6.png]]
        
        - KMS 스펙에 따라 S3에 영향을 끼칠 수 있다.
        - Object 업로드, 다운로드 마다 KMS에 Key 요청을 한다.
        - KMS quota는 초당 5500, 10000, 3000이다.
        - 이 방법을 그래도 사용하고 싶으면 Service Quotas Console에 요청해라
        
          
        
        ![[image 4 6.png]]
        
        - Client Side에서 key와 함께 데이터를 업로드한다.
        - S3는 클라이언트의 키를 저장하지 않는다.
        - HTTPS를 무조건 사용해야 한다.
        - 헤더에 매 번 키를 같이 넣어야 한다.
        
        > [!important]  
        > 왜 HTTPS를 써야햐나? 여기서 의구심이 들었다. ALB를 사용하여 백엔드 서비스를 제공할 때는 내부적으로 인스턴스끼리 HTTP를 통해서 통신을 한다고 알고 있다. VPC를 사용하므로 인터넷망을 통하지 않아서 이는 문제가 발생하지 않는다.(VPC 내부적으로 암호화도 있음)반면에, S3는 공용서비스이므로 인터넷 망에서 접근이 가능하다.(퍼블릿 엔드포인트라는 인터넷망을 통해서 접근이 가능한 포인트가 있음) 만약, VPC Endpoint를 통해서 VPC 내부 망을 통해서만 전송을 하면 HTTPS를 사용하지 않아도 괜찮다.  
        
          
        
        ![[image 5 6.png]]
        
        - 클라이언트가 암호화 후에 데이터를 전달한다.
        - 클라이언트가 직접 암호화하고 직접 복호화해야 한다.
        
          
        
        ![[image 6 6.png]]
        
          
        
    - Aboud DSSE-KMS
        
        새로 나온 암호화 기법인데 아직 시험에 안나옴
        
    - S3 Default Encryption
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0348.jpg]]
        
        - Bucket Policy를 사용하면 Encryption을 확인하고 요청을 거부할 수 있다.
        - S3 업로드 이전에 버켓 정책을 먼저 확인하고 조건을 만족하는 경우에만 암호화가 동작한다.
    - S3 CORS
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0349.jpg]]
        
        - Cross-Origin Resource Sharing(CORS)를 의미합니다.
        - 스키마 + 호스트 주소 + 포트 번호로 식별합니다.
        - 웹브라우저 기반 기술로 origin이 다른 곳에 요청할 때 사용됩니다.
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0350.jpg]]
        
        1. 브라우저로부터 A origin에 요청
        2. A origin에서 다른 B origin에 자원을 가져오는 코드가 작성되어 있음
        3. 브라우저는 B 오리진에 프리플라이 request를 통해 A 오리진에서 너를 명시했는데 써도 되냐고 물어봄
        4. 만약, B에서 명시를 했다면 요청을 허가하는 응답을 보냄
        5. 프리플라이트가 끝났으면 결과에 따라 웹브라우저가 요청을 보낼 수 있음
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0351.jpg]]
        
        - 클라이언트가 cross-origin 요청을 S3 버켓에 하면 S3 버켓의 헤더에 해당 설정을 해줘야함.
        - 특정 오리진을 명시하거나 모두 허용 가능하게 설정할 수 있음.
    - S3 MFA Delete
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0352.jpg]]
        
        - S3가 MFA를 사용하는 곳
            - 이전 버전 오브젝트를 삭제하는 것
            - 버저닝을 중단하는 것
        - MFA가 사용되지 않는 경우
            - 버저닝 활성화
            - 삭제된 버전 리스트
        - 오직 bucket owner MFA Delete 설정이 가능함
    - S3 Access Logs
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0353.jpg]]
        
        - 심사 목적으로 S3 버켓의 모든 액션을 로그로 남기고 싶을 수가 있다.
        - S3로 오는 모든 요청은 또 다른 S3 버킷에 기록된다.
        - Athena와 같은 툴들로 해당 로깅 버켓을 분석 가능하다.
        - 로깅 버켓은 모니터링할 버켓과 동일한 리전에 존재해야 한다.
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0354.jpg]]
        
        - 로깅 버켓을 모니터링하지 말 것 → 로깅 순환 호출됨
    - S3 Pre-signed URLs
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0355.jpg]]
        
        - 사전 승인 URL은 특정 기간동안 S3 버킷에 액션이 가능한 URL을 말합니다.
        - S3 Console로 제작: 1분 ~ 720분(12시간)
        - AWS CLI로 제작: default 1시간 최대 168시간
        - 해당 링크로 GET, PUT이 가능하다.
        
          
        
        - 사용 예시
            - 프리미엄 유저만 다운 가능한 영상
            - 매 번 바뀌는 유저들이 다운로드 가능하게 동적으로 만드는 URL
            - 임시로 유저에게 특정 버킷 공간에 업로드 가능하게 설정
    - Glacier Vault Lock & S3 Object Lock
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0356.jpg]]
        
        - WORM (작성은 1번만하고 조회만) 모델을 적용하는데 사용된다.
        - 해당 설정을 적용하면 루트 유저부터 AWS까지 어떠한 사용자도 해당 볼트 삭제가 불가능하다.
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0357.jpg]]
        
        retention: 보유
        
        - Object Lock은 Vault Lock과 달리 Object를 잠금니다.
        - 특정 기간동안 Object 삭제를 방지합니다.
        - Retention mode - Compliance
            - 어떤 유저도 데이터 수정이 불가능
            - Retention 모드 변경이 불가능하며 보유 기간도 줄일 수 없음
        - Retention mode - Governance
            - 대부분의 유저는 수정이 불가능하면 몇몇 특정 유저는 수정이 가능함
            - Retention 모드랑 보유 기간 모두 변경 가능
        - Retention Period: 보유 기간으로 해당 기간동안 오브젝트 수정 불가. 기간 연장은 불가능함
        - Legal Hold
            - retention 기간이 지나도 잠시동안 오브젝트 삭제를 유예시킴
            - s3:PutObjectLegalHoldIAM이라는 IAM 권한으로 Legal Hold를 주거나 제거할 수 있음.
        
          
        
    - S3 Access Points
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0358.jpg]]
        
        - 버켓의 액세스 포인트를 통해서 유저가 접근하게 만든다.
        - 버켓 하나 당 여러 개의 Access Point가 존재할 수 있다.
        - 액세스 포인트엔 적절한 IAM 권한을 가지면 접근이 가능하다.
        - Read Write 권한을 별개로 부여해서 특정 권한만 사용하게 설정할 수도 있다.
        - VPC 내에 Access Point를 만들어서 내부 트래픽으로만 접근 가능하게 만들거나 인터넷 망 엔드포인트를 사용해서 외부에서 접근 가능하게 만들 수도 있다.
        - 액세스 포인트는 다음 두 가지를 가진다.
            - DNS name (Internet Origin이거나 VPC Origin)
            - Access Point Point Policy - manage security at scale(대규모 보안도 관리한다는 뜻)
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0359.jpg]]
        
        - VPC 내부에서만 접근 가능한 Access Point를 정의할 수도 있다.
        - VPC EndPoint(Gateway나 Interface)를 만들어야 S3 VPC Origin Access Point에 접근이 가능하다.
        - VPC EndPoint 정책으로 Access Point랑 S3 Bucket 모두 접근이 가능하게 설정해야 한다.
        
          
        
    - S3 Multi-Region Access Points
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0360.jpg]]
        
        - 여러 Region에 퍼져있는 S3 중에서 가장 latency와 네트워크 혼잡도(congestion)이 낮은 곳으로 자동 라우팅해준다.
        - 여러 Region의 S3는 양방향 동기화가 이뤄지며 이를 통해 동일한 데이터를 조회할 수 있다.
        - s3로 요청이 실패했을 때 자동으로 failover control이 이뤄져 정상적인 S3로 요청을 보낸다.
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0361.jpg]]
        
          
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0362.jpg]]
        
          
        
    - S3 VPC Endpoints
        
        ![[AWS_Certified_SysOps_Slides_v31_page-0363.jpg]]
        
        - 인터넷망을 통해서 접근하는 경우 Internet Gateway를 통해서 S3 Bucket에 접근한다.
        - VPC 내부 네트워크를 사용해서 VPC Endpoint Gateway를 통해서 접근하면 인터넷 망으로 트래픽이 전달되지 않는다.
        - VPC를 사용할지는 S3 Bucket Policy를 통해 설정이 가능하다.

### 핵심 요약

- 핵심 요약 접기
    
    - AI 요약
        - S3 Encryption: 다양한 암호화 방식을 제공하여 데이터 보안을 강화합니다.
        - S3 CORS: 웹 애플리케이션에서 cross-origin 리소스 공유를 가능하게 합니다.
        - S3 MFA Delete: 중요한 버전 삭제 및 버저닝 비활성화에 추가 보안을 제공합니다.
        - S3 Access Logs: 버킷 액세스 활동을 모니터링하고 분석할 수 있습니다.
        - S3 Pre-signed URLs: 임시 액세스를 위한 URL을 생성하여 보안을 유지합니다.
        - S3 Object Lock: WORM 모델을 구현하여 데이터 무결성을 보장합니다.
        - S3 Access Points: 대규모 데이터 액세스 관리를 간소화합니다.
        - S3 Multi-Region Access Points: 글로벌 애플리케이션의 성능을 최적화합니다.
    
      
    

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 