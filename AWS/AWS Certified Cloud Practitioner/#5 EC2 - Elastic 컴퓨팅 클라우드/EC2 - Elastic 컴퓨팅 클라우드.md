# EC2 - Elastic 컴퓨팅 클라우드

1. [EC2 기초](#1-EC2-기초)
2. [웹 사이트 실습을 위한 EC2 사용자 데이터로 인스턴스 생성](#2-웹-사이트-실습을-위한-EC2-사용자-데이터로-인스턴스-생성)

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

###  EC2 instance types: example

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


