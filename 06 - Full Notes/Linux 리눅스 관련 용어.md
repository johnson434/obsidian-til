---
기술:
  - Linux
  - OS
---
[[Linux]]
- **데몬(Daemon)**
    
    리눅스에서 백그라운드로 실행되는 프로세스를 일컫는 말
    
- **namespace**
    
    리눅스의 기능으로 시스템의 자원을 공유하는 **그룹**을 말한다.
    
    시스템 리소스를 독립적으로 운영하기 위해 사용된다.
    
    namespace를 통해 독립된 프로세스 트리를 만들면 독립된 프로세스 트리끼리는 서로에 대해 알 수 없다. 컨테이너가 컨테이너끼리 독립된 이유가 바로 namespace를 이용해서 독립된 프로세스 트리를 만들어줬기 때문.
    
    namespaces : Docker를 사용하면서 Process나 Network 등이 어떻게 각 컨테이너마다 따로 관리되는지 궁금하지 않으셨나요? VM에서는 각 게스트 머신별로 독립적인 공간을 제공하고 서로가 충돌하지 않도록 하는 기능을 갖고 있습니다. Docker에서는namespaces를 통해 이러한 독립된 공간을 제공합니다.namespaces은 nested process tree를 만들 수 있게 해주며, 이 말은 각 프로세스가 시스템 리소스(process IDs, hostnames, user IDs, network access, interprocess communication, filesystem 등)와 함께 고유하게 분리된 프로세스 트리를 가질 수 있음을 의미합니다.분리된 process tree는 다른 process tree에서 확인inspect하거나 삭제kill 할 수 없습니다.PID namespace를 알아보며 이해를 더해보겠습니다.
    
    [https://gngsn.tistory.com/129](https://gngsn.tistory.com/129)
    
    ![[Untitled 9.png]]
    
    > [!info] 1. Namespace :: Developer's Delight  
    > Namespace 기술은 cgourp(Control Group)과 함께 컨테이너(Container) 솔루션을 구성하는 기술 중 하나입니다.  
    > [https://linuxias.github.io/container/namespace/1.what_is_namespace/](https://linuxias.github.io/container/namespace/1.what_is_namespace/)  
    
- **cgroup**
    자원의 할당량을 제한할 수 있다. cgroup에 할당된 프로세스들의 CPU, 메모리, IO 등 자원의 한계를 정할 수 있다. 이를 통해 컨테이너의 자원을 제한할 수 있는 것.
    
- **Union Mount Filesystems(overlayfs)**
    여러 개의 파일 시스템을 하나의 파일 시스템에 마운트 하는 기능이다. 도커의 컨테이너가 UFS를 기반으로 동작한다.(컨테이너 레이어와 이미지 레이어)