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

---

### ETCD
- ETCD는 분산되고 신뢰할 수 있는 키-값 저장소로, 간단하고 안전하며 빠른 성능을 자랑함
- Kubernetes의 중요한 구성 요소로서 클러스터의 상태와 설정 정보를 저장함

#### key-value store (키-값 저장소)
![image](https://github.com/seonwook97/Certificate/assets/92377162/7653301f-1eaa-4c0a-a496-3f1f51bbd583)
![image](https://github.com/seonwook97/Certificate/assets/92377162/0af2e48a-45b1-4537-98e7-1c5d34996abb)
- 전통적인 데이터베이스는 데이터를 표 형식으로 저장하는 반면, 키-값 저장소는 데이터를 문서나 페이지 형태로 저장함 
- 각 개인은 문서를 가지고 있으며, 해당 문서에 개인과 관련된 모든 정보가 저장됨
- 이 방식은 데이터 구조에 유연성을 제공하고, 필요에 따라 데이터를 쉽게 확장하거나 수정할 수 있게 함

#### 설치 및 실행
- 운영 체제에 맞는 바이너리를 GitHub 릴리스 페이지에서 다운로드
- 다운로드한 파일을 추출하고, `etcd` 실행 파일을 실행
  ```shell
  # 바이너리 다운로드
  curl -L https://github.com/etcd-io/etcd/releases/download/v3.3.11/etcdv3.3.11-linux-amd64.tar.gz -o etcd-v3.3.11-linux-amd64.tar.gz

  # 압축풀기
  tar xzvf etcd-v3.3.11-linux-amd64.tar.gz

  # etcd 실행
  ./etcd
  ```
- ETCD를 실행하면 기본적으로 포트 2379에서 수신 대기하는 서비스가 시작됨
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/c10cb9e6-8aa1-4a21-a4b4-41df2778a3c7)
- 이후 클라이언트를 통해 ETCD 서비스에 연결하고 데이터를 저장하고 검색할 수 있음

#### ETCDCTL 클라이언트
- ETCDCTL은 ETCD와 함께 제공되는 명령줄 클라이언트로, 키-값 쌍을 저장하고 검색하는 데 사용됨
- **데이터 저장**: `./etcdctl set key1 value1`
- **데이터 검색**: `./etcdctl get key1`
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/be5d63e6-13a8-4e26-9dc7-4f64fab87f94)

#### ETCD 버전 및 API
- **v0.1**: 2013년 8월 출시
- **v2.0**: 2015년 2월 출시, RAFT 합의 알고리즘 재설계
- **v3.0**: 2017년 1월 출시, 최적화 및 성능 개선
- **CNCF 인큐베이션**: 2018년 11월
- v2.0과 v3.0 사이에는 API 버전의 변화가 있었음. ETCDCTL 명령도 이에 맞춰 변경되었음

#### ETCDCTL 버전 확인 및 설정
- **버전 확인**: `ETCDCTL_API` 환경 변수를 통해 API 버전을 설정하거나, `etcdctl version` 명령을 통해 확인할 수 있음
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/b49736ab-863b-4fbb-91d7-0a880c610094)
- **API v3.0 사용**: `ETCDCTL_API=3` 환경 변수를 설정하여 v3.0 API와 함께 작동하도록 함
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/650ec0c5-5b52-48cc-a76a-ab3deac0c526)

#### v3.0 명령어
- **값 설정**: `./etcdctl put key value`
- **값 가져오기**: `./etcdctl get key`
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/00b68f07-7996-4d3d-bd65-88bf934d5305)

#### 고가용성 및 분산 시스템
- ETCD는 분산 시스템으로 설계되어 있으며, 고가용성을 위해 클러스터 모드에서 작동할 수 있음
- 이 과정에서 RAFT 프로토콜을 사용하여 노드 간의 일관성을 유지함

#### etcd의 역할
- Kubernetes에서 etcd는 클러스터에 관한 모든 정보를 저장하는 중앙 데이터 저장소 역할
  - Nodes
  - PODs
  - Configs
  - Secrets
  - Accounts
  - Roles
  - Bindings
  - Others

#### etcd 배포 방법
- 클러스터를 설정하는 방법에 따라 etcd는 다르게 배포될 수 있음
- **Manual**
  ```Shell
  wget -q --https-only \"https://github.com/coreos/etcd/releases/download/v3.3.9/etcd-v3.3.9-linux-amd64.tar.gz"
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/338830ad-7c11-453a-8189-6e64289ba737)
  - etcd 바이너리를 직접 다운로드
  - 바이너리 설치 및 etcd 구성
  - 마스터 노드에서 etcd를 서비스로 실행
  - `advertise-client-urls`
    - etcd가 수신하는 주소로, 서버의 IP와 포트 2379를 포함
    - kube API 서버가 etcd 서버에 접근하려면 이 URL을 구성해야 함
- **kubeadm**
  ```Shell
  kubectl get pods -n kube-system
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/c677d3e3-71cb-4017-bcdc-d39b36ccd1b3)
  - kubeadm을 사용하여 클러스터를 설정하는 경우, kubeadm은 etcd 서버를 포드로 배포
  - 이 포드는 `kube-system` 네임스페이스에 위치
  ```Shell
  kubectl exec etcd-master –n kube-system etcdctl get / --prefix –keys-only
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/63490486-7230-4b00-9166-71e2bec4c1be)
  - etcd 데이터베이스를 탐색하려면 이 포드 내에서 etcdctl 유틸리티를 사용할 수 있음
  - Kubernetes에 저장된 모든 키를 나열하려면 다음 명령을 실행

#### etcdctl 유틸리티에 대한 추가 정보
- etcdctl이 etcd API 서버에 인증할 수 있도록 인증서 파일의 경로 지정
- 인증서 파일은 다음 경로의 etcd - master에서 사용할 수 있음
  ```Shell
  kubectl exec etcd - master - n kube - system -- sh - c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert /etc kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt --key /etc/kubernetes/pki/etcd/server.key" 
  ```

---

### Kube-api Server
- Kubernetes의 기본 관리 구성 요소
- `kubectl` 명령을 실행하면 `kubectl` 유틸리티는 kube-apiserver에 요청을 보냄

#### Kube-api Server 요청 처리 과정
```Shell
kubectl get nodes
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/b47fe2bd-d9e8-4302-8b02-a805c74f6438)
- `kubectl` 명령을 통해 요청이 kube-apiserver에 도달
- kube-apiserver는 요청을 인증하고 검증
- etcd 클러스터에서 데이터를 검색하여 응답

```Shell
curl -X POST /api/v1/namesapces/default/pods ...[other]
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/3384cc33-0bc5-45c1-84d5-3330f9c07123)
- 포드를 생성하는 POST 요청을 보내면, 요청이 인증되고 유효성이 검사
- API 서버는 etcd 서버의 정보를 업데이트 함
- Scheduler는 새로운 포드가 생성되었음을 인식하고, 올바른 노드에 포드를 할당
- 이 정보는 kube-apiserver를 통해 etcd 클러스터에 업데이트
- kube-apiserver는 클러스터의 다양한 작업을 중앙에서 관리함
- Scheduler, kube-controller-manager, kubelet 모두 kube-apiserver를 통해 클러스터를 업데이트

#### Kube-api Server 배포
- kubeadmin 도구를 사용하여 클러스터를 부트스트랩한 경우, kube-apiserver는 자동으로 설정
- 수동 설정
  ```Shell
  - wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-apiserver
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/4f0bedca-298a-4836-a3dd-d44f1e081da1)
  - Kubernetes 릴리스 페이지에서 kube-apiserver 바이너리를 다운로드
  - 바이너리를 설치하고 서비스로 실행되도록 구성
  - kube-apiserver는 많은 매개변수를 사용하여 실행됨 
  - 주요 매개변수 중 하나는 etcd 서버의 위치를 지정하는 것

#### Kube-api Server 옵션 보기
- kubeadmin을 사용하여 설정한 경우
  ```Shell
  kubectl get pods -n kube-system
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/5ba839b8-6a51-4393-914d-2ae6dd419dcd)
  - `kube-system` 네임스페이스에 Pod로 배포됨
  - 포드 정의 파일은 `/etc/kubernetes/manifest` 폴더에 있음

- kubeadmin을 사용하지 않고 설정한 경우
  ```Shell
  cat /etc/kubernetes/manifests/kube-apiserver.yaml
  ```
  - 위치한 kube-apiserver 서비스를 확인하여 옵션을 검사할 수 있음
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/02347665-9d54-42ba-91a5-a7a781fdf945)
  ```Shell
  cat /etc/systemd/system/kube-apiserver.service
  ```
  - `/etc/systemd/system/kube-apiserver.service`에서 실행중인 서비스를 확인할 수 있음
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/ba813d99-5215-4f81-92e7-237d221ce501)
  ```Shell
  ps -aux | grep kube-apiserver
  ```
  - 프로세스를 마스터노드에 나열하고 `kube-apiserver`를 검색하면 프로세스 실행과 효과적인 옵션을 볼 수 있음
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/a356b835-649a-4b7a-abca-2bc6e494c24e)
  
---

### Kube Controller Manager

#### Kube Controller Manager의 역할
- Kube Controller Manager는 Kubernetes에서 다양한 컨트롤러를 관리함
- 컨트롤러는 Kubernetes 시스템의 다양한 구성 요소의 상태를 지속적으로 모니터링
- 전체 시스템을 원하는 상태로 유지하기 위해 필요한 조치를 취함

#### Controller
- **노드 컨트롤러 (Node Controller)**
  ```Shell
  kubectl get nodes
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/6471252a-789d-4039-8981-2a9917f2d0e8)
  - 노드의 상태를 모니터링
  - 5초마다 노드의 상태를 점검하여, 노드가 연결되지 않은 상태로 40초 동안 유지되면 해당 노드를 연결할 수 없다고 표시
  - 노드가 연결되지 않은 상태로 5분이 지나면 해당 노드에 할당된 POD를 제거하고, POD가 복제본 세트의 일부인 경우 다른 건강한 노드에 POD를 재프로비저닝함

- **복제 컨트롤러 (Replication Controller)**
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/6cf93d4d-e39e-4347-b894-47d3378a64ed)
  - 복제 세트 내에서 항상 원하는 수의 POD가 실행 중인지 확인함
  - POD가 종료되면 새로운 POD를 생성함

- **기타 컨트롤러**
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/bd921ea4-8d8f-4e7b-b0d4-e2bf0d62e412)
  - 다양한 Kubernetes 리소스를 관리하는 많은 다른 컨트롤러가 있음
    - Deployment(배포), Service-Account(서비스), Namespace(네임스페이스), Persistent Volume(영구 볼륨) 등
  - 각 컨트롤러는 시스템의 특정 부분을 담당하며, 클러스터의 상태를 원하는 상태로 유지하기 위해 협력함

#### Kube Controller Manager의 설치 및 구성
- Kube Controller Manager는 여러 컨트롤러를 단일 프로세스로 패키징한 것
- 설치
  - **Kube Controller Manager 다운로드**
    ```Shell
    wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-controller-manager
    ```
    ![image](https://github.com/seonwook97/Certificate/assets/92377162/3ca04e3b-ba23-4085-8de8-a973156fed60)
    - Kubernetes 릴리스 페이지에서 Kube Controller Manager 바이너리를 다운로드함
  - **추출 및 실행**
    - 바이너리를 추출하고 서비스로 실행함
      - 컨트롤러 중 일부가 작동하지 않거나 존재하지 않음

#### 옵션 설정
- **Kube Controller Manager를 실행할 때 많은 옵션을 설정할 수 있음**
  - **노드 감시 기간, 유예 기간 및 퇴거 시간 초과**와 같은 노드 컨트롤러의 설정
  - **활성화할 컨트롤러**를 지정하는 옵션
  - 기본적으로 모든 컨트롤러가 활성화되어 있지만, 필요에 따라 특정 컨트롤러만 활성화할 수도 있음
- Kube 관리자가 Kube Controller Manager를 배표
- 마스터 노드의 kube-system NAMESPACE에 POD로 저장됨
  ```Shell
  kubectl get pods -n kube-system
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/d671dfd0-85e3-4fa6-a87b-cc7ab08dbf8f)

- **Kube 관리자가 아닌 설정에서는 옵션을 검사할 수 있음**
  ```Shell
  cat /etc/kubernetes/manifests/kube-controller-manager.yaml
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/57d23cee-38f1-423f-8446-852d0e2aa08b)

- **Kube Controller Manager 서비스를 확인하여 실행중인 프로세스를 볼 수 있음**
  ```Shell
  cat /etc/systemd/system/kube-controller-manager.service
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/7e212d12-8e3e-4ed0-8d18-65c9f620d6ae)

- **마스터 노드에 실행중인 프로세스를 나열하여 Kube Controller Manager 옵션 확인**
  ```Shell
  ps -aux | grep kube-controller-manager
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/c961bd1b-12ae-4753-849c-095c94836e00)
