## 2. Core Concepts

### Cluster Architecture
- Kubernetes의 목적은 애플리케이션을 자동화된 방식으로 컨테이너 형태로 제공하여 쉽게 배포하고, 필요한 만큼 인스턴스를 늘리거나 줄이며, 애플리케이션 내의 다양한 서비스 간에 쉽게 통신할 수 있도록 함
- Kubernetes 아키텍처를 높은 수준에서 살펴보면, 두 종류의 선박으로 비유할 수 있음
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/15ad0923-0c32-4746-97b7-15de8bf7b9f7)
  - **작업을 수행하는 화물선**: 컨테이너를 운반하는 역할을 하며, 실제 애플리케이션이 실행되는 노드
  - **선박을 통제하고 모니터링하는 선박**: 클러스터의 관리를 담당하는 마스터 노드

### 클러스터 구성 요소
![image](https://github.com/seonwook97/Certificate/assets/92377162/44eed8ae-a2b1-45f5-868d-44292c2e9357)

#### 노드 (Nodes)
- Kubernetes 클러스터는 물리적 또는 가상 노드의 집합으로 구성됨. 노드는 컨테이너 형태로 애플리케이션을 호스팅함
  - **작업자 노드 (Worker Nodes)**: 애플리케이션이 실행되는 노드
  - **마스터 노드 (Master Nodes)**: 클러스터 관리 및 제어를 담당

#### etcd
- 고가용성 키-값 저장소로, 클러스터의 모든 데이터를 저장함

#### 스케줄러 (Scheduler)
- 컨테이너를 배치할 적절한 노드를 식별함. 컨테이너의 리소스 요구 사항과 노드의 용량 등을 고려하여 배치함

#### 컨트롤러 (Controllers)
- 클러스터의 상태를 관리함
  - **노드 컨트롤러 (Node Controller)**: 노드의 상태를 관리함
  - **복제 컨트롤러 (Replication Controller)**: 올바른 수의 컨테이너가 실행 중인지 확인함

#### Kube API 서버 (Kube API Server)
- 클러스터 내의 모든 작업을 조정함. Kubernetes API를 노출하여 외부 사용자가 클러스터를 관리할 수 있게 함

#### 컨테이너 런타임 (Container Runtime)
- 컨테이너를 실행할 수 있는 소프트웨어임. Docker, containerD 등이 이에 해당함

#### kubelet
- 각 노드에서 실행되는 에이전트로, Kube API 서버의 지시에 따라 컨테이너를 배포하거나 파괴함

#### Kube 프록시 (Kube Proxy)
- 작업자 노드 간의 네트워킹을 관리하여 클러스터 내 서비스 간의 통신을 가능하게 함

---

### Docker vs ContainerD: 상세 비교

![image](https://github.com/seonwook97/Certificate/assets/92377162/560ac0d3-3939-4302-97a3-b4074b4f2fa3)

#### Docker의 시작

- 컨테이너 기술의 초창기에는 Docker가 가장 지배적인 도구였음
- Docker는 사용자가 컨테이너 작업을 매우 간단하게 할 수 있게 해줬고, 이로 인해 널리 사용되었음
- Kubernetes는 처음에 Docker를 조율하기 위해 만들어졌음

#### Kubernetes와 CRI

- Kubernetes가 인기를 얻으면서 rkt와 같은 다른 컨테이너 런타임도 필요하게 됨
- 이를 해결하기 위해 Kubernetes는 컨테이너 런타임 인터페이스(CRI)를 도입하여 다양한 런타임이 Kubernetes와 호환될 수 있도록 함
- CRI는 OCI(Open Container Initiative) 표준을 준수하는 모든 런타임을 지원함.

#### OCI 표준

- OCI는 이미지 사양과 런타임 사양을 정의함
  - **Imagespec**: 컨테이너 이미지를 어떻게 구축해야 하는지 
  - **Runtimespec**: 컨테이너 런타임을 어떻게 개발해야 하는지 

#### Docker와 dockershim

- Docker는 CRI 표준을 지원하지 않았기 때문에 Kubernetes는 Docker를 지원하기 위해 dockershim을 도입했음
- 이는 일시적인 해결책으로, Docker를 계속 사용하기 위해 복잡함과 추가 노력이 필요했음
- Kubernetes 1.24 버전부터 dockershim이 완전히 제거되어 Docker에 대한 지원이 종료됨

#### Containerd의 등장

- ContainerD는 Docker의 일부였으나, 현재는 독립된 프로젝트로 CRI와 호환됨
- ContainerD는 Docker와 별개로 설치 및 사용할 수 있음
- 이는 Docker가 아닌 다른 런타임을 사용할 수 있게 함

#### CLI 도구들

**ctr**
- ContainerD와 함께 제공되는 기본 CLI 도구로, 주로 디버깅 목적으로 사용됨
- 기능이 제한적이며, 프로덕션 환경에서는 사용하기 어려움

**nerdctl**
- Docker CLI와 유사한 도구로, ContainerD와 함께 사용하기에 적합함
- 대부분의 Docker 명령을 지원하며, 최신 ContainerD 기능에도 접근할 수 있음

**crictl**
- Kubernetes 커뮤니티에서 제공하는 도구로, 모든 CRI 호환 런타임과 상호작용할 수 있음
- 주로 디버깅 목적으로 사용됨
