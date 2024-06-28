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
  - kubelet을 서비스로 실행함 실행 중인 kubelet 프로세스를 확인할 수 있습니다.

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


