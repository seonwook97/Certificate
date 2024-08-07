##  1. Introduction
- **CKA 시험 커리큘럼**: https://github.com/cncf/curriculum/blob/master/CKA_Curriculum_v1.30.pdf
- **CKA 시험 지침**: https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad
- **CKA kodekloud 강의노트**: https://github.com/kodekloudhub/certified-kubernetes-administrator-course

---

### CKA 시험 커리큘럼
- **25% - Cluster Architecture, Installation, and Configuration (클러스터 아키텍처, 설치 및 구성)** 
  - Managing Role-Based Access Control (RBAC) (역할 기반 액세스 제어 (RBAC) 관리)
  - Installing the base cluster using Kubeadm (Kubeadm을 사용하여 기본 클러스터 설치)
  - Managing High Availability Kubernetes clusters (고가용성 Kubernetes 클러스터 관리)
  - Provisioning underlying infrastructure for deploying Kubernetes clusters (Kubernetes 클러스터 배포를 위한 기반 인프라 프로비저닝)
  - Performing version upgrades of Kubernetes clusters using Kubeadm (Kubeadm을 사용하여 Kubernetes 클러스터의 버전 업그레이드 수행)
  - Implementing etcd backup and restore (etcd 백업 및 복원 구현)

- **15% - Workloads and Scheduling (워크로드 및 스케줄링)** 
  - Understanding deployment and rolling update/rollback strategies (배포 및 롤링 업데이트 및 롤백 전략 이해)
  - Configuring applications using ConfigMaps and Secrets (ConfigMaps 및 Secrets를 사용하여 애플리케이션 구성)
  - Understanding application scaling (애플리케이션 확장 이해)
  - Understanding the building blocks used to create resilient and self-healing application deployments (견고하고 자가 치유 기능을 갖춘 애플리케이션 배포 생성에 사용되는 기본 요소 이해)
  - Understanding how resource limits affect Pod scheduling (리소스 제한이 Pod 스케줄링에 어떤 영향을 미치는지 이해)
  - Awareness of manifest management and common templating tools (매니페스트 관리 및 일반적인 템플릿 도구 인식)

- **20% - Services and Networking (서비스 및 네트워킹)** 
  - Understanding host networking configuration on cluster nodes (클러스터 노드에서 호스트 네트워킹 구성 이해)
  - Understanding connectivity between Pods (Pod 간 연결성 이해)
  - Understanding ClusterIP, NodePort, LoadBalancer service types and endpoints (ClusterIP, NodePort, LoadBalancer 서비스 유형 및 엔드포인트 이해)
  - Understanding Ingress controllers and Ingress resources usage (Ingress 컨트롤러 및 Ingress 리소스 사용 방법 이해)
  - Understanding CoreDNS configuration and usage (CoreDNS 구성 및 사용 방법 이해)
  - Selecting appropriate container network interface plugins (적절한 컨테이너 네트워크 인터페이스 플러그인 선택)

- **10% - Storage (스토리지)** 
  - Understanding storage classes and persistent volumes (스토리지 클래스, 지속적인 볼륨 이해)
  - Understanding volume modes, access modes, and volume reclaim policies (볼륨 모드, 액세스 모드 및 볼륨 재클레임 정책 이해)
  - Understanding persistent volume claims basics (지속적인 볼륨 클레임 기본 요소 이해)
  - Understanding how to configure applications with persistent storage (지속적인 스토리지로 애플리케이션 구성 방법 이해)

- **30% - Troubleshooting (문제해결)**
  - Evaluating cluster and node logging (클러스터 및 노드 로깅 평가)
  - Understanding application monitoring (애플리케이션 모니터링 이해)
  - Managing container stdout and stderr logs (컨테이너 stdout 및 stderr 로그 관리)
  - Troubleshooting application failures (애플리케이션 장애 해결)
  - Troubleshooting cluster component failures (클러스터 구성 요소 장애 해결)
  - Troubleshooting networking failures (네트워킹 장애 해결)

---

### CKA kodekloud 강의 목표
- **Core Concepts (핵심 개념)**
  - Cluster Architecture (클러스터 아키텍처)
  - API Primitives (API 기본 요소)
  - Services & Other Network Primitives (서비스 및 기타 네트워크 기본 요소)

- **Scheduling (스케줄링)**
  - Labels & Selectors (라벨 및 셀렉터)
  - Daemon Sets (데몬셋)
  - Resource Limits (리소스 제한)
  - Multiple Schedulers (다중 스케줄러)
  - Manual Scheduling (수동 스케줄링)
  - Scheduler Events (스케줄러 이벤트)
  - Configure Kubernetes Scheduler (Kubernetes 스케줄러 구성)

- **Logging & Monitoring (로그 및 모니터링)**
  - Monitor Cluster Components (클러스터 구성 요소 모니터링)
  - Monitor Cluster Components Logs (클러스터 구성 요소 로그 모니터링)
  - Monitor Applications (애플리케이션 모니터링)
  - Application Logs (애플리케이션 로그)

- **Application Lifecycle Management (애플리케이션 라이프사이클 관리)**
  - Rolling Updates and Rollbacks in Deployments (배포에서 롤링 업데이트 및 롤백)
  - Configuring Applications (애플리케이션 구성)
  - Scale Applications (애플리케이션 확장)
  - Self-Healing Applications (자가 치유 애플리케이션)

- **Cluster Maintenance (클러스터 유지 보수)**
  - Cluster Upgrade Process (클러스터 업그레이드 프로세스)
  - Operating System Upgrades (운영 체제 업그레이드)
  - Backup and Restore Methodologies (백업 및 복원 방법론)

- **Security (보안)**
  - Authentication & Authorization (인증 및 권한 부여)
  - Kubernetes Security (Kubernetes 보안)
  - Network Policies (네트워크 정책)
  - TLS Certificates for Cluster Components (클러스터 구성 요소에 대한 TLS 인증서)
  - Image Security (이미지 보안)
  - Network Policies (네트워크 정책)
  - Security Contexts (보안 컨텍스트)
  - Secure Persistent Key Value Store (보안 지속적인 키-값 저장소)

- **Storage (스토리지)**
  - Persistent Volumes (지속적인 볼륨)
  - Access Modes for Volumes (볼륨 액세스 모드)
  - Persistent Volume Claims (지속적인 볼륨 클레임)
  - Kubernetes Storage Object (Kubernetes 스토리지 객체)
  - Configure Applications with Persistent Storage (지속적인 스토리지로 애플리케이션 구성)

- **Networking (네트워킹)**
  - Pre-Requisites - Network, Switching, Routing, Tools (사전 요구 사항 - 네트워크, 스위칭, 라우팅, 도구)
  - Pre-Requisites - Network Namespaces (사전 요구 사항 - 네트워크 네임스페이스)
  - Pre-Requisites - Networking in Docker (사전 요구 사항 - Docker에서의 네트워킹)
  - Networking Configuration on Cluster Nodes (클러스터 노드에서의 네트워킹 구성)
  - Service Networking (서비스 네트워킹)
  - POD Networking Concepts (POD 네트워킹 개념)
  - Network Loadbalancer (네트워크 로드밸런서)
  - Ingress (인그레스)
  - Cluster DNS (클러스터 DNS)
  - CNI

- **Installation, Configuration & Validation (설치, 구성 및 유효성 검사)**
  - Design a Kubernetes Cluster (Kubernetes 클러스터 설계)
  - Install Kubernetes Master and Nodes (Kubernetes 마스터 및 노드 설치)
  - Secure Cluster Communication (클러스터 통신 보안)
  - HA Kubernetes Cluster (고가용성 Kubernetes 클러스터)
  - Kubernetes Release Binaries (Kubernetes 릴리스 이진 파일)
  - Provision Infrastructure (인프라 프로비저닝)
  - Choose a Network Solution (네트워크 솔루션 선택)
  - Kubernetes Infrastructure Config (Kubernetes 인프라 구성)
  - Run & Analyze end-to-end test (end-to-end 테스트 실행 및 분석)
  - Node end-to-end tests (노드 end-to-end 테스트)
  
- **Troubleshooting (문제 해결)**
  - Application Failure (애플리케이션 실패)
  - Control Plane Failure (제어 평면 실패)
  - Worker Node Failure (워커 노드 실패)
  - Networking (네트워킹)