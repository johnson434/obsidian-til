---
⭕첫 학습날: 2024-10-08
⭕과목: AWS
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 4일 복습
🛑첫날: "✏첫날 : 2024/10/08"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤19일째❤
🛑4일후: "🥉4일뒤 : 2024/10/12"
🛑7일후: "🥈7일뒤 : 2024/10/15"
🛑14일후: "🥇14일뒤 : 2024/10/22"
4일후: "@2024년 10월 12일"
4일후(text): 2024/10/12
7일후: "@2024년 10월 15일"
7일후(text): 2024/10/15
14일후: "@2024년 10월 22일"
14일후(text): 2024/10/22
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/10/08
오늘과 첫학습날 사이: "19"
사이: "19"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[AWS]]

### 단서 질문

- 질문1

### 핵심 필기

- 전체 내용 접기
    - AWS User 만들고 Access Key 발급
        1. AWS Console에서 IAM 메뉴 접근
        2. User 생성 및 정책 부여. 정책은 Administrator Access
    - AWS CLI에서 configure로 Access Key 설정
        
        ```Bash
        # 터미널
        aws configure
        ```
        
          
        
    - AWS CLI에서 user 조회하여 권한 확인
        
        ```Bash
        aws iam get-user
        ```
        
    - VPC 생성하기
        
        ```Bash
        # 태그를 주는 이유는 VPC ID가 아닌 Name 태그를 통해서 쉽게 사용하기 위해서
        aws ec2 create-vpc --cidr-block 10.0.0.0/16 \
        	--tag-specifications "ResourceType=vpc,Tags=[{Key=name,Value=MyVPC}]" \
        	--output yaml
        ```
        
          
        
    - VPC 조회하기
        
        ```Bash
        aws ec2 describe-vpcs --query "Vpcs[0]"
        CidrBlock: 10.0.0.0/16
        CidrBlockAssociationSet:
        - AssociationId: vpc-cidr-assoc-036427cd85c75e789
          CidrBlock: 10.0.0.0/16
          CidrBlockState:
            State: associated
        DhcpOptionsId: dopt-02637573251b13a3b
        InstanceTenancy: default
        IsDefault: false
        OwnerId: '961341529973'
        State: available
        Tags:
        - Key: name
          Value: MyVPC
        VpcId: vpc-0fb6045d8f9393bdf
        
        aws ec2 describe-vpcs --query "Vpcs[0]".VpcId
        "vpc-0fb6045d8f9393bdf"
        ```
        
          
        
    - 인터넷 게이트웨이 생성하기
        
        ```Bash
        $ aws ec2 create-internet-gateway --tag-specifications "ResourceType=internet-gateway, Tags=[{Key=Name,Value=MyIGW}]"
        InternetGateway:
          Attachments: []
          InternetGatewayId: igw-017b8704b7405427f
          OwnerId: '961341529973'
          Tags:
          - Key: Name
            Value: MyIGW
        ```
        
          
        
    - 인터넷 게이트웨이에 VPC 붙이기
        
        ```Bash
        aws ec2 attach-internet-gateway --vpc-id $VPC_ID --internet-gateway-id $IGW_ID
        ```
        
          
        
          
        
    - 인터넷 게이트웨이 조회하기
        
        ```Bash
        aws ec2 describe-internet-gateways --internet-gateway-id $IGW_ID
        ```
        
          
        
    - 라우트 테이블은
        
        라우팅 테이블 정보만 담는 그릇이다.
        
        ```Bash
        
        # 라우트 테이블을 만들고
        aws ec2 create-route-table --vpc-id $VPC_ID --tag-specification "ResourceType=route-table,Tags=[{Key=Name,Value=PublicRouteTable}]"
        
        # 라우팅을 만든다.
        aws ec2 create-route --route-table-id $PUBLIC_RT_ID --destination-cidr-block 0.0.0.0/0 --gateway-id $IGW_ID
        
        # 라우트 테이블 조회
        $ aws ec2 describe-route-tables
        RouteTables:
        - Associations: []
          OwnerId: '961341529973'
          PropagatingVgws: []
          RouteTableId: rtb-068710a12ae426407
          Routes:
          - DestinationCidrBlock: 10.0.0.0/16
            GatewayId: local
            Origin: CreateRouteTable
            State: active
          - DestinationCidrBlock: 0.0.0.0/0
            GatewayId: igw-017b8704b7405427f
            Origin: CreateRoute
            State: active
          Tags:
          - Key: Name
            Value: PublicRouteTable
          VpcId: vpc-0fb6045d8f9393bdf
        - Associations:
          - AssociationState:
              State: associated
            Main: true
            RouteTableAssociationId: rtbassoc-02afb3826ce45eb89
            RouteTableId: rtb-05a5b311ee7921c59
          OwnerId: '961341529973'
          PropagatingVgws: []
          RouteTableId: rtb-05a5b311ee7921c59
          Routes:
          - DestinationCidrBlock: 10.0.0.0/16
            GatewayId: local
            Origin: CreateRouteTable
            State: active
          Tags: []
          VpcId: vpc-0fb6045d8f9393bdf
        
        # 퍼블릭 서브넷과 퍼블릭 route table을 연결한다.
        $ aws ec2 associate-route-table --subnet-id $PublicSubnetA_ID \
        	--route-table-id $PUBLIC_RT_ID
        
        # 서브넷의 퍼블릿 IP를 줘야 한다.(인터넷으로 통신하기 위해서)
        aws ec2 modify-subnet-attribute --subnet-id $PublicSubnetA_ID  \
        	--map-public-ip-on-launch
        	
        # VPC DNS 호스트 이름을 활성화
        $ aws ec2 modify-vpc-attribute --vpc-id $VPC_ID --enable-dns-hostnames
        
        # 프라이빗 서브넷 생성
        ```
        
          
        
    - 프라이빗 서브넷 흐름
        
        VPC 생성 → Subnet 생성 → 라우트 테이블 생성 → 프라이빗 라우트 생성→ 서브넷과 라우트 테이블 연결(Attach)
        
    - 퍼블릭 서브넷 흐름
        
        VPC 생성 → 인터넷 게이트웨이 생성 → VPC와 인터넷 게이트웨이 연결 → Subnet 생성 → 라우트 테이블 생성 → 퍼블릭 라우트 생성(인터넷 게이트웨이와 연결) → 서브넷과 라우트 테이블 연결
        
    - kOps
        
        ```Bash
        $ kubectl config get-contexts
        CURRENT   NAME                          CLUSTER               AUTHINFO              NAMESPACE
                  kubernetes-admin@kubernetes   kubernetes            kubernetes-admin      
        *         mycluster.k8s.local           mycluster.k8s.local   mycluster.k8s.local   
        
        $ kubectl config use-context kubernetes-admin@kubernetes
        
        $ kops delete cluster $NAME --yes
        # 실행하면 모든 관련 리소스가 삭제되지만 S3 버킷은 남아있다(백업용도이므로)
        ```
        
          
        

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 