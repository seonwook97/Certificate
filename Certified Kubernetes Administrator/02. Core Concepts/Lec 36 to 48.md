## 2. Core Concepts

### Services

#### Service 개요
![image](https://github.com/seonwook97/Certificate/assets/92377162/300eff40-da48-495a-9cf8-c9b2af6f945a)
- 쿠버네티스 서비스는 애플리케이션 내부 구성요소 간 그리고 외부와의 통신을 가능하게 함
- 마이크로서비스 간의 느슨한 결합을 가능하게 함
- 주요 기능:
  - 내부 구성요소 간 통신 지원
  - 외부 사용자의 접근 지원
  - 프런트엔드와 백엔드 간 통신 지원
  - 외부 데이터 소스와의 연결 지원

#### Service 유형
![image](https://github.com/seonwook97/Certificate/assets/92377162/d08a77ea-8853-4b30-8ca0-4f96a8d6a5c0)
- **NodePort**: 노드의 포트를 통해 Pod에 접근 가능하게 함
- **ClusterIP**: 클러스터 내부 통신을 위한 가상 IP 생성
- **LoadBalancer**: 클라우드 제공자의 로드 밸런서 프로비저닝

#### NodePort Service 상세
![image](https://github.com/seonwook97/Certificate/assets/92377162/f8c3574c-3cb7-4805-889a-911f9daab7e7)
- **targetPort**: Pod의 실제 애플리케이션 포트 (예: 80)
- **port**: 서비스 자체의 포트
- **nodePort**: 노드의 외부 접근 포트 (기본 범위: 30000-32767)

#### NodePort Service YAML 파일 정의
![image](https://github.com/seonwook97/Certificate/assets/92377162/3dc2133c-da8a-4646-a938-531a1372e677)
```yaml
apiVersion: v1
kind: Service
metadata:
    name: myapp-service
spec: # Service 정의
    type: NodePort # 서비스의 유형: ClusterIP, Nodeport, LoadBalancer
    ports: # list type
     - targetPort: 80 # targetPort를 정의하지 않으면 port와 동일한 것으로 가정
       port: 80 # 필수 필드
       nodePort: 30008 # nodePort를 정의하지 않으면 30,000~32,767 자동 할당
    selector: # Pod YAML에서 labels를 참조
       app: myapp
       type: front-end
```

**Service 정의 파일 생성**
```sh
kubectl create –f service-definition.yml
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/edcb0e6e-0083-416c-afec-f244a6b88c97)

**Service 보기**
```sh
kubectl get services
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/66edf695-87ed-472e-bd2a-202635cd4297)

**Service 실행**
```sh
curl http://192.168.1.2:30008
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/66533ce3-1639-4623-bd0d-22ce033f7a13)

**다중 Pod 지원**
![image](https://github.com/seonwook97/Certificate/assets/92377162/c2dd29ec-d38f-4aaa-8f62-39ee4c88d8f3)
- 서비스는 라벨 셀렉터를 사용하여 여러 Pod에 연결 가능
- 내장된 로드 밸런서로 무작위 알고리즘을 사용하여 트래픽 분산

**다중 Node 환경**
![image](https://github.com/seonwook97/Certificate/assets/92377162/297b6905-5288-484b-8a81-5dc1bafa7e50)
- 서비스는 자동으로 모든 노드의 동일한 nodePort에 매핑됨
- 클러스터의 모든 노드 IP와 해당 nodePort로 접근 가능
- 서비스의 유연성
  - Pod의 추가/제거 시 서비스가 자동으로 업데이트됨
  - 생성 후 추가 구성 변경이 거의 필요 없음

--- 

### Services Cluster IP

#### ClusterIP Service 개요
![image](https://github.com/user-attachments/assets/0a8cabf5-4679-41b6-a97e-3d51656adc87)
- 풀 스택 웹 애플리케이션의 다양한 구성 요소 간 내부 통신을 위한 서비스
  - 예: 프런트엔드 웹 서버, 백엔드 서버, Redis, MySQL 등
- Pod IP의 동적 특성으로 인한 통신 문제 해결

#### ClusterIP 서비스의 역할
- Pod를 그룹화하고 단일 인터페이스 제공
- 서비스 내 Pod 간 로드 밸런싱 (무작위 알고리즘)
- 마이크로서비스 기반 애플리케이션(MSA)의 효과적인 배포 지원
- 각 서비스에 고유한 IP와 이름 할당

#### ClusterIP Service YAML 파일 정의
```yaml
apiVersion: v1
kind: Service
metadata:
    name: backend
spec:
    type: ClusterIP  # 자동으로 추정
    ports:
     - targetPort: 80
       port: 80
    selector:
       app: myapp
       type: backend
```

**Service 정의 파일 생성**
```sh
kubectl create –f service-definition.yml
```
![image](https://github.com/user-attachments/assets/4f3d06e2-4e91-4291-8d80-dccacbbef623)

**Service 보기**
```sh
kubectl get services
```
![image](https://github.com/user-attachments/assets/08dbf300-d3af-464e-af7b-0e635e97a2b4)

**ClusterIP 서비스 특징**
- 클러스터 내부에서만 접근 가능
- 다른 Pod에서 서비스 이름 또는 ClusterIP로 접근
- 기본 서비스 유형 (type을 지정하지 않으면 ClusterIP로 생성)

**ClusterIP 서비스의 이점**
- 동적 Pod IP 변경에 관계없이 안정적인 통신 제공
- 서비스 레이어 간 독립적인 확장 및 이동 가능
- 마이크로서비스 아키텍처(MSA) 지원

---

### Services - LoadBalancer

#### LoadBalancer Service 개요
- 외부 사용자가 애플리케이션에 접근할 수 있게 하는 서비스 타입
- 클라우드 제공업체의 로드 밸런서와 통합되어 작동

#### NodePort vs LoadBalancer
- NodePort: 워커 노드의 특정 포트를 통해 애플리케이션 노출
- LoadBalancer: 클라우드 제공업체의 로드 밸런서를 통해 단일 엔드포인트 제공

#### LoadBalancer Service의 필요성
<img width="726" alt="image" src="https://github.com/user-attachments/assets/3830bffd-1812-44ba-89f0-b6096fa9d523">

- 여러 노드와 포트 조합 대신 단일 URL 제공 (예: votingapp.com)
- 수동으로 외부 로드 밸런서를 설정하고 관리하는 번거로움 해소
- 지원되는 클라우드 플랫폼에서만 완전히 작동 (GCP, AWS, Azure 등)
- 서비스 타입을 'LoadBalancer'로 설정하여 사용

#### LoadBalancer Service YAML 파일 정의
```yaml
apiVersion: v1
kind: Service
metadata:
    name: frontend-loadbalancer
spec:
    type: LoadBalancer
    ports:
     - targetPort: 80
       port: 80
       nodePort: 30008       
    selector:
       app: myapp
       type: frontend-loadbalancer
```

---

### Namespaces

#### Namespace 개요
- 쿠버네티스 클러스터 내 가상 클러스터
- 리소스 격리 및 조직화에 사용
- 다중 사용자 환경에서 리소스 충돌 방지

#### 기본 Namespace
![image](https://github.com/user-attachments/assets/d72f3c48-e5b8-4596-975f-b302bc09a3f1)

- **default**: 기본적으로 생성되는 객체가 위치
- **kube-system**: 쿠버네티스 시스템 컴포넌트와 서비스가 위치
- **kube-public**: 모든 사용자가 접근 가능한 공개 리소스 위치

#### Namespace 사용 이점
- 개발/운영 환경 분리
  ![image](https://github.com/user-attachments/assets/8c764a37-329c-4438-a7b5-f434cacee063)

- 리소스 정책 및 할당량 관리
  <img width="657" alt="image" src="https://github.com/user-attachments/assets/78bb8114-2d4f-4ecf-9243-dea5e1b062cd">

- 팀 또는 프로젝트별 리소스 분리
  ![image](https://github.com/user-attachments/assets/533d0d29-0082-4dac-8b28-182bda26d223)

#### Namespace 간 통신
- 같은 namespace 내: 서비스 이름으로 통신
- 다른 namespace: `<servicename>.<namespace>.svc.cluster.local` 형식 사용
  <img width="631" alt="image" src="https://github.com/user-attachments/assets/d6af34c6-d2e6-48b4-ad60-f18ccd104951">
  ![image](https://github.com/user-attachments/assets/43b00f8e-6152-44f7-a6d4-eb7cf29e0925)


#### Namespace 관련 명령어
```sh
# 기본 namespace 파드 나열
kubectl get pods

# 특정 namespace의 파드 나열
kubectl get pods --namespace=kube-system
```
![image](https://github.com/user-attachments/assets/f7554f61-7508-4619-9223-295fa876b316)

#### Namespace YAML 파일 정의
```sh
# 기본 namespace에 파드 생성
kubectl create -f pod-definition.yml

# 특정 namespace에 파드 생성
kubectl create -f pod-definition.yml --namesapce=dev
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  namespace: dev # 특정 namespace에 생성할 때
  labels:
     app: myapp
     type: front-end
spec:
  containers:
  - name: nginx-container
    image: nginx
```
<img width="326" alt="image" src="https://github.com/user-attachments/assets/18d655b0-7839-440a-982b-34593b05c2ff">

#### Namespace 생성
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
```

```sh
# yml 생성
kubectl create -f namespace-dev.yml

# namespace 생성
kubectl create namespace dev
```

#### 현재 컨텍스트의 Namespace 변경
```sh
kubectl config set-context  $(kubectl config current-context) --namespace=dev
```
- 그 밖
![image](https://github.com/user-attachments/assets/37ae1d26-b172-4626-a896-ace4169f0e58)

#### Namespace 리소스 할당량 생성
![image](https://github.com/user-attachments/assets/30f281c6-e905-4a97-82af-a599e030d9c7)

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
    name: compute-quota
    namespace: dev
spec:
  hard:
    pods: “10"
    requests.cpu: “4"
    requests.memory: 5Gi
    limits.cpu: “10"
    limits.memory: 10Gi
```

```sh
kubectl create -f compute-quota.yaml
```

---

### Imperative vs Declarative

#### Infrastructure as Code
![image](https://github.com/user-attachments/assets/7449028d-b02a-4a60-8c08-ded88923cfdd)

- **Imperative**: 목적지에 도달하기 위해 무엇을, 어떻게 할건지 명시해야 함
  - 'web-server'라는 이름의 VM을 프로비저닝
  - 해당 VM에 NGINX 소프트웨어를 설치
  - 설정 파일을 편집하여 포트 '8080'을 사용하도록 함
  - 설정 파일을 편집하여 웹 경로를 '/var/www/nginx'로 설정
  - GIT 저장소 X에서 '/var/www/nginx'로 웹 페이지를 로드
  - NGINX 서버를 시작

- **Declarative**: 최종 목적지 지정 후(무엇을 할건지) 시스템이 올바른 경로를 통해 도달. 단계별 지침을 제공하지 않음(어떻게 할건지)
  - VM Name: web-server
  - Package: nginx
  - Port: 8080
  - Path: /var/www/nginx
  - Code: GIT Repo - X

#### Kubernetes
- **Imperative Commands**
  - 장점: 빠른 생성 및 수정, YAML 파일 불필요
  - 단점: 기능 제한, 복잡한 사용 사례에 부적합, 추적 어려움
  - Create Objects
    ```sh
    kubectl run --image=nginx nginx
    kubectl create deployment --image=nginx nginx
    kubectl expose deployment nginx --port 80
    ```
  - Update Objects
    ```sh
    kubectl edit deployment nginx
    kubectl scale deployment nginx --replicas=5
    kubectl set image deployment nginx nginx=nginx:1.18
    ```

- **Imperative Object Configuration Files**
  - 장점: YAML 파일로 구성 관리, 버전 관리 가능
  - 단점: 현재 상태 확인 필요, 오류 발생 가능
  - Create Objects
    ```sh
    kubectl create –f nginx.yaml
    ```
  - Update Objects
    ```sh
    kubectl replace –f nginx.yaml
    kubectl delete –f nginx.yaml
    ```

- **Declarative**
  - 장점:
    - 현재 상태를 자동으로 확인하고 필요한 변경사항만 적용
    - 여러 오브젝트 동시 관리 가능
    - 일관된 명령으로 생성, 수정, 삭제 가능
  - 단점: 복잡한 변경사항 추적이 어려울 수 있음
  - Create Objects
    ```sh
    kubectl apply –f nginx.yaml
    kubectl apply –f /path/to/config-files
    ```
  - Update Objects
    ```sh
    kubectl apply –f nginx.yaml
    ```

#### Exam Tips
- 실제 환경: 선언형 접근 방식 사용 (kubectl apply)
- 시험 환경: 상황에 따라 명령형과 선언형 접근 방식 혼용
- Kubernetes 공식 문서 참조하여 다양한 접근 방식 숙지
  - https://kubernetes.io/docs/tasks/manage-kubernetes-objects/

---

### Certification Tips - Imperative Commands with Kubectl

#### 유용한 옵션
- `--dry-run=client`: 실제로 리소스를 생성하지 않고 명령의 유효성 검사
- `-o yaml`: 리소스 정의를 YAML 형식으로 출력

#### POD 관련 명령
```sh
# NGINX Pod 생성
kubectl run nginx --image=nginx

# Pod YAML 파일 생성 (생성하지 않음)
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

#### Deployment 관련 명령
```sh
# Deployment 생성
kubectl create deployment --image=nginx nginx

# Deployment YAML 파일 생성 (생성하지 않음)
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

# 4개의 Replica로 Deployment 생성
kubectl create deployment nginx --image=nginx --replicas=4

# 스케일 조정을 통한 Deployment 확장
kubectl scale deployment nginx --replicas=4

# YAML 파일로 저장 후 수정
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml
```

#### Service 관련 명령
```sh
# redis pod를 포트 6379에 노출하는 ClusterIP 타입의 redis-service라는 이름의 Service 생성
# (1) 자동으로 pod의 label을 selector로 사용
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml 
# (2) pod의 label을 selector로 사용하지 않고, 대신 selector를 app=redis로 가정 - selector 수정 필요
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml 

# 노드의 포트 30080에서 nginx pod의 포트 80을 노출하는 NodePort 타입의 nginx라는 이름의 Service 생성
# (1) node port를 지정할 수 없어, YAML 생성 후 service 생성 전 수동으로 node port 추가 필요
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
# (2) pod의 label을 selector로 사용하지 않음
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
```

#### Reference
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands
- https://kubernetes.io/docs/reference/kubectl/conventions/

---

### Kubectl Apply Command

#### kubectl apply 명령의 세 가지 요소
- local file
- last applied configuration(마지막으로 적용된 구성)
- kubernetes live object configuration(라이브 객체 정의)

#### 객체 생성 과정
- 객체가 존재하지 않으면 생성됨
- Kubernetes 내에 객체 구성이 생성됨
  - 로컬에서 생성한 것과 유사하지만 객체 상태를 저장하는 추가 필드가 있음
  - Kubernetes 클러스터의 라이브 구성

#### kubectl apply 명령의 추가 동작
- local file의 YAML 버전을 JSON 형식으로 변환함
- last applied configuration으로 저장

#### 객체 업데이트 과정
- 세 가지 구성(로컬, 라이브, 마지막 적용)을 비교
- 라이브 객체에 필요한 변경 사항을 식별함
  - 예: local file에서 nginx 이미지가 1.19로 업데이트된 경우
    - 이 값을 live object configuration의 값과 비교
    - 차이가 있으면 live object configuration을 새 값으로 업데이트
- 변경 후, last applied configuration을 항상 최신 상태로 업데이트

#### 필드 삭제 처리
- local file에서 필드가 삭제된 경우
  - last applied configuration에는 있지만 local file에는 없는 경우
  - 해당 필드를 live object configuration에서 제거해야 함을 의미
- live object configuration에만 있고 local file이나 last applied configuration에 없는 필드는 그대로 둠
- local file에서 누락되고 last applied configuration에 있는 필드
  - 이전 단계에서 존재했지만 현재 제거되고 있음을 의미
  - 이 필드는 live object configuration에서 제거됨

#### last applied configuration의 저장 위치
- Kubernetes 클러스터의 live object configuration에 주석으로 저장됨
- 주석 이름: "last-applied-configuration"

#### 주의사항
- apply 명령을 사용할 때만 last applied configuration이 저장됨
- kubectl create 또는 replace 명령은 이 구성을 저장하지 않음
- 명령형과 선언형 접근 방식을 혼합하여 사용하지 않도록 주의
- **apply 명령은 변경 사항이 있을 때마다 세 가지 구성을 모두 비교**
- **이를 통해 live object configuration에 필요한 변경 사항을 결정**