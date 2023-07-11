![image](https://github.com/seonwook97/Certificate/assets/92377162/08ec5143-b1fa-4bd7-99f5-cff66973c94b)# IAM - ID 및 액세스 관리

1. [IAM 소개: 사용자, 그룹, 정책](#1-IAM-소개:-사용자,-그룹,-정책)
2. [IAM 정책](#2-IAM-정책)

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
