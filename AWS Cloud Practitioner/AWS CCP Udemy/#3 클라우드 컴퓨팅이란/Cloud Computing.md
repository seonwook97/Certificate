# Cloud Computing

1. [기존 IT 개요](#1-기존-IT-개요)
2. [클라우드 컴퓨팅이란](#2-클라우드-컴퓨팅이란)
3. [다양한 유형의 클라우드 컴퓨팅](#3-다양한-유형의-클라우드-컴퓨팅)
4. [AWS 클라우드 개요](#4-AWS-클라우드-개요)
5. [AWS의 콘솔 및 서비스 둘러보기](#5-AWS의-콘솔-및-서비스-둘러보기)
6. [공동 책임 모델 및 AWS 허용 정책](#6-공동-책임-모델-및-AWS-허용-정책)

---

## 1. 기존 IT 개요

### 웹 사이트 동작
- 클라이언트 : IP주소들을 가지고 있음
- 네트워크
- 서버 : IP주소들을 가지고 있음

![image](https://github.com/seonwook97/Certificate/assets/92377162/3aaa12d4-4622-426e-b0b7-b1d113657448)

### 서버 구성
- Compute : CPU
- Memory : RAM
- Storage : Data
- Database : Store data in a structured way
- Network : Routers, swtich, DNS server

### IT 용어
- Network: 네트워크는 서로 연결될 케이블과 라우터, 서버의 묶음
- Router: 컴퓨터 네트워크 간의 데이터 패킷을 전달하는 특정기기, 인터넷에서 패킷을 어디로 보낼지 파악
- Switch: 패킷을 네트워크의 정확한 클라이언트에게 보냄
  
  ![image](https://github.com/seonwook97/Certificate/assets/92377162/acd6b247-6f08-43b5-91e5-c20393253a26)
  - 클라이언트가 데이터를 라우터에 보내면 
  - 라우터는 스위치에 도달하는 방법을 찾고 네트워크에 있는 어떤 컴퓨터로 데이터를 보낼지 파악

### 전통적 IT인프라 구성
- 서버를 사서 집에 서버 설치 -> 웹사이트가 커지면 더 많은 서버가 필요함 -> 데이터 센터에서 더 많은 서버를 추가하거나 구매해서 확장

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/6ea55112-692e-46b5-a202-f0a2802d6558)

#### 이에 따른 문제
- 집에 서버를 보관하면 임대료 지불
- 전원장치 추가, 쿨링 및 유지보수
- 서버를 추가하거나 교체하기 위한 시간이 오래 소모(서버 주문, 데이터 센터 서버 연결)
- 규모를 10배 확장하려면 10배 많은 서버가 필요 
- 문제 발생에 대비해 인프라를 24시간으로 매일 모니터링 할 팀도 있어야 함
- 재난 발생
- 모든 것을 외부화? -> **클라우드!**

---

## 2. 클라우드 컴퓨팅이란
- 컴퓨팅 성능, 데이터베이스 스토리지, 애플리케이션, 다른 IT 리소스를 **온디맨드로 제공**하는 것 -> 필요할 때 바로 얻는 것
- 클라우드 서비스 플랫폼으로 종량제 요금을 이용할 수 있음 -> 요청한만큼만 비용을 지불
- 필요한 컴퓨팅 리소스의 정확한 유형과 크기를 프로비저닝 할 수 있음
  - 프로비저닝 : IT 인프라를 생성하고 설정하는 프로세스     
- 모든 리소스에 바로 접근할 수 있음
- 인터페이스가 단순하여 서버, 스토리지, 데이터베이스, 애플리케이션 서비스에 쉽게 접근할 수 있음
- 특정 AWS는 웹 애플리케이션을 통해 필요한 것을 프로비저닝하고 사용하는 동안 이런 애플리케이션 서비스를 위한 네트워크로 연결된 하드웨어를 소유하며 유지하고 있음

### 클라우드 서비스

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/0e3e7f2d-470d-46f3-90bd-cf2dfb46b74a)

### 클라우드 서비스의 전개

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/b964ffac-5cbd-421e-a1eb-0470a6a97570)

### 클라우드 컴퓨팅의 5가지 특징
- **On-demand self service: 완전한 온디맨드이며 셀프서비스**
  - 사용자는 리소스를 프로비저닝 할 수 있고 AWS의 개입없이 사용할 수 있음
- **Broad network access: 광역 네트워크에 접근할 수 있음**
  - 네트워크를 통해 리소스를 사용할 수 있고 다양한 방법으로 접근가능
- **Multi-tenancy and resource pooling: 멀티 테넌시가 되며 리소스 풀링이 가능**
  - 자신뿐만 아니라 AWS의 다른 고객도 동일한 인프라와 애플리케이션을 공유하면서도 보안과 프라이버시를 유지할 수 있음
  - 많은 고객은 동일한 물리적 리소스로 서비스를 받게 됨 -> 모든 사용자들이 클라우드의 전체 데이터 센터를 공유하는 것과 같음
  - 멀티 테넌시 : 단일 소프트웨어 인스턴스로 서로 다른 여러 사용자 그룹에 서비스를 제공할 수 있는 소프트웨어 아키텍처, SaaS가 멀티테넌트 아키텍처의 예시
  - 리소스 풀링 : 서버나 스토리지 등의 자원을 미리 확보하고 이를 사용자 요청에 따라 제공한다는 개념 혹은 이를 확보해놓은 가상적인 공간
- **Rapid elasticity and scalability: 빠른 탄력성과 확장성 제공**
  - 필요할 때 자동으로 신속하게 원하는 리소스를 획득하고 처리할 수 있음
  - 온디맨드 기반으로 쉽고 빠르게 확장할 수 있음
- **Measured service: 측정 가능한 서비스**
  - 사용량을 측정해서 정확히 사용한 만큼 지불하는 것 -> 온프레미스에서 가장 크게 바뀐 점!

### 클라우드 컴퓨팅의 6가지 장점
- **Trade CAPEX to OPEX: 자본적 지출을 업무 지출로 교환할 수 있음**
  - 하드웨어를 소유하지 않고 온디맨드로 지불하는 것 -> 하드웨어를 구매하지않고 AWS에서 임대
  - 총 소유 비용인 TCO와 업무 지출(OPEX)을 절감할 수 있음
- **Benefit from massive economies of scale: 거대한 규모의 경제로부터 혜택을 얻을 수 있음**
  - 시간이 지남에 따라 AWS 가격이 인하됨 -> AWS는 규모가 크기 때문에 실행하는데 효과적
- **Stop guessing capacity: 용량을 짐작할 필요가 없음**
  - 애플리케이션의 실제 측정된 사용량을 기반으로 자동 확장 가능
- **Increase speed and agility: 속도와 민첩성향상(온디맨드)**
- **Stop spending money running and maintaining data centers: 데이터 센터의 운영 및 관리하는 막대한 비용을 지불하지 않아도 됨**
- **Go global in minutes: leverage the AWS global infrastructure**

### 클라우드를 사용해 해결할 수 있는 문제
- Flexibility: change resource types when needed
- Cost-Effectiveness: pay as you go, for what you use
- Scalability: accommodate larger loads by making hardware stronger or adding additional nodes
- Elasticity: ability to scale out and scale-in when needed
- High-availability and fault-tolerance: build across data centers
- Agility: rapidly develop, test and launch software applications

---

## 3. 다양한 유형의 클라우드 컴퓨팅
- IaaS(Infrastructure as a Service)
  - 클라우드 IT에 관한 구성 요소 제공: 네트워킹, 컴퓨터 또는 데이터 스토리지 공간을 원시형태로 제공
  - 높은 유연성
  - 기존 온프레미스와 쉬운 병렬
- PaaS(Platform as a Service
  - 기본 인프라를 관리할 필요가 없음
  - 배포와 애플리케이션 관리만 집중할 수 있음
- SaaS(Software as a Service)
  - 서비스 제공업체가 완전히 운영하고 관리

![image](https://github.com/seonwook97/Certificate/assets/92377162/7c859636-7d59-4c19-a2ca-427a61ba2c41)

### 클라우드 컴퓨팅 타입 예시
- Infrastructure as a Service:
  - Amazon EC2 (on AWS)
  - GCP, Azure, Rackspace, Digital Ocean, Linode
- Platform as a Service:
  - Elastic Beanstalk (on AWS)
  - Heroku, Google App Engine (GCP), Windows Azure (Microsoft)
- Software as a Service:
  - Many AWS services (ex: Rekognition for Machine Learning)
  - Google Apps (Gmail), Dropbox, Zoom

### 클라우드 가격책정 요약
- AWS는 3가지의 기본 가격이 있음(종량 과금제)
  - Compute: 컴퓨팅 시간에 따라 지불
  
    ![image](https://github.com/seonwook97/Certificate/assets/92377162/335ec4c9-2b74-431a-b6e6-10a80cf878af)
  
  - Storage: 저장한 양만큼 지불
  
    ![image](https://github.com/seonwook97/Certificate/assets/92377162/92c8f177-fb04-4233-aeee-13ed18896cfa)
  
  - Data transfer OUT of the Cloud(클라우드에 들어오는 모든 데이터는 무료)
    
    ![image](https://github.com/seonwook97/Certificate/assets/92377162/20fcfb28-5d6a-4592-9218-bff1c730f744)

---

## 4. AWS 클라우드 개요

### AWS 역사

![image](https://github.com/seonwook97/Certificate/assets/92377162/22d03af7-14e3-468a-ba1b-32f74e2b341a)

### AWS Global Infrastructure
- AWS Regions
- AWS Availability Zones
- AWS Data Centers
- AWS Edge Locations / Points of Presence
- https://infrastructure.aws/

### AWS Regions
- AWS has Regions all around the world
- Names can be us-east-1, eu-west-3…
- A region is a cluster of data centers
- Most AWS services are region-scoped

#### How to choose an AWS Region -> AWS 리전을 어떻게 선택하는지 출제 가능
- **Compliance with data governance and legal requirements(법률준수)**: data never leaves a region without your explicit permission
- **Proximity to customers(지연시간을 줄여야)**: reduced latency
- **Available services within a Region(해당 리전에 해당서비스가 있는지)**: new services and new features aren’t available in every Region
- **Pricing(리전마다 요금이 다름)**: pricing varies region to region and is transparent in the service pricing page

### AWS Availability Zones
- 가용영역은 리전 내 존재
- 보통은 3개씩, 최소 2개 ~ 최대 6개
- 시드니 리전: ap-southeast-2 -> 3개의 가용영역
  - ap-southeast-2a
  - ap-southeast-2b
  - ap-southeast-2c
- 각각의 가용 영역은 여분의 전원 네트워킹, 통신기능을 갖춘 하나 또는 두 개의 개별적인 데이터 센터로 구성
  - southeast-2a 내에 두 개의 데이터센터, 2b에도 두 개, 2c에도 두 개가 있을 수 있음(1개, 3개, 4개도 가능 AWS가 공개하지 않아 정확히는 알 수 없음)
- 각각의 가용 영역들이 재난 발생에 대비해 서로 분리되어 있음 -> 2a가 불이나도 2b, 2c에는 영향이 가지 않음
- 가용 영역들은 높은 대역폭의 초저지연 네트워킹으로 서로 연결되어 리전을 형성

### AWS Points of Presence (Edge Locations)
- AWS는 42개국 84개의 도시에 200개가 넘는 전송 지점을 가지고 있음
- 이런 점으로 인해 최소 지연 시간으로 최종 사용자에게 컨텐츠를 전달하는 데에 아주 유용
- https://aws.amazon.com/cloudfront/features/

![image](https://github.com/seonwook97/Certificate/assets/92377162/83552d2d-7237-4922-ba63-4dbebac8df05)

---

## 5. AWS의 콘솔 및 서비스 둘러보기

### AWS Console
- AWS Global Services
  - Identity and Access Management (IAM)
  - Route 53 (DNS service)
  - CloudFront (Content Delivery Network)
  - WAF (Web Application Firewall)
- Most AWS services are Region-scoped:
  - Amazon EC2 (Infrastructure as a Service)
  - Elastic Beanstalk (Platform as a Service)
  - Lambda (Function as a Service)
  - Rekognition (Software as a Service)
- 리전별 AWS 서비스: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services

---

## 6. 공동 책임 모델 및 AWS 허용 정책

### Shared Responsibility Model(공동 책임 모델)
![image](https://github.com/seonwook97/Certificate/assets/92377162/27f50aec-b1e7-45a6-860a-c81a687ff4b2)
- 고객
  - 고객으로서 클라우의 내의 보안 책임 -> 클라우드에서 무엇을 사용하고 어떻게 구성하든 모든 책임은 고객
  - 보안, 데이터, 운영체제, 네트워크 방화벽 구성 등
- AWS
  - 클라우드에 관한 보안 책임이 있음
  - 모든 인프라, 하드웨어, 소프트웨어, 자체 내부 보안 등
- CCP에서 **AWS의 책임, 고객의 책임**에 대한 문제가 출제
- https://aws.amazon.com/compliance/shared-responsibility-model/

### AWS Acceptable Use Policy(이용 목적 제한 방침 동의)
- https://aws.amazon.com/aup/
- No Illegal, Harmful, or Offensive Use or Content
- No Security Violations
- No Network Abuse
- No E-Mail or Other Message Abuse
