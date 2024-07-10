## 2. Core Concepts

### Recap - ReplicaSets

#### Replication Controller
- 컨트롤러는 Kubernetes의 두뇌 역할을 하며, Kubernetes 객체를 모니터링하고 그에 따라 대응하는 프로세스

#### Replication Controller의 필요성
![image](https://github.com/seonwook97/Certificate/assets/92377162/b3613789-4797-4506-99f9-30bb49059a12)
- 애플리케이션을 실행하는 단일 포드가 있는 경우, 포드가 충돌하거나 고장 나면 애플리케이션에 접근할 수 없게됨 - 이를 방지하기 위해 복제 컨트롤러를 사용하여 여러 인스턴스를 실행할 수 있음
- 복제 컨트롤러는 단일 포드의 여러 인스턴스를 실행하여 높은 가용성을 제공함
- 포드가 실패하면 자동으로 새로운 포드를 생성하여 항상 지정된 수의 포드가 실행 중임을 보장함
  
![image](https://github.com/seonwook97/Certificate/assets/92377162/af4ada35-b5f9-4a0a-8b33-b53b28f76cbb)
- 복제 컨트롤러의 또 다른 사용 사례는 부하 분산
- 사용자 수가 증가하면 추가 포드를 배치하여 부하를 분산시킬 수 있음
- 이는 여러 노드에 걸쳐 포드를 분산 배치하여 애플리케이션의 확장성을 향상시킴

#### Replication Controller와 Replica Set
- 복제 컨트롤러는 이전 기술이며, 현재는 복제 세트(Replica Set)로 대체됨
- Replica Set은 복제 컨트롤러와 유사하지만, 더 많은 기능을 제공함
  - 모든 데모와 구현에서는 Replica Set을 사용예정

#### Replication Controller 생성
**YAML 파일 정의**
```yaml
apiVersion: v1 # Kubernetes API 버전 (v1)
kind: ReplicationController # 객체의 종류 (ReplicationController)
metadata: # 객체의 이름과 라벨
  name: my-app-rc
  labels:
      app: my-app
      type: front-end
spec: # 객체의 사양으로, 복제본 수와 포드 템플릿을 포함
  ##### pod-definition.yml #####
  template:
    metadata:
     name: my-app-pod
     labels:
        app: my-app
        type: frontend
    spec:
      containers:
      - name: my-app-container
        image: nginx
  ##############################
  replicas: 3
```
**Replication Controller 생성**
```sh
kubectl create –f rc-definition.yml
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/a1766d59-6d87-45de-a302-5eef48161739)

**Replication Controller 목록 확인**
```sh
kubectl get replicationcontroller
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/cdc0ecc7-4673-4781-9fe0-f0b8f81754e8)

**Replication POD 확인**
```sh
kubectl get pods
```

#### Replica Set 생성
**YAML 파일 정의**
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-app-rs
  labels:
      app: my-app
      type: front-end
spec:
  ##### pod-definition.yml #####
  template:
    metadata:
     name: my-app-pod
     labels:
        app: my-app
        type: front-end
    spec:
      containers:
      - name: my-app-container
        image: nginx
  ##############################
  replicas: 3
  selector: # Replica Set은 selector 추가 - 어떤 POD가 해당되는지 식별함
    matchLabels:
       type: front-end
```
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/80a69368-5656-4270-b45a-1661bab270af)
  - ReplicaapiVersion: v1 X -> apps/v1 O

**Replica Set 생성**
```sh
kubectl create –f replicaset-definition.yml
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/445403ad-c44b-4798-ad06-0b31e124d8f1)

**Replica Set 확인**
```sh
kubectl get replicaset
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/1407d102-dad6-41fa-a5c2-c84c188ba78e)

**POD 목록 확인**
```sh
kubectl get pods
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/728e087f-ba94-4935-a332-b4b1405cdbc6)

#### Labels and Selectors
![image](https://github.com/seonwook97/Certificate/assets/92377162/93c474bc-d7c2-49c4-a5d8-24ce0a25b604)
![image](https://github.com/seonwook97/Certificate/assets/92377162/a8696cb7-7f84-4a78-bc29-2a27fbb597fe)
- Replica Set은 실제로 POD를 모니터링하는 프로세스
- selector에서 matchLables를 사용하여 POD를 생성할 때 사용한 라벨과 동일한 라벨을 제공할 수 있음
- 이를 통해 Replica Set은 어떤 포드를 모니터링해야 할지 알 수 있음

#### Replica Set 확장
- 정의 파일에서 복제본 수를 업데이트한 후, `kubectl replace` 명령을 사용하여 파일을 지정
  ```yaml
  apiVersion: apps/v1
  kind: ReplicaSet
  metadata:
    name: my-app-rs
    labels:
        app: my-app
        type: front-end
  spec:
    template:
      metadata:
      name: my-app-pod
      labels:
          app: my-app
          type: front-end
      spec:
        containers:
        - name: my-app-container
          image: nginx
    replicas: 6 # 3 -> 6
    selector:
      matchLabels:
        type: front-end
  ```
  ```sh
  kubectl replace -f replicaset-definition.yml
  ```

- `kubectl scale` 명령을 사용하여 명령줄에서 직접 복제본 수를 업데이트
  ```sh
  kubectl scale -–replicas=6 –f replicaset-definition.yml
  ```
  ```sh
  kubectl scale -–replicas=6 replicaset myapp-replicaset # TYPE: replicaset, NAME: myapp-replicaset
  ```
  - YAML 파일에는 여전히 3개의 복제본이 지정되어 있을 수 있음
  - `kubectl scale` 명령이 정의 파일을 수정하지 않기 때문 

#### Replica Set 명령어
- Replica Set 생성
  ```sh
  kubectl create -f rs-definition.yaml
  ```
- Replica Set 목록 확인
  ```sh
  kubectl get replicaset
  ```
- POD 목록 확인
  ```sh
  kubectl get pods
  ```
- Replica Set 확장
  ```sh
  kubectl scale --replicas=6 -f rs-definition.yaml
  ```
- Replica Set 삭제
  ```sh
  kubectl delete replicaset my-app-rs # 추가로 모든 기본 POD를 삭제
  ```
- Replica Set 교체
  ```sh
  kubectl replace -f rs-definition.yaml
  ```

---

### Deployments

#### Deployment 개요
- 프로덕션 환경에서 애플리케이션 배포를 관리하는 고수준 Kubernetes 객체
- 주요 기능:
  - 다수의 애플리케이션 인스턴스 실행
  - 롤링 업데이트를 통한 무중단 업그레이드
    - `롤링 업데이트`: 영향도에 따른 순차적 인스턴스 업그레이드
  - 롤백 기능
  - 환경 변경 일시 중지 및 재개

#### Deployment의 위치
<img width="573" alt="image" src="https://github.com/seonwook97/Certificate/assets/92377162/70718bfa-2ad6-4a93-83c6-5215ac531875">

- **Pod**: 단일 애플리케이션 인스턴스
- **ReplicaSet**: 여러 Pod 관리
- **Deployment**: ReplicaSet을 관리하며 추가 기능 제공

#### Deployment 생성
**YAML 파일 정의**
```yaml
apiVersion: apps/v1
kind: Deployment # 배포
metadata:
  name: my-app-deployment
  labels:
    app: my-app
    type: front-end
spec:
  replicas: 3
  selector:
    matchLabels:
      type: front-end
  template:
    metadata:
      labels:
        app: my-app
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx
```

**Deployment 정의 파일 생성**
```sh
kubectl create –f deployment-definition.yml
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/75c9e867-f868-4b1a-8b9b-8bacc38ed869)

**Deployments 실행**: ReplicaSet을 자동으로 생성
```sh
kubectl get deployments
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/bb9f1c56-b51c-47db-b8ba-8323594effad)

**ReplicaSet 실행**: Pods를 자동으로 생성
```sh
kubectl get replicaset
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/bce02f8c-69c2-42fc-a30a-616dcdf0b283)

**Pods 가져오기**: 배포와 복제세트 이름이 적힌 파드를 볼 수 있음
```sh
kubectl get pods
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/ec48a8ed-708d-41b4-aacb-d55522b4d03d)

**생성된 객체 한번에 보기**
```sh
kubectl get all
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/12768391-fd30-4973-90bd-33d6fa865ce2)