---
⭕첫 학습날: 2024-10-14
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 1일 복습
🛑첫날: "✏첫날 : 2024/10/14"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤13일째❤
🛑4일후: "🥉4일뒤 : 2024/10/18"
🛑7일후: "🥈7일뒤 : 2024/10/21"
🛑14일후: "🥇14일뒤 : 2024/10/28"
4일후: "@2024년 10월 18일"
4일후(text): 2024/10/18
7일후: "@2024년 10월 21일"
7일후(text): 2024/10/21
14일후: "@2024년 10월 28일"
14일후(text): 2024/10/28
오늘1: "@2024년 10월 27일 오후 2:00"
오늘2: 2024/10/27
첫학습날text: 2024/10/14
오늘과 첫학습날 사이: "13"
사이: "13"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[IaC]] [[DevOps]]

### 단서 질문

- 테라폼이란?
    
    IaC 도구로 코드를 통해 리소스를 관리 가능하게 만든다.
    

### 핵심 필기

- 전체 내용 접기
    - Terraform이란?
        
        멀티/하이브리드 클라우드 리소스를 프로비저닝하기 위해 사용되는 IaC 도구
        
    - 기능
        
        **오케스트레이션**
        
        - 클라우드 리소스 생성할 때 오케스트레이션을 한다.
        
        **Cloud agnostic**
        
        - AWS, Azure, GCP, NCP 등 다양한 클라우드 서비스를 지원한다.
        
        **선언형 문법**
        
        - 리소스를 단순히 선언만 하면 된다. (순서 생각x)
        
        **Modules**
        
        - 모듈화를 통해 Terraform 코드 재사용이 가능하다.
        
        **StateManagement**
        
        - 인프라를 만드는동안 상태가 지속된다.
        - 상태를 다른 팀 멤버와 공유하여 협동이 가능하다.
        
        **Provisioning**
        
        - local-exec와 remote-exec 블록에서 스크립트를 실행 가능하다.
        - Ansible, Chef와 같은 환경 관리 도구와 같이 쓰면 유용하다.
        
        **오픈소스**
        
    - Terraform Workflow [init - plan - apply -destroy]
        
        테라폼은 코드를 실행하기 위해서 특정 절차를 거친다. 이 절차들은 클라우드 리소스의 라이프사이클과 관련이 깊다.
        
        이 절차는 클라우드 종류와 관계 없이 동일하다. 이 말은 즉, 동일한 steps/commands가 cloud provider의 리소스를 CRUD하는데 동일하게 동작한다.
        
    - init 커맨드
        
        terraform은 모든 클라우드 제공자를 설치하지 않으며, provider를 통해 명시한 제공자의 기능만 설치한다.
        
        `terraform init` 은 명시한 provider를 통해 적절한 플러그인을 다운로드합니다.
        
    - plan 커맨드
        
        `terraform plan` 은 실행 계획 만드는 것을 도와줍니다. 이 단계에서 Terraform은 실행 가능성을 체크합니다. 문법 에러부터 API Authentication, 상태 확인 등을 합니다.
        
        `plan` 은 Terraform 스크립트에서 문제가 발생하는 부분을 하이라이팅합니다. 만약, 체크가 성공적으로 끝나면 인프라 변경 사항을 요약해서 출력합니다.
        
        `plan` 은 apply를 사용하기 전에 먼저 실행해야 합니다.
        
        - 실행 코드
            
            ```JavaScript
            $ terraform plan
            
            Terraform used the selected providers to generate the following execution plan. Resource actions are
            indicated with the following symbols:
              + create
            
            Terraform will perform the following actions:
            
              # aws_instance.myec2 will be created
              + resource "aws_instance" "myec2" {
                  + ami                                  = "ami-12345"
                  + arn                                  = (known after apply)
                  + associate_public_ip_address          = (known after apply)
                  + availability_zone                    = (known after apply)
                  + cpu_core_count                       = (known after apply)
                  + cpu_threads_per_core                 = (known after apply)
                  + disable_api_stop                     = (known after apply)
                  + disable_api_termination              = (known after apply)
                  + ebs_optimized                        = (known after apply)
                  + get_password_data                    = false
                  + host_id                              = (known after apply)
                  + host_resource_group_arn              = (known after apply)
                  + iam_instance_profile                 = (known after apply)
                  + id                                   = (known after apply)
                  + instance_initiated_shutdown_behavior = (known after apply)
                  + instance_lifecycle                   = (known after apply)
                  + instance_state                       = (known after apply)
                  + instance_type                        = "t2.micro"
                  + ipv6_address_count                   = (known after apply)
                  + ipv6_addresses                       = (known after apply)
                  + key_name                             = (known after apply)
                  + monitoring                           = (known after apply)
                  + outpost_arn                          = (known after apply)
                  + password_data                        = (known after apply)
                  + placement_group                      = (known after apply)
                  + placement_partition_number           = (known after apply)
                  + primary_network_interface_id         = (known after apply)
                  + private_dns                          = (known after apply)
                  + private_ip                           = (known after apply)
                  + public_dns                           = (known after apply)
                  + public_ip                            = (known after apply)
                  + secondary_private_ips                = (known after apply)
                  + security_groups                      = (known after apply)
                  + source_dest_check                    = true
                  + spot_instance_request_id             = (known after apply)
                  + subnet_id                            = (known after apply)
                  + tags_all                             = (known after apply)
                  + tenancy                              = (known after apply)
                  + user_data                            = (known after apply)
                  + user_data_base64                     = (known after apply)
                  + user_data_replace_on_change          = false
                  + vpc_security_group_ids               = (known after apply)
            
                  + capacity_reservation_specification (known after apply)
            
                  + cpu_options (known after apply)
            
                  + ebs_block_device (known after apply)
            
                  + enclave_options (known after apply)
            
                  + ephemeral_block_device (known after apply)
            
                  + instance_market_options (known after apply)
            
                  + maintenance_options (known after apply)
            
                  + metadata_options (known after apply)
            
                  + network_interface (known after apply)
            
                  + private_dns_name_options (known after apply)
            
                  + root_block_device (known after apply)
                }
            
            Plan: 1 to add, 0 to change, 0 to destroy.
            
            ────────────────────────────────────────────────────────────────────────────────────────────────────────
            
            Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly
            these actions if you run "terraform apply" now.
            ```
            
    

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 