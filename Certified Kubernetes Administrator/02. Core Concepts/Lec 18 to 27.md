## 2. Core Concepts

### kube-scheduler

#### kube-scheduler의 역할
![image](https://github.com/seonwook97/Certificate/assets/92377162/60f3fc84-3892-4ae9-ad24-1e24b73165b3)
- 스케줄러는 어느 Pod가 어느 노드에 위치할지를 결정함
- 실제로 Pod를 노드에 배치하는 작업은 kubelet의 역할

#### kube-scheduler가 필요한 이유
- **리소스 확인**: 스케줄러는 각 컨테이너가 필요한 리소스를 확인하고 올바른 노드에 배치함
- **노드의 용량**: 스케줄러는 노드의 CPU 및 메모리 용량을 고려하여 Pod를 배치함
- **다양한 목적지**: 노드가 다양한 용도로 사용될 수 있으므로, 스케줄러는 올바른 목적지에 컨테이너가 배치되도록 함

#### kube-scheduler의 동작 방식
- **필터링**: Pod의 요구 사항을 충족하지 않는 노드를 필터링함. 예를 들어, CPU나 메모리가 부족한 노드를 제외함
- **우선순위 매기기**: 남은 노드들 중에서 가장 적합한 노드를 선택함. 이는 노드에 점수를 매겨 결정. 점수는 0에서 10까지의 척도로 매겨지며, 리소스가 많이 남아 있는 노드가 높은 점수를 받음

#### kube-scheduler의 설치
```Shell
wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-scheduler
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/df0fb5c6-97ef-457d-a8bb-d4b5da9b99b2)
- Kubernetes 릴리스 페이지에서 kube-scheduler 바이너리를 다운
- 서비스 실행 시 스케줄러 구성 파일을 지정함

```Shell
cat /etc/kubernetes/manifests/kube-scheduler.yaml
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/0b84236a-73c6-4ac9-bf2c-810adad1974d)
- kubeadm 도구를 사용하면, kube-scheduler는 마스터 노드의 kube-system 네임스페이스에 Pod로 배포
- Pod 정의 파일은 `/etc/kubernetes/manifests/` 폴더에 위치함

```Shell
ps -aux | grep kube-scheduler
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/85b3f6ce-f293-483d-9ab7-ede27888904c)
- 프로세스를 마스터 노드에 나열하고 kube-scheduler를 검색하여 프로세스 실행과 효과적인 옵션을 볼 수 있음 

---

### kubelet 

#### kubelet의 역할
![image](https://github.com/seonwook97/Certificate/assets/92377162/889cbaec-f225-4309-ac1b-aa5a9237ae6f)
- Kubernetes 작업자 노드에서 실행되는 에이전트
  - **클러스터 등록**: 작업자 노드를 Kubernetes 클러스터에 등록함
  - **컨테이너 관리**: 마스터 노드의 스케줄러 지시에 따라 노드에 컨테이너(Pod)를 배포하거나 제거함
  - **상태 보고**: 정기적으로 노드와 컨테이너의 상태를 모니터링하고 kube API 서버에 보고함

#### kubelet 설치
```Shell
wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kubelet
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/d90de9e7-01e9-405f-9a32-3ef7d0007f3b)
  - kubeadm 지원 X. kubelet은 항상 수동으로 설치해야 함
  - kubelet을 서비스로 실행함 실행 중인 kubelet 프로세스를 확인할 수 있음

#### kubelet 구성
```Shell
ps -aux | grep kubelet
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/8353ec58-f995-476c-855d-06e5abc14e0c)
- 프로세스를 작업자 노드에 나열하고 kubelet을 검색하여 실행중인 프로세스와 효과적인 옵션 확인
  - **설정 파일 편집**: kubelet의 설정 파일을 편집하여 필요한 구성을 적용함
  - **인증서 생성**: kubelet이 클러스터 내에서 인증되도록 인증서를 생성함
  - **TLS Bootstrap**: kubelet을 TLS Bootstrap으로 설정하여 보안 통신을 설정함

---

### kube-proxy

#### kube-proxy의 역할
- Kubernetes 클러스터 내에서 모든 Pod는 서로에게 접근할 수 있음
- 이를 위해 클러스터에 Pod 네트워크 솔루션이 배포됨
- Pod 네트워크는 클러스터 내 모든 노드에 걸쳐 있는 내부 가상 네트워크로, 모든 Pod가 이 네트워크에 연결됨

#### Pod 네트워크와 서비스
- 첫 번째 노드에 웹 애플리케이션이 배포되고 두 번째 노드에 데이터베이스 애플리케이션이 배포된 경우
  - 웹 애플리케이션은 단순히 Pod의 IP를 사용하여 데이터베이스에 접근할 수 있음
  - 그러나 데이터베이스 Pod의 IP가 항상 동일하게 유지된다는 보장은 없음
  - 따라서 웹 애플리케이션이 데이터베이스에 접근하는 더 나은 방법은 서비스를 사용하는 것
- 서비스는 클러스터 전체에서 데이터베이스 애플리케이션을 노출함
- 웹 애플리케이션은 서비스 이름인 `DB`를 사용하여 데이터베이스에 접근할 수 있음 
  - 서비스는 IP 주소도 할당받음
- Pod가 서비스의 IP 또는 이름을 사용하여 서비스에 접근하려고 할 때, 트래픽은 백엔드 Pod, 이 경우에는 데이터베이스로 전달됨

#### kube-proxy의 역할
- 서비스는 실제 컨테이너가 아니므로 Pod 네트워크에 참여할 수 없음
- 서비스는 Kubernetes 메모리에만 존재하는 가상 구성 요소
- 그러나 서비스는 클러스터의 모든 노드에서 접근 가능해야 하며 이를 가능하게 하는 것이 **kube-proxy**
- **kube-proxy**는 Kubernetes 클러스터의 각 노드에서 실행되는 프로세스임
- kube-proxy는 새로운 서비스가 생성될 때마다 해당 서비스로의 트래픽을 백엔드 Pod로 전달하는 적절한 규칙을 각 노드에 생성함
  - 이는 iptables 규칙을 사용하여 수행됨 
  - 서비스의 IP가 10.96.0.12이고 실제 Pod의 IP가 10.32.0.15인 경우, **kube-proxy**는 클러스터의 각 노드에 트래픽을 서비스 IP에서 실제 Pod IP로 전달하는 iptables 규칙을 생성함

#### kube-proxy 설치
```Shell
wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-proxy
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/f7914418-60a6-44e2-9ac5-0844d834531c)
- Kubernetes 릴리스 페이지에서 kube-proxy 바이너리를 다운, 압축 해제 후 서비스 실행

```Shell
kubectl get pods -n kube-system
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/e7770e12-e264-4c13-b041-19a470c59aba)
- kubeadm 도구는 각 노드에 Pod로 kube-proxy를 배포함 
```Shell
kubectl get daemonset -n kube-system
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/155fe4ad-0c7e-4175-988b-972ccd59dc0f)
- 사실은 DaemonSet으로 배포되며, 클러스터의 각 노드에 항상 하나의 Pod가 배포됨

---

### Recap - Pods

#### Pod 이해하기

- 설정사항 가정:
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/69d57d62-91fc-432b-9554-b682931f520e)
  - 애플리케이션이 개발되어 Docker 이미지로 만들어졌으며, Docker Hub와 같은 Docker 저장소에 업로드되어 있음
  - Kubernetes 클러스터가 이미 설정되어 작동 중. 이는 단일 노드 설정일 수도 있고 다중 노드 설정일 수도 있음

![image](https://github.com/seonwook97/Certificate/assets/92377162/558c5915-56bf-4410-a8f7-ac8e95150c01)
- Kubernetes의 궁극적인 목표는 애플리케이션을 컨테이너 형태로 클러스터의 작업자 노드에 배포하는 것
- 하지만 Kubernetes는 컨테이너를 직접 배포하지 않고, 컨테이너를 Kubernetes 객체인 Pod에 캡슐화하여 배포함
- Pod는 애플리케이션의 단일 인스턴스를 나타내며, Kubernetes에서 만들 수 있는 가장 작은 단위

#### Pod의 동작 방식

**단일 컨테이너 Pod**
- 가장 간단한 경우는 단일 노드 Kubernetes 클러스터에서 단일 Docker 컨테이너로 애플리케이션을 실행하는 것
- Pod는 이 단일 컨테이너를 캡슐화함

**여러 인스턴스 확장**
![image](https://github.com/seonwook97/Certificate/assets/92377162/06e6b8ce-8c27-4b01-8823-93a3813d4551)
- 사용자가 증가하면 애플리케이션을 확장해야 함
- 이를 위해 새로운 Pod를 생성하여 애플리케이션의 추가 인스턴스를 배포함
- 기존 Pod에 추가 컨테이너를 추가하는 것이 아니라, 새로운 Pod를 생성하여 확장

**다중 컨테이너 Pod**
![image](https://github.com/seonwook97/Certificate/assets/92377162/9c6fa49c-9636-4e16-9a8e-68f1ed476d51)
- 하나의 Pod에 여러 컨테이너를 포함할 수도 있음
- 이는 주로 도우미 컨테이너와 같은 보조 작업을 수행하는 경우에 사용됨
  - 예를 들어, 데이터 처리를 위한 도우미 컨테이너와 함께 웹 애플리케이션을 실행할 수 있음
  - 이 경우, 두 컨테이너는 동일한 Pod 내에서 생성되고 함께 소멸되며, 동일한 네트워크 및 저장소 공간을 공유할 수 있음

#### Docker와 비교
![image](https://github.com/seonwook97/Certificate/assets/92377162/1e07b840-073f-4586-beeb-f27c127b0f4d)
- Docker 환경에서 여러 컨테이너를 관리하는 것은 복잡함
- 네트워크 연결, 볼륨 공유 및 상태 모니터링 등을 수동으로 관리해야 함
- 그러나 Kubernetes는 Pod를 사용하여 이러한 작업을 자동으로 처리함
- Pod는 컨테이너 간의 네트워크와 저장소 공유를 자동으로 설정하며, 상태 모니터링과 관리도 자동화함

#### Pod 배포

- Pod를 배포하기 위해 `kubectl run` 명령을 사용할 수 있음
  - 이 명령은 Docker 컨테이너를 배포하기 위해 자동으로 Pod를 생성함
- NGINX Docker 이미지를 배포
  ```shell
  kubectl run nginx --image=nginx
  ```
- Pod 목록 확인 
  ```shell
  kubectl get pods
  ```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/d038557f-dc97-4e3a-bda3-e41d8f169968)
  
### Pods with YAML

#### Pod YAML 구성
```yaml
apiVersion: v1 -- String
kind: Pod -- String
metadata: -- Dictionary  
  name: my-app-pod # 객체의 이름 지정
  labels: # 객체를 식별하는 key-value, 여러 레이블을 추가하여 객체를 필터링하고 그룹화 할 수 있음
    app: my-app
spec:
  containers: -- List/Array # 여러 개의 컨테이너를 포함할 수 있음 
    - name: my-app-container
      image: nginx
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/41bfdc50-9904-492f-a454-b7b84fc2e826)
- apiVersion(API 버전): API 버전은 Kubernetes API의 버전을 나타냄(ex. `v1`)
- kind(종류): 생성하려는 객체의 유형(`pod`, `replica set`, `deployment`, `service`) 
- metadata(메타데이터): 객체에 대한 정보를 담고 있으며, 이름과 레이블을 포함. 딕셔너리 형태
- spec(사양): 객체의 구성, Pod의 경우 컨테이너 정보를 포함

#### 파일 생성 및 Pod 생성
```Shell
kubectl create -f pod-definition.yaml
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/50f10f69-4461-4ddf-a054-0de9066c46d1)

#### Pod 확인
```Shell
kubectl get pods
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/efac840c-940e-4a59-882c-f18c40b62398)

#### Pod 상세 정보
```Shell
kubectl describe pod my-app-pod
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/9211b554-d014-4438-9e59-239a194b75de)