# IAM - ID 및 액세스 관리

1. [IAM 소개: 사용자, 그룹, 정책](#1-IAM-소개-사용자-그룹-정책)
2. [IAM 정책](#2-IAM-정책)
3. [IAM MFA 개요](#3-IAM-MFA-개요)
4. [AWS 액세스 키, CLI 및 SDK](#4-AWS-액세스-키-CLI-및-SDK)
5. [AWS 서비스에 대한 IAM 역할](#5-AWS-서비스에-대한-IAM-역할)
6. [IAM 보안 도구](#6-IAM-보안-도구)

---

## 1. IAM 소개: 사용자, 그룹, 정책

### IAM: Users & Groups
- IAM(Identity and Access Management), Global service
- 계정을 생성할 때 루트 계정을 만듦 -> 기본적으로 생성되는 것, 계정을 생성할 때만 사용
- 사용자 생성할 때 하나의 사용자는 조진 내의 한 사람에 해당
- 그룹에는 오직 사용자만 배치, 다른 그룹을 포함시킬 수 없음
- 그룹에 포함되지 않을 수 있으며 한 사용자가 다수의 그룹에 속할 수 있음

![image](https://github.com/seonwook97/Certificate/assets/92377162/0acd71e9-232f-4736-bf5c-65b64adeb8d1)

### IAM: Permissions
- 사용자와 그룹을 생성하는 이유? -> AWS 계정을 사용하도록 허가하기 위함
- 사용자 또는 그룹에게 정책, 또는 IAM 정책이라고 불리는 JSON 문서를 지정할 수 있음
  - 특정 사용자, 혹은 특정 그룹에 속한 모든 사용자들이 AWS 서비스의 어떤 작업에 권한을 가지고 있는지를 설명해 놓음
- AWS는 모든 사용자에게 모든 것을 허용하지 않음
  - 새로운 사용자가 너무 많은 서비스를 실행하여 큰 비용이 발생하거나, 보안 문제를 야기
- AWS는 최소 권한의 원칙을 적용 -> 사용자가 꼭 필요로 하는 것 이상의 권한을 주지 않음

![image](https://github.com/seonwook97/Certificate/assets/92377162/0417f110-e304-42ee-871b-822be98daeae)

---

## 2. IAM 정책

### IAM Policies inheritance

![image](https://github.com/seonwook97/Certificate/assets/92377162/abdddf46-e764-43db-8a6f-8499cadc1ed6)

### IAM Policies Structure
- Consists of
  - Version: policy language version, always include “2012-10-17”
  - Id: an identifier for the policy (optional)
  - Statement: one or more individual statements (required)
- Statements consists of
  - Sid: an identifier for the statement (optional)
    - 문장의 ID로 문장의 식별자
  - Effect: whether the statement allows or denies access(Allow, Deny)
    - 문장이 특정 API에 접근하는 걸 허용할지 거부할지에 대한 내용 -> 사진 예시로는 AWS 계정의 루트 계정에 적용
  - Principal: account/user/role to which this policy applied to
    - 특정 정책이 적용될 사용자, 계정, 혹은 역할로 구성
  - Action: list of actions this policy allows or denies
    - effect에 기반해 허용 및 거부되는 API 호출의 목록
  - Resource: list of resources to which the actions applied to
    - 적용될 action의 리소스의 목록 -> 사진 예시로는 버킷 다른 것들도 가능
  - Condition: conditions for when this policy is in effect(optional)
    - Statement가 언제 적용될지 결정함 

![image](https://github.com/seonwook97/Certificate/assets/92377162/e7c8fc54-a0a5-431b-b791-3f0cba93b05e)

---

## 3. IAM MFA 개요

### IAM - Password Policy
- Strong passwords = higher security for your account
- In AWS, you can setup a password policy:
  - Set a minimum password length
  - Require specific character types:
    - including uppercase letters
    - lowercase letters
    - numbers
    - non-alphanumeric characters
- Allow all IAM users to change their own passwords
- Require users to change their password after some time (password expiration)
- Prevent password re-use

### Multi Factor Authentication - MFA(다요소 인증)
- 사용자들은 계정에 접근 권한이 있고 관리자일 경우 구성을 변경하거나 리소스를 삭제하는 등의 작업을 할 수 있음
- 적어도 루트 계정은 무슨 일이 있어도 반드시 보호해야 하며 전체 IAM 사용자들도 보호해야 함
- MFA는 내가 알고 있는 비밀번호와 내가 가지고 있는 보안 장치를 함께 사용하는 것

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/268ab999-c399-48af-961c-590917e6469e)

- MFA 장점
  - 해킹을 당해 비밀번호가 누출된 상황이라고 해도 해커에게는 로그인을 위해 Alice 소유의 물리적 장치가 추가로 필요하기 때문에 계정을 침투받을 가능성이 적음

### MFA devices options in AWS(AWS에서의 MFA 장치 옵션)
- Virtual MFA device
  - Google Authenticator(phone only)
  - Auth(multi-device)
  - 한 개의 기기에 다수의 토큰을 지원
- Universal 2nd Factor(U2F) Security Key
  - 하나의 보안 키에서 여러 루트 계정과 IAM 사용자를 지원
- 그 외

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/6b081528-af92-4f49-8f67-fd939abeaf4e)

---

## 4. AWS 액세스 키, CLI 및 SDK

### AWS에 액세스하는 방법
- 3가지
  - AWS Management Console (protected by password + MFA) - AWS 콘솔
  - AWS Command Line Interface (CLI): protected by access keys - 터미널에서 설정
  - AWS Software Developer Kit (SDK) - for code: protected by access keys - 애플리케이션 코드 내에서 API를 호출하고자 할 때
- 액세스 키 생성
- 관리 콘솔을 통해 생성
- 사용자들이 액세스 키를 직접 관리
- 공유 X
  - Access Key ID ~= username
  - Secret Access Key ~= password

  ![image](https://github.com/seonwook97/Certificate/assets/92377162/9b515dce-8b0c-43d6-b25f-8c814452fe8e)

### AWS CLI
- 명령줄 인터페이스로 AWS 서비스들과 상호작용할 수 있도록 해주는 도구
- CLI를 사용하면 AWS 서비스의 공용 API로 직접 액세스 가능
- 리소스를 관리하는 스크립트를 개발해 일부 작업을 자동화
- 오픈소스: https://github.com/aws/aws-cli
- 관리 콘솔 대신 사용하기도 함

### AWS SDK
- AWS Software Development Kit
- 특정 언어로 된 라이브러리 집합 -> 프로그래밍 언어에 따라 개별 SDK 존재
- AWS 서비스나 API에 프로그래밍을 위한 액세스가 가능하도록 지원
- SDK는 터미널 내에서는 사용하는 것이 아니라 코딩을 통해 애플리케이션 내에 심어두어야 함
  - 앱 내에 자체적으로 AWS SDK가 있는 것
- 강의에서 사용하게 될 AWS CLI는 Boto라는 Python용 AWS SDK에 구축되어 있음

![image](https://github.com/seonwook97/Certificate/assets/92377162/e26d7963-27cd-4674-94b3-20c19a189910)

---

## 5. AWS 서비스에 대한 IAM 역할
- 몇몇의 AWS 서비스는 본인 계정으로 진행해야 함
- AWS 서비스에 권한을 부여하기 위해 IAM 역할을 만들어야 함
  - EC2 인스턴스가 AWS에 있는 어떤 정보에 접근하려고 할 때 IAM 역할을 사용
    
    ![image](https://github.com/seonwook97/Certificate/assets/92377162/713ac71d-58db-4fc5-8498-6c6c48ef9923)

- 몇가지 일반적인 역할
  - EC2 Instance Roles
  - Lambda Function Roles
  - Roles for CloudFormation

---

## 6. IAM 보안 도구
- IAM Credentials Report(account-level): IAM 자격 증명 보고서
  - 보고서는 계정에 있는 사용자와 다양한 자격 증명의 상태를 포함
- IAM Access Advisor(user-level): IAM 액세스 관리자
  - 사용자에게 부여된 서비스 권한과 해당 서비스에 마지막으로 액세스한 시간이 보임 -> 최소 권한의 원칙을 따랐을 때 매우 도움되는 정보
  - 해당 도구를 사용하여 어떤 권한이 사용되지 않는지 볼 수 있음 -> 사용자의 권한을 줄여 최소권한의 원칙을 지킬 수 있음
