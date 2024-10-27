---
기술:
  - Docker
---
[[Docker]] [[Container]]
# Docker Compose

- YAML을 통해 실행
- 여러 개의 컨테이너를 정의하거나 실행할 수 있다.

# Use Cases

- Kuberneties와 같은 full orchestrator가 필요 없을 때
- 로컬에서 개발 및 테스트할 때
- 클라우드나 버츄얼 머신에서 Docker Compose 사용 가능

# Docker Compose command

**Build the app**

```Plain
docker compose build
```

**Run the app**

```Plain
docker compose up -d
```

**List the containers**

```Plain
docker compose ps
```

**Look at the db container logs**

```Plain
docker compose logs -f web-fe
```

**Compose V2 commands**

LS will list the current projects

```Plain
docker compose ls
```

**Let's try to deploy a second version**

```Plain
docker compose up -d
```

**Deploy a second version using a different project name**

Let's now use a project name to see if we can deploy a second version

```Plain
docker compose -p test up -d
```

  

# 환경 변수

```YAML
services:
	web:
		image: nginx:lts
		# 오버라이딩 가능
		environment:
			- DEBUG=1
			- FOO=BAR
```

# 네트워킹

컴포즈 내에서 이름으로 네트워킹한다.

network: 8080:80 # 호스트 OS의 8080 포트로 가는 트래픽은 컨테이너의 80번 포트로 전송된다는 뜻.

network: 80 # 컨테이너 내에서 80포트를 통해 전송한다는 뜻

- Volume
    
    ![[Untitled 16.png]]
    
- depends-on
    - 특정 컨테이너 시작 후에 컨테이너를 실행하도록 설정
- Restart Policy
    
    재시작 정책
    
    - no : default 정책으로 재시작 안함.
    - always : 늘 재시작함.
    - on-failure : 에러 발생 시 재시작
    - unless-stopped : stop하거나 remove를 제외하면 재시작