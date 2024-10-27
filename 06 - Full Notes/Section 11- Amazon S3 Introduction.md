---
⭕첫 학습날: 2024-10-02
⭕과목: AWS
⭕교재: Ultimate AWS Certified SysOps Administrator Associate 2024
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: false
🧠장기기억: false
복습: 14일 복습
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
[[AWS]] [[Ultimate AWS Certified SysOps Administrator Associate 2024]] [[S3]]

### 단서 질문

- S3는 무엇인가요?
    
    AWS에서 제공하는 무한대로 확장가능한 저장 공간
    
- S3는 스코프 범위가 어떻게 되나요?
    
    S3의 Region에 설정합니다. 그러나, Region에 한정되지 않고 전세계에서 접근 가능합니다.
    
- S3의 사용 예시 3가지만
    1. archive: 기록 백업용
    2. Media Hosting: 미디어 파일을 호스팅해준다.
    3. Hybrid Cloud Storage: 온프로미스와 같이 사용하는 저장 공간
- 버켓 네이밍룰은 어떻게 되나요?
    
    영어 소문자나 숫자로 시작하며 대문자는 사용이 불가능하다. 또한 하이픈(’-’)을 사용할 수 있다.
    
    또한, AWS 전체에서 이름이 유일(unique)해야 한다.
    
- S3 Versioning이랑?
    
    오브젝트에 덮어씌울 때마다 버전을 사용하여 이전 오브젝트를 복구할 수 있게 설정한다.
    
- Bucket Policy로 할 수 있는 일
    - 특정 Organization만 접근 허가
    - S3 업로드 시에 암호화 강제하기
    - S3 작업 시에 MFA 인증 받기
- AWS S3로 호스팅한 웹사이트로 요청을 했는데 403 Forbidden 에러가 나오면 원인이 뭔가?
    
    S3에 퍼블릭 리드 권한을 안줘서
    
- 버저닝을 Enable하면 오브젝트의 버전이 어떻게 되는가?
    
    null로 시작한다.
    
- 버저닝을 중단하면 오브젝트의 버전들은 어떻게 되는가?
    
    유지된다.
    

### 핵심 필기

- 전체 내용 접기
    - S3 Overview
        
        ![[image 31.png]]
        
          
        
        ![[image 1 5.png]]
        
        - Hybrid Cloud Storage: 온프로미스와 클라우드를 병행해서 사용
        - 오른쪽 나스닥과 시스코는 S3의 사용 예시
        
          
        
        ![[image 2 5.png]]
        
        - S3는 Object라는 단위로 파일을 Bucket에 저장한다.
        - Bucket의 이름은 모든 AWS에서 유니크하다.
        - Bucket은 Region Level에서 정의된다. 다른 Region에선 사용 불가능
        
        ![[image 3 4.png]]
        
        - Object는 key를 가진다.
        - key는 prfix + object name으로 이뤄진다. (Bucket 명과 s3프로토콜은 key에 포함되지 않음.)
        
        ![[image 4 4.png]]
        
        - 오브젝트의 content에 관한 설명입니다.
        - 최대 크기는 5테라바이트
        - 5GB 이상의 파일을 올리려면 multi-part로 분해해서 업로드한다.
        - 메타데이터 (키와 값의 쌍으로 시스템 정보나 유저 정보가 들어간다)
        - Tags
        
          
        
    - S3 Security: Bucket Policy
        - Security
            
            ![[image 5 4.png]]
            
            - 유저 기반
                - IAM Policies - IAM에서 특정 유저에게 API 호출을 허락하는 방법
            - 리소스 기반
                - Bucket Policies - 버켓 내부에서 접근 권한을 설정하는 방법 - 다른 계정도 허락 가능하며 JSON 형식으로 작성하여 Bucket ACL보다 디테일하게 설정 가능
                - Object Access Control List (ACL) - 오브젝트(파일) 별로 접근 권한을 허횽
                - Bucket Access Control List - Bucket Policies와 동일하게 버켓과 해당하는 버켓의 Object에 접근 권한을 설정
            - finer grain(미세한 입자) Object 별로 접근 권한을 나눔
            
              
            
        - S3 Bucket Policies
            
            ![[image 6 4.png]]
            
            - Principal은 해당 정책을 적용할 계정이나 유저
        - Example: Public Access - Use Bucket Policy
            
            ![[image 7 3.png]]
            
              
            
        - Example: User Access to S3 - IAM permissions
            
            ![[image 8 3.png]]
            
              
            
        - Example: EC2 instance Access - Use IAM Roles
            
            ![[image 9 3.png]]
            
              
            
              
            
        - Advanced: Cross-Account Access - Use Bucket Policy
            
            ![[image 10 3.png]]
            
              
            
        - Bucket settings for Block Public Access
            
            ![[image 11 3.png]]
            
              
            
    - S3 Security: Bucket Policy Advanced
        - S3 Bucket Policies
            
            ![[image 12 3.png]]
            
            - Source VPC: 특정 VPC에서만 S3 버킷에 접근이 가능하게
            - CloudFront Origin Identity: CloudFront가 해당 버킷에 접근할 수 있도록
            
              
            
            > [!important]  
            > CloudFront란? CDN으로 자주 요청되는 데이터를 캐싱해서 제공한다.  
            
        - Bucket Policies - Advanced Examples
            
            ![[image 13 3.png]]
            
              
            
            ![[image 14 3.png]]
            
              
            
            ![[image 15 3.png]]
            
              
            
    - S3 Website Overview
        
        ![[image 16 3.png]]
        
          
        
    - S3 Versioning
        
        ![[image 17 3.png]]
        
          
        
          
        
    - S3 Replication
        
        ![[image 18 3.png]]
        
          
        
          
        
    - S3 Replication Notes
        
        ![[image 19 3.png]]
        
          
        
          
        
    - S3 Storage Classes Overview
        - S3
            
            ![[image 20 3.png]]
            
            - AWS S3 Storage Classes는 변경이 가능하다.
        - S3 Durability and Avaiability
            
            ![[image 21 3.png]]
            
              
            
        - S3 Standard - General Purpose
            
            ![[image 22 3.png]]
            
            **S3 Standard - General Purpose**
            
            - 99.99% 가용성
            - 자주 접근 되는 데이터
            - 낮은 지연성과 높은 대역폭
            
        - S3 Storage Classes - Infrequent Access
            
            ![[image 23 3.png]]
            
            S3 Storage Classes - Infrequent Access (IA)
            
            - GP보다 덜 접근되는 데이터들. 그러나, 필요할 땐 빠른 접근이 필요할 때
            - S3 Standard보다 저렴함
            
              
            
            - Amazon S3 Standard-Infrequent Access (S3 Standard-IA)
                - 99.9% Availability
                - 사용 예: 재난 복구, 백업
            - Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)
                - 단일 AZ에서 높은 지속성(99.99999999%)을 가진다. AZ가 파괴되면 데이터 유실
                - 99.5% Availability
                - 사용 예: 두번 째 백업 카피
        - Amazon S3 Glacier Storage Classes
            
            ![[image 24 3.png]]
            
            **Amazon S3 Glacier Storage**
            
            - 저비용 아카이빙/백업용 오브젝트 저장소
            - retrieving을 통해서 데이터를 복구 후에 사용 가능
            - 비용: 저장소 사용 공간 가격 + 오브젝트 조회 비용
            
            **Amazon S3 Glacier Instant Retrieval**
            
            - 복구에 milisecond, 분기 별로 접근되는 데이터에 사용하면 좋다.
            - Inteligent Tiering에선 90일 이상 접근하지 않으면 이 Class로 옮긴다.
            
            **Amazon S3 Glacier Flexible Retrieval** (이전엔 S3 Glacier라고 불렀다)
            
            - Expedited (1~5분), Standard (3~5시간), Bulk (5 to 12 hours) - Free
            - Inteligent Tiering에선 90일 이상 접근하지 않으면 이 Class로 옮긴다.
            
            Amazon S3 Glacier Deep Archive - 장기간 보관 시에
            
            - Standard (12시간), Bulk (48시간)
            - Inteligent Tiering에선 180일 이상 접근하지 않으면 이 Class로 옮긴다.
        - S3 Intelligent-Tiering
            
            ![[image 25 3.png]]
            
            **S3 Intelligent-Tiering**
            
        - S3 Storage Classes Comparison
            
            ![[image 26 3.png]]
            
              
            
            ![[image 27 3.png]]
            
              
            

### 핵심 요약

- 핵심 요약 접기
    - S3는 무한대로 확장 가능한 AWS의 객체 스토리지 서비스입니다.
    - 버킷은 S3의 기본 컨테이너로, 글로벌 고유 이름을 가져야 합니다.
    - S3는 버킷 정책, IAM 정책, ACL 등 다양한 보안 옵션을 제공합니다.
    - S3 버저닝을 통해 객체의 여러 버전을 유지 관리할 수 있습니다.
    - S3 복제를 사용하여 버킷 간에 객체를 자동으로 복사할 수 있습니다.
    - S3는 Standard, Infrequent Access, Glacier 등 다양한 스토리지 클래스를 제공합니다.
    - S3 Intelligent-Tiering은 액세스 패턴에 따라 객체를 자동으로 이동시켜 비용을 최적화합니다.
    - S3는 또한 데이터 수명 주기 관리 기능을 제공하여 객체를 자동으로 다른 스토리지 클래스로 이동하거나 삭제할 수 있습니다.
    - 이를 통해 장기 보관 데이터의 스토리지 비용을 최적화할 수 있습니다. 또한, S3는 강력한 데이터 암호화 옵션을 제공하여 저장 및 전송 중인 데이터의 보안을 보장합니다.
    - S3는 또한 다양한 데이터 분석 도구와 통합되어 있어, 저장된 데이터에 대한 인사이트를 얻는 데 도움을 줍니다.
    - 예를 들어, Amazon Athena를 사용하면 S3에 저장된 데이터에 대해 SQL 쿼리를 실행할 수 있습니다.
    - S3 Select 기능을 사용하면 전체 객체를 다운로드하지 않고도 필요한 데이터만 효율적으로 검색할 수 있습니다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 