---
⭕첫 학습날: 2024-10-20
⭕과목: Ansible
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
복습: 1일 복습
🛑첫날: "✏첫날 : 2024/10/20"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤7일째❤
🛑4일후: "🥉4일뒤 : 2024/10/24"
🛑7일후: "🥈7일뒤 : 2024/10/27"
🛑14일후: "🥇14일뒤 : 2024/11/03"
4일후: "@2024년 10월 24일"
4일후(text): 2024/10/24
7일후: "@2024년 10월 27일"
7일후(text): 2024/10/27
14일후: "@2024년 11월 3일"
14일후(text): 2024/11/03
오늘1: "@2024년 10월 27일 오후 2:01"
오늘2: 2024/10/27
첫학습날text: 2024/10/20
오늘과 첫학습날 사이: "7"
사이: "7"
"1일차복습여부1,0": "0"
"4일차복습여부1,0": "0"
"7일차복습여부1,0": "0"
"장기기억저장여부1,0": "0"
학습률: "0"
진행바: ⬜ 0%
---
[[03 - Tags/DevOps]] [[IaC]] [[Ansible Notion]] [[Ansible]]
> [!info] Ansible Documentation — Ansible Community Documentation  
> Welcome to Ansible community documentation!  
> [https://docs.ansible.com/ansible/latest/](https://docs.ansible.com/ansible/latest/)  

### 단서 질문

- 질문1

### 핵심 필기

- 전체 내용 접기
    - **Ansible 구성 요소 3가지**
        
        # Control Node
        
        - Ansible이 설치되어 있는 노드로 Control Node에서 Ansible을 실행하여 Managed Node를 프로비저닝한다. ssh를 통해서 Managed Node와 연결된다.
        
        # Inventory
        
        - Managed Node 리스트로 Control Node에 의해 관리되는 노드의 집합이다.
        
        - 코드 예시
            
            ```YAML
            myhosts:
              hosts:
                my_host_01:
                  ansible_host: 192.0.2.50
                my_host_02:
                  ansible_host: 192.0.2.51
                my_host_03:
                  ansible_host: 192.0.2.52
            ```
            
        
        # Managed Node
        
        - Ansible이 컨트롤할 원격 시스템이나 호스트를 의미한다.
        - ssh 접속만 허용하면 되며, 추가적으로 패키지를 설치할 필요가 없다.
        - 컨트롤 노드의 공개키를 매니저드 노드에 authorized_keys에 작성해야 한다.
            - 진행 과정 설명
                
                ```JavaScript
                controller-node@localhost: ~$ ssh-keygen # 키 생성
                # id_rsa와 id_rsa.pub가 생성
                # 연결할 노드(매니저드 노드)에 authrozied_keys에 id_rsa.pub 내용이 추가되어야 한다.
                
                controller-node@localhost: ~$ ssh -i ./id_rsa 유저명@호스트
                ```
                
    - Ansible의 특징
        
        **Agent-less 아키텍처**
        
        추가적인 소프트웨어를 설치를 피함으로써 유지를 위한 오버헤드를 줄일 수 있다.
        
        **간단함**
        
        YAML 문법으로 작성되어 읽기 편하며, 기존 OS 인증 방식을 사용하여 ssh로 접근한다.
        
    - ansible vs ansible-playbook
        
        ansible은 하나의 task를 진행하지만 ansible-playbook은 여러 개의 playbooks를 실행한다.
        
    - Inventory 작성 팁
        
        - 그룹명은 유일해야 하며 대소문자를 구분한다.
        - 공백과 하이픈을 사용하지 않고 숫자로 시작하면 안된다.
        - **What** Group hosts according to the topology, for example: db, web, leaf, spine.
        - **Where** Group hosts by geographic location, for example: datacenter, region, floor, building.
        - **When**Group hosts by stage, for example: development, test, staging, production.
        
        ```YAML
        leafs:
          hosts:
            leaf01:
              ansible_host: 192.0.2.100
            leaf02:
              ansible_host: 192.0.2.110
        
        spines:
          hosts:
            spine01:
              ansible_host: 192.0.2.120
            spine02:
              ansible_host: 192.0.2.130
        
        network:
          children:
            leafs:
            spines:
        
        webservers:
          hosts:
            webserver01:
              ansible_host: 192.0.2.140
            webserver02:
              ansible_host: 192.0.2.150
        
        datacenter:
          children:
            network:
            webservers:
        ```
        
    - Inventory 변수 사용
        
        ```YAML
        webservers:
          hosts:
            webserver01:
              ansible_host: 192.0.2.140
              http_port: 80
            webserver02:
              ansible_host: 192.0.2.150
              http_port: 443
        ---
        webservers:
          hosts:
            webserver01:
              ansible_host: 192.0.2.140
              http_port: 80
            webserver02:
              ansible_host: 192.0.2.150
              http_port: 443
          vars:
            ansible_user: my_server_user
        ```
        
    - playbook이란?
        
          
        

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.
