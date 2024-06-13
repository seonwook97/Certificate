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