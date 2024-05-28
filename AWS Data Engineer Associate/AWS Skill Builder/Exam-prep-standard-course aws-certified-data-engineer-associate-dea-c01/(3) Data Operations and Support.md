# (3) 데이터 운영 및 지원

## 3-1. AWS 서비스를 사용하여 데이터 처리 자동화
- 데이터 운영에는 데이터와 시스템 모니터링, 변화와 이상에 대한 자동 경고가 포함
- AWS에서 워크로드를 실행하면 인프라 배포의 모든 측면을 자동화할 수 있음

### 인프라 자동화
- **CloudFormation**: 데이터 파이프라인을 지원하는 인프라를 구축하기 위한 템플릿 파일을 생성할 수 있음
  - S3 버킷 생성
  - EventBridge 규칙 추가: S3 버킷에 파일이 작성될 때를 모니터링하고 Lambda 함수를 실행
  - Amazon SNS 주제 추가: 알림 전송

### 파이프라인 구성 요소
- **Lambda 함수**: 새로운 파일을 검증하고 Step Function 상태 머신 실행
- **AWS Glue 작업**: 파일 처리 및 데이터 카탈로그 업데이트
- **CodePipeline**: 지속적인 통합과 파이프라인 자동화

### 데이터 파이프라인 오케스트레이션
- **Amazon MWAA**: Apache Airflow를 사용하여 복잡한 워크플로우를 오케스트레이션
  - DAGs 정의: 작업의 의존성을 나타내는 그래프
  - 작업 유형: Spark 작업, AWS Glue 작업, AWS Batch 작업 등
- **Step Functions**: 분산 애플리케이션과 마이크로서비스를 워크플로우로 조정하고 시각화
  - 상태 머신 정의: 작업 수행, 결정 내리기, 이벤트 대기 등의 상태로 구성
  - Lambda 함수, AWS Glue 작업, Amazon EMR 클러스터와 통합

### Amazon MWAA 문제 해결
- **CloudWatch Logs**: Apache Airflow DAG 실행 중 발생하는 오류 메시지나 예외 확인
- **Apache Airflow 로그**: 작업 실행 및 내부 프로세스 로그 검토
- **IAM 역할 및 권한 검토**: 관련 서비스(AWS Glue, Amazon S3, Amazon EMR 등)의 IAM 역할과 권한 확인
- **종속성 및 파일 참조 검토**: DAG 및 Python 스크립트의 종속성과 파일 참조 확인

### 데이터 API 관리
- **Lambda**: 서버리스 함수 생성 및 API 요청 처리
- **API Gateway**: 보안, 확장 가능, 관리형 API 엔드포인트 제공
- **AWS SDK**: 다양한 프로그래밍 언어로 외부 API와 상호작용

### 데이터 처리 최적화
- **모니터링 및 로깅**: CloudWatch를 사용하여 API 요청 및 Lambda 함수 모니터링
- **자동 스케일링**: Lambda 함수나 백엔드 리소스의 자동 스케일링 구성
- **캐싱 전략**: API Gateway 캐싱 또는 ElastiCache 사용
- **쓰로틀링 및 속도 제한**: API Gateway에서 쓰로틀링 및 속도 제한 설정
- **오류 처리**: Lambda 함수 내에서 API 실패 시 오류 처리
- **API 통합 보안**: IAM 및 OAuth를 통한 인증 및 권한 부여
- **백업 및 재해 복구 전략**: 백엔드 시스템과 Lambda 함수 코드 및 구성 백업
- **API 버전 관리**: API 변경을 관리하고 하위 호환성 유지

### 데이터 처리 AWS 서비스
- **Amazon EMR**: Spark 클러스터 온디맨드로 실행, 데이터 병렬 처리 및 클러스터 확장
- **Amazon Redshift**: 데이터 웨어하우스에서 데이터 처리 및 분석
- **AWS Glue**: 데이터 준비 및 변환 작업 지원
- **Athena**: SQL 쿼리를 통해 데이터 탐색 및 분석

### 이벤트 및 스케줄러 관리
- **EventBridge**: 이벤트 기반 아키텍처 구현 및 프로세스 자동화
  - 이벤트 규칙 생성 및 이벤트 속성에 따라 이벤트 라우팅
  - CloudWatch와 통합하여 이벤트 모니터링 및 경고 설정

### 예제: Step Functions를 사용한 데이터 파이프라인 오케스트레이션
1. **Lambda 함수 생성**: 파일 확장자를 확인하여 파일 유형 결정
2. **두 번째 Lambda 함수 생성**: 식별된 파일 유형에 따라 파일 처리
3. **Amazon SNS 주제 생성**: 이메일 구독
4. **Step Function 상태 머신 생성**: 두 Lambda 함수와 Amazon SNS 주제 통합
5. **S3 버킷 CloudTrail 데이터 이벤트 설정**: S3 버킷이 CloudTrail 데이터 이벤트를 생성하도록 구성
6. **EventBridge 규칙 생성**: Step Function 상태 머신을 시작하는 규칙 생성

---