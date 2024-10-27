---
기술:
  - DevOps
  - 아키텍처
---
[[MSA]] [[Cloud Native]]
# Microservices Architecture

서비스 지항적 아키텍처 스타일로 서비스 간에 커플링을 느슨하게 하는 아키텍처

MicroService에선 가벼운 프로토콜을 사용한다.(ex : TCP, GRPC)

마이크로 서비스에 반대되는 개념이 **Monolithic Architecture**다.

## Monolithic Architecture

> [!important]  
> Monolithic Architecture는 전통적인 웹개발 방식으로 배포도 하나로, 개발도 하나로 통합된 방식이다.  

Monolithic Architecture는 흔히 3-tier apps 구조를 가진다.

Monolithic Architecture와 반대로 MSA 구조 서비스에선 아래와 같이 서비스 단위로 서버를 나눈다.

따라서, 비즈니스 로직을 위한 서버가 더 필요하다면 전체 서버가 아닌 비즈니스 로직을 처리하는 서버만 추가(Scale Up)하면 된다.



# Monolith to MicroServices

1. 애플리케이션을 작은 단위로 나누기
2. Strangler 패턴 사용하기
    
    1. https://martinfowler.com/bliki/StranglerFigApplication.html
    
    

# MicroServices 장점

1. Improved fault Isolation : Fault가 발생했을 때, 독립적이라 다른 서비스에 영향x
2. Eliminate vendor or technology lock-in : 기술 전환이 간단
3. Ease of understanding : 사용이 쉬움.
4. Smaller and faster deployments : 작아서 배포가 빠름
5. Scalability : 확장성. 필요한 서비스만 보충하면 됨.

# Microservices 단점

1. 복잡하다. : 여러 개의 서비스를 운영할 필요가 있으므로 전체를 운영하는데 까다롭다.
2. 보안 문제 : 각각의 서비스의 보안 문제를 신경 써야 한다.
3. 복잡한 이슈를 해결하는데 복잡도가 증가함.
    1. 팀원이 모두 MSA에 대한 이해가 있어야 한다.
4. 테스트가 쉬워보이지만 전체 테스트가 돌아갔는지 확신을 가져야함.
5. 배포도 용이해보이지만 여러 개의 팀이 배포하므로 팀이 이해도가 없으면 복잡도가 올라감.
    1. 이로 인해 하나의 MS에 배포하는데 다른 MS에 영향을 끼칠 수도 있음.
6. Multiple Databases : 여러 개에 데이터베이스를 다룰 준비가 됐나?
7. 지연성 이슈 : Non-microservice에선 하나에 서버에서 모든 일을 처리하기 때문에 서버 간 호출이 불필요하다. 반면에 MicroService에선 로직 처리를 위해 매 번 다를 서버에 요청을 해야하므로 지연성이 증가한다.
8. Transient errors(일시적인 에러) : 매 번 API 요청을 Server to Server로 해야하므로 실패 시에 retry 횟수 등을 정해놔야함.
9. Multiple point of failures : 몇몇 서비스가 다운되어도 동작할 수 있도록 해야함.
10. Security : 서버 간 통신 간에 보안 문제