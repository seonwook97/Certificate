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

