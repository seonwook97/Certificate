# EC2 - Elastic 컴퓨팅 클라우드

1. [EC2 기초](#1-EC2-기초)
2. [EC2 인스턴스 유형 기본 사항](#2-EC2-인스턴스-유형-기본-사항)
3. [보안 그룹 및 클래식 포트 개요](#3-보안-그룹-및-클래식-포트-개요)
4. [SSH 개요](#4-ssh-개요)
5. [SSH 문제 해결](#5-ssh-문제-해결)
6. [EC2 인스턴스 구매 옵션](#6-ec2-인스턴스-구매-옵션)
7. [EC2 요약 1](#7-ec2-요약-1)
8. [EC2 요약 2](#8-ec2-요약-2)

---

## 1. EC2 기초
- EC2 is one of the most popular of AWS’ offering
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- It mainly consists in the capability of :
  - Renting virtual machines (EC2)
  - Storing data on virtual drives (EBS)
  - Distributing load across machines (ELB)
  - Scaling the services using an auto-scaling group (ASG)
- AWS EC2의 사용법을 아는 것은 클라우드 작동 방식을 이해할 때 필수적
  - 클라우드는 필요할 때마다 언제든지 컴퓨팅을 대여할 수 있고 EC2가 그 예시

### EC2 sizing & configuration options
- AWS에서 임대하는 가상 서버인 EC2에서 어떤 것을 선택할 수 있을까?
- EC2 인스턴스의 운영 체제로 어떤 것을 선택할 수 있을까?
- Operating System (OS): Linux, Windows or Mac OS
- How much compute power & cores (CPU)
- How much random-access memory (RAM)
- How much storage space:
  - Network-attached (EBS & EFS)
  - hardware (EC2 Instance Store)
- Network card: speed of the card, Public IP address
- Firewall rules: security group
- Bootstrap script (configure at first launch): EC2 User Data
- 내가 원하는대로 가상 머신을 선택하여 AWS에서 빌릴 수 있음

### EC2 User Data
- EC2 사용자 데이터 스크립트를 사용하여 인스턴스를 부트스트래핑할 수 있음
- 부트스트래핑: 머신이 작동될 때 명령을 시작하는 것
- 스크립트는 처음 시작할 때 한번만 실행되고 다시 실행되지 않음
- EC2 사용자 데이터에는 매우 특정한 목적이 있는데 부팅 작업을 자동화하기 때문에 부트스트래핑이라는 이름을 갖게 됨
- 인스턴스를 부팅할 때 자동화하고 싶은 작업 -> 사용자 데이터 스크립트에 작업을 더 추가할수록 부팅 시 인스턴스가 할 일이 늘어남
  - Installing updates
  - Installing software
  - Downloading common files from the internet
  - Anything you can think of
- EC2 사용자 데이터 스크립트는 루트 계정에서 실행됨 -> 모든 명령문은 sudo

###  EC2 Instance Types: example

![image](https://github.com/seonwook97/Certificate/assets/92377162/c2449066-57d1-44ff-a517-e6d168a3b6c6)
- https://instances.vantage.sh

---

## 2. EC2 인스턴스 유형 기본 사항
- You can use different types of EC2 instances that are optimised for different use cases (https://aws.amazon.com/ec2/instance-types/)
- AWS has the following naming convention:

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/523eddaa-8cd2-4114-a332-afb64c578c25)
  - 크기가 클수록 인스턴스에 더 많은 메모리와 CPU를 가지게 됨

### EC2 Instance Types - General Purpose
- 범용의 인스턴스는 웹 서버나 코드 저장소와 같은 다양한 작업에 적합
- Balance between:
  - Compute
  - Memory
  - Networking
- 강의에서는 범용 인스턴스의 프리티어인 t2.micro 사용

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/6baf4541-f2f0-464d-bd84-5f4db80e814b)

### EC2 Instance Types - Compute Optimized
- 컴퓨팅 최적화 인스턴스는 컴퓨터 집약적인 작업에 최적화된 인스턴스
- 고성능 프로세서는 어디에 사용?
  - Batch processing workloads - 일부 데이터의 일괄 처리
  - Media transcoding - 미디어 트랜스코딩 작업
  - High performance web servers - 고성능 웹 서버 필요 시
  - High performance computing (HPC) - 고성능 컴퓨팅이라는 HPC 작업을 할 때
  - Scientific modeling & machine learning - 머신러닝
  - Dedicated gaming servers - 전용 게임 서버      

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/04f25d11-7a8c-4f9f-b688-8842c2ae1dc6)

### EC2 Instance Types - Memory Optimized
- 메모리(RAM)에서 대규모 데이터셋을 처리하는 유형의 작업에 바른 성능을 제공
- 사용사례:
  - 대부분 인메모리 DB가 되는 고성능의 관계형 또는 비관계형의 DB에 사용
  - 일래스틱 캐시를 예로 들 수 있는 분산 웹스케일 캐시 저장소에도 사용
  - BI에 최적화된 인 메모리 DB와 대규모 비정형 데이터의 실시간 처리를 실행하는 애플리케이션에도 사용
  - 메모리 최적화 인스턴스의 이름을 보면 R로 시작(X1, Z1도 있음)

    ![image](https://github.com/seonwook97/Certificate/assets/92377162/46cc1eee-69b3-444d-9440-30d1d8eb95b5)

### EC2 Instance Types - Storage Optimized
- 로컬 스토리지에서 대규모의 데이터셋에 액세스할 때 적합한 인스턴스
- 스토리지 최적화 인스턴스의 사용 사례:
  - 고주파 온라인 트랜잭션 처리인 OLTP 시스템에 사용
  - 관계형과 비관계형인 NoSQL 데이터베이스에 사용
  - 레디스와 같은 메모리 데이터베이스의 캐시
  - 데이터 웨어하우징 애플리케이션
  - 분산 파일 시스템에 사용
- AWS의 스토리 최적화 인스턴스는 이름이 I, G 또는 H1으로 시작

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/257652c6-86ac-487f-9713-5e1eea2672fc)

- 작은 메모리나 많은 CPU 등 네트워크 성능에 따라 EBS 대역폭 등이 달라짐

---

## 3. 보안 그룹 및 클래식 포트 개요

### Introduction to Security Groups
- AWS 클라우드에서 네트워크 보안을 실행하는 핵심
- EC2 인스턴스에 들어오고 나가는 트래픽을 제어
- 보안 그룹은 **허용** 규칙만 포함
- IP 주소를 참조해 규칙을 만들 수 있음
  - 컴퓨터의 위치나 다른 보안 그룹을 참조하는 것
  - 보안 그룹끼리 서로 참조할 수도 있음

- 컴퓨터에서 공공 인터넷을 사용해 EC2 인스턴스에 액세스하려고 할 경우 EC2 인스턴스 주변에 보안 그룹을 생성해야 함 
  - 방화벽(보안 그룹은 규칙을 가지게 됨) -> 인바운드 트래픽의 여부
  - 외부에서 EC2 인스턴스로 들어오는 것이 허용되면 아웃바운드 트래픽도 수행할 수 있는 것
    - 인바운드 트래픽: 외부에서 가상서버 내부로 데이터가 유입될 때 발생하는 트래픽
    - 아웃바운드 트래픽: 가상서버 내에서 외부로 데이터가 전송되었을 때의 트래픽

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/c54b2fa2-f647-44a9-98d6-648f718a1211)

### Security Groups Deeper Dive
- 보안 그룹은 EC2 인스턴스의 방화벽
- 포트로의 액세스를 통제
- 인증된 IP 주소의 범위를 확인해 IPv4인지 IPv6인지 확인(인터넷 IP의 2가지 종류)
- 외부에서 인스턴스로 들어오는 인바운드 네트워크도 통제
- 인스턴스에서 외부로 나가는 아웃바은드 네트워크도 통제
- 보안 그룹 규칙

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/b1d579d6-d298-495f-bd41-8a93975b70d7)

  - Type: 유형을 확인할 수 있음
  - Protocol: TCP
  - Port Range: 트래픽이 인스턴스에서 통과하는 위치
  - Source: IP 주소의 범위
    - 0.0.0.0/0는 전체 IP
    - 122.149.196.86/32 -> 하나의 IP

### Security Groups Good to know
- 여러 인스턴스에 연결할 수 있음, 보안 그룹과 인스턴스 간의 일대일 관계 X, 인스턴스에 여러 보안 그룹을 연결할 수 있음
- 보안 그룹은 지역과 VPC 결합으로 통제되어 있음 -> 지역을 전환하면 새 보안 그룹을 생성하거나 다른 VPC를 생성해야 함
- 보안 그룹은 EC2 외부에 존재 -> 트래픽이 차단되면 EC2 인스턴스 확인 
- SSH 액세스를 위해 하나의 별도 보안 그룹을 유지하는 것이 좋음
- 타임아웃으로 애플리케이션에 접근할 수 없으면 보안 그룹 문제, 어떤 포트에 연결을 시도하는데 컴퓨터가 계속 멈추고 대기하기만 해도 보안 그룹 문제
- 연결 거부 오류가 발생하면 보안 그룹은 실행됐고 트래픽은 통과했지만 애플리케이션이 실행되지 않는 등 문제가 발생한 것
- 기본적으로 모든 인바운드 트래픽은 차단되어 있음
- 모든 아웃바운드 트래픽은 허용됨

### Referencing other security groups Diagram

![image](https://github.com/seonwook97/Certificate/assets/92377162/dfc24383-b93e-4502-8962-8e4870f8c067) 

- 기본적인 인바운드 규칙은 보안 그룹 1의 인바운드를 보안 그룹 2에 허용하는 것
  - 다른 EC2 인스턴스를 생성하고 보안 그룹 2를 연결한 경우 방금 설정한 보안 그룹 규칙으로 첫 번째 EC2 인스턴스로 정한 포트를 통해서 EC2 인스턴스가 바로 연결되도록 허용함
  - 마찬가지로 보안 그룹 1에 연결된 다른 EC2 인스턴스가 있다면 이 인스턴스도 우리의 인스턴스와 바로 통신하도록 허용함
  - EC2 인스턴스의 IP와는 상관없음, 올바른 보안 그룹에 연결되어 있기 때문에 다른 인스턴스를 통해서 바로 통신할 수 있는 것
  - IP는 신경 쓰지 않아도 되는 점이 좋음
  - 또 다른 EC2 인스턴스는 보안 그룹 3에 연결되어 있을 것, 보안 그룹 1의 인바운드 규칙으로 보안 그룹 3과 연결되어 있지 않아서 거부되고 실행되지 않기 때문

### Classic Ports to know
- SSH: 포트는 22번 포트로 Linux EC2 인스턴스로 로그인하도록 함
- FTP: 포트는 21번 포트로 파일 공유 시스템에 파일을 업로드하는데 사용됨
- SFTP: 22번 포트를 사용, SSH를 사용해서 업로드 하기 때문이고 보안 파일 전송 프로토콜이 되기 때문
- HTTP: 80번 포트를 사용, 보안이 되지 않은 사이트에 액세스하기 위한 것
- HTTPS: 443번 포트를 사용, 보안 사이트에 액세스 현재 표준 
- RDP(Remote Desktop Protocol): 3389 포트를 사용, 윈도우 인스턴스에 로그인할 때 사용

---

## 4. SSH 개요

### SSH Summary Table
- 명령줄 인터페이스 도구 Mac과 Linux에서 사용할 수 있고 Windows10 이상의 버전에서 사용할 수 있음
- Windows 10이하의 버전은 Putty 사용
- SSH, Putty 모두 SSH 프로토콜을 사용해 EC2 인스턴스에 연결하도록 함
- EC2 Instance Connect는 웹 브라우저에 사용, 모든 버전의 Mac, Linux, Windows에서 사용 가능
  - Amazon Linux2에서만 작동

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/e09e5d08-649a-42fe-9b83-52267e2c49c7)

---

## 5. SSH 문제 해결
- 연결 타임아웃 이슈가 있습니다.
  - 이 부분은 보안 그룹 문제입니다. 모든 타임아웃 (SSH 뿐만 아니라)은 보안 그룹 또는 방화벽과 관련된 문제 입니다. 보안 그룹이 다음과 같이 표시되고 EC2 인스턴스에 올바르게 할당되었는지 확인하세요.

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/6fd90ad7-ae7e-4d77-bad3-ae26c5afbe82)

- 여전히 연결 타임아웃 이슈가 있습니다.
  - 보안 그룹이 위와 같이 올바르게 구성되어 있음에도 불구하고 지속적으로 연결 타임아웃 이슈가 발생한다면 회사 방화벽이나 개인 방화벽이 연결을 차단하고 있음을 의미합니다. 

- SSH윈도우에서 작동하지 않습니다.
  - 다음과 같이 표시되는 경우: `ssh command not found`, 즉 Putty를 사용해야 함을 의미합니다.

- 연결이 거부되었습니다.
  - 이는 인스턴스에 연결할 수 있지만 인스턴스에서 실행 중인 SSH 유틸리티가 없음을 의미합니다.
    - 인스턴스 다시 시작 시도
    - 작동하지 않으면 인스턴스를 종료하고 **아마존 리눅스 2**를 사용하여 새 인스턴스를 만드십시오.

- `Permission denied (publickey,gssapi-keyex,gssapi-with-mic)`
  - 이것은 다음 두 가지를 의미합니다.
    - 잘못된 보안 키를 사용하거나 보안 키를 사용하지 않고 있습니다. EC2 인스턴스 구성을 살펴보고 올바른 키를 할당했는지 확인하십시오.
    - 잘못된 사용자를 사용하고 있습니다. **Amazon Linux 2 EC2 인스턴스**를 시작했는지 확인하고, **ec2 사용자**를 사용하고 있는지 확인하세요. 이것은 SSH 명령 또는 Putty 구성에서 **ec2-user@**`<public-ip>` (ex: `ec2-user@35.180.242.162`) 를 실행할 때 지정하는 것입니다.

- 아무것도 작동하지 않습니다 
  - Amazon Linux 2를 시작했는지 확인하면 튜토리얼을 따라오실 수 있습니다.

- 어제는 접속이 가능했는데 오늘은 안 되네요.
  - 이는 EC2 인스턴스를 중지했다가 오늘 다시 시작했기 때문일 수 있습니다. 그렇게 하면 EC2 인스턴스의 퍼블릭 IP가 변경됩니다. 따라서 명령 또는 Putty 구성에서 새 공용 IP를 편집하고 저장해야 합니다.

---

## 6. EC2 인스턴스 구매 옵션

### EC2 인스턴스 구매 옵션
- 온디맨드 인스턴스 – 짧은 워크로드, 예측 가능한 가격, 초당 지불
- 예약(1년 및 3년)
  - 예약된 인스턴스 – 긴 워크로드
  - 전환 가능한 예약 인스턴스 – 유연한 인스턴스를 통해 긴 워크로드 지원
- 절약 계획(1년 및 3년) – 사용량과 긴 워크로드에 대한 헌신
- 스폿 인스턴스 – 짧은 워크로드, 저렴한 워크로드, 인스턴스 손실(신뢰성 저하)
- 전용 호스트 – 전체 물리적 서버 예약, 인스턴스 배치 제어
- 전용 인스턴스 – 다른 고객이 하드웨어를 공유하지 않음
- 용량 예약 – 특정 AZ에서 모든 기간 동안 용량 예약

### EC2 온디맨드
- 사용 비용 지불:
  - Linux 또는 Windows - 1분 후 초당 과금
  - 기타 모든 운영 체제 - 시간당 과금
- 비용은 가장 높지만 선불은 없습니다
- 장기적인 약속 없음
- 애플리케이션 작동 방식을 예측할 수 없는 단기 및 무중단 워크로드에 권장

### EC2 예약 인스턴스
- 온디맨드 대비 최대 72% 할인
- 특정 인스턴스 특성(인스턴스 유형, 지역, 테넌트, OS)을 예약합니다
- 예약 기간 – 1년(+할인) 또는 3년(++할인)
- 지불 옵션 – 선불 없음(+), 부분 선불(+), 모두 선불(++)
- 예약 인스턴스의 범위 – 지역 또는 지역(예약)eAZ의 용량)
- 정상 상태 사용 애플리케이션(think 데이터베이스)에 권장
- 예약 인스턴스 마켓플레이스에서 구매 및 판매할 수 있습니다
- 변환 가능한 예약 인스턴스
  - EC2 인스턴스 유형, 인스턴스 패밀리, OS, 범위 및 테넌트를 변경할 수 있습니다
  - 최대 66% 할인

### EC2 저축 계획
- 장기 사용량을 기준으로 할인 적용(최대 72% - RI와 동일)
- 특정 유형의 사용(1년 또는 3년 동안 시간당 10달러)을 약속합니다
- EC2 절감 플랜을 초과하는 사용량은 온디맨드 가격으로 청구됩니다
- 특정 인스턴스 패밀리 및 AWS 영역(예: us-east-1의 M5)에 잠금
- 유연한 전체 환경:
  - 인스턴스 크기(예: m5.xlarge, m)5.2배 큼)
  - OS(예: Linux, Windows)
  - 테넌트(호스트, 전용, 기본)

### EC2 스폿 인스턴스
- On-Demand 대비 최대 90%
- 최대 가격이 현재 현물 가격보다 낮은 경우 언제든지 "손실"할 수 있는 인스턴스
- AWS에서 가장 비용 효율적인 인스턴스
- 장애에 대한 탄력적인 워크로드에 유용
  - 배치 작업
  - 데이터 분석
  - 이미지 처리
  - 임의의 분산 workloads
  - 시작 및 종료 시간이 유연한 워크로드
- 중요 작업 또는 데이터베이스에 적합하지 않음

### EC2 전용 호스트
- 사용자 전용 EC2 인스턴스 용량을 갖춘 물리적 서버
- 규정 준수 요구사항을 해결하고 기존 서버 바인딩 소프트웨어 라이센스(소켓별, 코어별, PE-VM 소프트웨어 라이센스)를 사용할 수 있습니다
- 구매 옵션:
- 온디맨드 – 활성 전용 호스트에 대해 초당 지불
- 예약 - 1년 또는 3년(없음) 선불, 부분 선불, 모두 선불)
- 가장 비싼 옵션
- 라이센스 모델이 복잡한 소프트웨어에 유용합니다(BYOL – BYOL 자체 라이센스 가져오기)
- 또는 강력한 규제 또는 규정 준수 요구가 있는 기업의 경우

### EC2 전용 인스턴스
- 사용자 전용 하드웨어에서 인스턴스 실행
- 동일한 계정의 다른 인스턴스와 하드웨어를 공유할 수 있음
- 인스턴스 배치를 제어할 수 없음(중지/시작 후 하드웨어 이동 가능)
  
![image](https://github.com/seonwook97/Certificate/assets/92377162/92668b9e-2b93-42ec-b02a-95da436d5050)

### EC2 용량 예약
- 특정 AZ에서 일정 기간 동안 온디맨드 인스턴스 용량 예약
- 필요할 때 항상 EC2 용량에 액세스할 수 있습니다
- 시간 약속 없음(언제든지 만들기/취소), 청구 할인 없음
- 지역 예약 인스턴스 및 절감 계획과 결합하여 청구 할인 혜택을 누릴 수 있습니다
- 당신은 On-Dema에서 청구됩니다인스턴스 실행 여부를 평가합니다
- 특정 AZ에 있어야 하는 중단 없는 단기 워크로드에 적합

### 나에게 적합한 구매 옵션은 무엇입니까
- 온 디맨드: 언제든지 리조트에 와서 머무르며, 우리는 모든 가격을 지불합니다
- 예약: 미리 계획을 세우는 것과 같이, 만약 우리가 오랫동안 머물 계획이라면, 우리는 좋은 할인을 받을 수 있습니다.
- 절약 플랜: 특정 기간 동안 시간당 일정 금액을 지불하고 모든 객실 유형(예: 킹, 스위트, 씨뷰 등)에서 숙박합니다
- 현장 사례: 호텔은 빈 객실에 대한 입찰을 허용하고 가장 높은 입찰자가 객실을 유지합니다. 당신은 언제든지 쫓겨날 수 있습니다
- 전용 호스트: 리조트의 전체 건물을 예약합니다
- 용량 예약: 숙박하지 않더라도 일정 기간 동안 정가로 방을 예약합니다

### 가격 비교 예 – m4.large – us-east-1

![image](https://github.com/seonwook97/Certificate/assets/92377162/6eb452ec-2e90-4fc6-ab4d-7944681cf9af)

---

## 7. EC2 요약 1

### Shared Responsibility Model for EC2

- AWS
  - 모든 데이터 센터와 인프라에 관한 보안 책임이 있음
  - 사용자가 물리적 호스트와 분리된 상태인지 확인하는 책임이 있음
  - 서버 장애로 결함 있는 하드웨어를 교체하거나 동의한 규정을 준수하고 있는지 확인해야 하는 책임이 있음

- 사용자
  - 클라우드 내의 보안을 책임, 자체 보안 그룹 규칙을 정의 -> EC2 인스턴스에 사용자 또는 다른 사용자의 액세스를 허용하는 것
  - EC2 인스턴스 내부에 전체 가상 머신을 소유 -> 운영체제가 Windows나 Linux임을 의미하며 모든 패치와 업데이트를 AWS가 아니라 사용자가 해야 함, AWS는 가상 머신만 제공
  - EC2 인스턴스에 모든 소프트웨어와 유틸리티가 설치되어 있음 -> 사용 방법은 사용자 책임
  - IAM 역할의 할당 방법을 이해하고 권한이 올바른지 확인해야 함
  - 인스턴스의 데이터가 안전한지 확인하는 것도 매우 중요한 책임

---

## 8. EC2 요약 2

### EC2 Section - Summary
- **EC2 Instance**: AMI (OS) + Instance Size (CPU + RAM) + Storage + security groups + EC2 User Data
- **Security Groups**: Firewall attached to the EC2 instance
- **EC2 User Data**: Script launched at the first start of an instance
- **SSH**: start a terminal into our EC2 Instances (port 22)
- **EC2 Instance Role**: link to IAM roles
- **Purchasing Options**: On-Demand, Spot, Reserved (Standard + Convertible + Scheduled), Dedicated Host, Dedicated Instance
