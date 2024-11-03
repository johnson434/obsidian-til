---
❤1일복습여부: false
🧡4일복습여부: false
💛7일복습여부: false
💚14일복습여부: false
🧠장기기억: false
🛑첫날: "✏첫날 :"
---
[[EKS]]
https://www.youtube.com/watch?v=d16UXBthfYQ&ab_channel=AmazonWebServicesKorea
# 단서 질문
- EKS란?
	- AWS에서 제공하는 Managed Kubernetes Service
# 핵심 필기
# Amazon EKS의 특징
**Upstream K8s**
- k8s 소스 코드를 변형 없이 그대로 사용한다. 
**높은 가용성**
- AWS측에서 쿠버네티스 서비스를 위한 환경을 관리해준다.
**통합성**
- AWS의 다양한 서비스들과 통합 (VPC, ELB, IAM 권한, CloudWatch 등)

**EKS의 장점**
- **IAM을 통한 역할 관리**
	- EKS에선 IAM을 통해서 역할을 관리하므로 직접 k8s 클러스터를 구축하는 것보다 권한 관리가 편리하다.
- **네트워크**
	- Amazon VPC CNI를 사용해서 파드가 VPC 주소를 가진다.  
		- Pod는 VPC 주소를 통해 통신하므로 오버헤드가 발생하지 않는다. 
		- **예**
			- 노드 내의 pod 간에 통신은 가상 이더넷(veth)을 통한 bridge 네트워크를 통해서 이뤄진다. 이 때 헤더엔 도착 Pod의 주소만 패킷에 포함된다.
			- 반연에, 서로 다른 노드의 pod 간에 통신은 노드 주소와 파드 주소가 헤더의 포함되어 통신하다. -> 헤더의 크기가 커짐 -> 통신이 느려진다.
		- 반면에, AWS VPC CNI를 사용하면 Pod에 VPC의 IP를 부여합니다. 
		- Pod는 VPC의 IP 주소로 통신하므로 헤더엔 Pod의 IP만 포함됩니다. 
			-> 내가 생각하는 고려해야 할 사항: Pod의 개수만큼 IP 주소를 사용할텐데 CIDR을 잘 생각하고 설정할 것
	- Amazon VPC CNI의 단점
		- Pod에 IP를 할당하기 위해선 해당 인스턴스의 ENI에 IP를 먼저 할당해야 합니다.
		- 그런데, 인스턴스마다 사용할 수 있는 ENI 개수 제한이 있고 ENI는 사용 가능한 IP의 개수 제한은 10개입니다.
		- m5 인스턴스 기준 ENI를 3개까지 사용 가능하므로 사용 가능한 총 IP 개수는 29개입니다.
		- 따라서, 총 29개의 파드만이 오버헤드 없이 통신을 할 수 있습니다.
		- 이를 해결하기 위해 접두사 위임(Prefix Delegation)을 사용합니다. (지금 필요한 지식 같지 않아서 스킵)
	- VPC Securty Group을 통해서 네트워크 격리 가능
		- Security Group은 ENI 단위로 설정된다.
		- ENI를 공유하는 Pod가 동일한 Security Group을 사용하게 된다.
# 핵심 요약
- EKS를 사용하면 Pod간 통신이 간편해진다. 
- Pod마다 IP를 설정하면 통신 오버헤드가 줄어들어서 통신 속도도 빨라진다.
- 권한 설정도 IAM을 통해 간편하게 설정할 수 있다.
- **클러스터 내에서 직접 설정해야 할 요소들이 AWS 서비스를 통해서 간단하게 설정 가능해진다.** 