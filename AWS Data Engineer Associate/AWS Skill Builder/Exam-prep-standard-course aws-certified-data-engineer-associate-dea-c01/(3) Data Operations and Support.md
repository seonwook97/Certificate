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

### Step Functions를 사용한 데이터 파이프라인 오케스트레이션
- **Lambda 함수 생성**: 파일 확장자를 확인하여 파일 유형 결정
- **두 번째 Lambda 함수 생성**: 식별된 파일 유형에 따라 파일 처리
- **Amazon SNS 주제 생성**: 이메일 구독
- **Step Function 상태 머신 생성**: 두 Lambda 함수와 Amazon SNS 주제 통합
- **S3 버킷 CloudTrail 데이터 이벤트 설정**: S3 버킷이 CloudTrail 데이터 이벤트를 생성하도록 구성
- **EventBridge 규칙 생성**: Step Function 상태 머신을 시작하는 규칙 생성

---

## 3-2. AWS 서비스를 사용하여 데이터 분석

### 데이터 조작 작업
- **데이터 집계**: 여러 레코드에서 데이터를 요약하거나 결합하여 단일 값으로 만드는 작업
  - Amazon Redshift, Athena, Amazon OpenSearch Service 사용
  - 예: SQL 집계 함수 사용(sum, average, count)
- **이동 평균**: 지정된 기간 내의 값 집합의 평균을 계산하여 데이터의 변동을 완화
  - Amazon Redshift, Amazon QuickSight 사용
- **그룹화**: 특정 속성이나 필드를 기준으로 데이터를 그룹화하는 작업
  - Amazon Redshift, Athena, QuickSight 사용
- **피벗팅**: 행 데이터를 열로 변환하여 보고 목적으로 데이터 형식 변경
  - Amazon Redshift, QuickSight 사용

### AWS 서비스
- **QuickSight**: 대시보드 생성 및 애드혹 데이터 분석
- **AWS Glue DataBrew**: 시각적 데이터 준비 도구로 코드 작성 없이 데이터 정리 및 정규화
- **Athena**: Amazon S3에 저장된 데이터에 대해 인터랙티브 SQL 쿼리 실행
- **Amazon Redshift**: 표준 SQL 쿼리를 사용하여 대규모 데이터셋 분석
- **Amazon EMR**: Spark와 Hadoop을 사용하여 대량의 데이터 처리
- **AWS Glue**: 데이터 검색, 카탈로그 및 변환
- **AWS Data Pipeline**: 다양한 AWS 서비스 및 온프레미스 데이터 소스 간의 데이터 이동 및 변환 오케스트레이션 및 자동화
- **Lake Formation**: 데이터 레이크에서 여러 소스의 데이터에 접근하고 분석

### 사례 질문
#### 대시보드 및 검색 기능 추가
- **기존 디자인**: 8시간마다 EC2 인스턴스에서 스크립트를 실행하여 Amazon S3에서 데이터를 추출하고 정리한 후 CSV 파일로 변환하여 스프레드시트 형태로 분석
- **솔루션**: 스크립트를 Lambda 함수로 이전하고 Amazon OpenSearch 클러스터에 결과 전송
  - EventBridge를 사용하여 함수 8시간마다 실행
  - OpenSearch를 통해 대시보드 및 실시간 모니터링과 검색 기능 제공

#### 비용 효율적인 IoT 센서 데이터 시각화
- **솔루션**: 트랜지언트 클러스터를 사용하여 데이터 변환 작업 수행 및 QuickSight를 통해 시각적 보고서 제공
  - 트랜지언트 클러스터로 데이터를 매일 집계한 후 자동 종료
  - QuickSight를 사용하여 시각적 보고서 생성

### AWS 데이터베이스 서비스에서 SQL 쿼리 실행
- **Amazon RDS 및 Aurora**: 관계형 데이터베이스에서 SQL 사용
- **DynamoDB**: SQL 호환 쿼리 언어인 PartiQL 지원
- **Amazon DocumentDB**: MongoDB 호환 NoSQL 데이터베이스 서비스로 SQL 유사 쿼리 사용
- **AWS Glue**: SQL 유사 변환 사용
- **Athena**: Amazon S3의 데이터에 SQL 쿼리 실행

### Athena에서 Spark를 사용한 데이터 분석
- **설정**: Amazon EMR 클러스터에 Spark 설정 후 S3에서 데이터 로드하여 상호작용식으로 데이터 분석
- **Jupyter Notebook**: Spark 코드 작성 및 실행을 위한 인터페이스 제공

### 데이터 검증 및 정리
- **사용 가능한 서비스**: Lambda, Athena, QuickSight, Jupyter Notebook, Amazon SageMaker Data Wrangler
- **목적에 따른 서비스 사용**: 
  - Lambda로 맞춤 데이터 검증 및 보강
  - Athena로 SQL 기반 데이터 검증
  - QuickSight로 데이터 시각화 및 탐색
  - Jupyter Notebook으로 복잡한 데이터 정리 작업
  - SageMaker Data Wrangler로 기계 학습 모델을 위한 데이터 준비

---

## 3-3. 데이터 파이프라인 유지 및 모니터링

### 데이터 측면 질문
- 데이터를 쿼리할 때 입력과 출력이 올바른지 어떻게 확인하는지
- 테이블에 쿼리를 저장할 때 스키마가 올바른지 어떻게 알 수 있는지
- 입력 데이터셋과 변환 데이터셋에 대해 데이터 품질 테스트를 실행하는 이유는 무엇인지
- 변환 단계에서 데이터 품질 문제가 발생하면 문제를 플래그하고, 변경 사항을 롤백하며, 근본 원인을 조사할 수 있어야 함

### 운영 측면 질문
- 시스템 성능을 어떻게 보장할 수 있는지
- 모니터링해야 할 메트릭은 무엇인지
  - 쿼리 대기열 길이
  - 쿼리 동시성
  - 메모리 사용량
  - 스토리지 활용도
  - 네트워크 지연 시간 
  - 디스크 입출력 

### AWS 모니터링 및 가시성 서비스
- **CloudWatch**: 리소스 및 애플리케이션 모니터링
- **CloudWatch Logs**: 로그 파일 모니터링 및 저장
- **CloudWatch Events**: 시스템 이벤트 실시간 스트림
- **EventBridge**: 이벤트 기반 아키텍처 구현
- **X-Ray**: 엔드 투 엔드 트레이싱 및 분석
- **Lambda**: 각 함수 호출 자동 로그 기록
- **RDS 로그**: 오류 로그, 느린 쿼리 로그, 일반 로그 등
- **CloudTrail**: 모든 API 호출 기록

### 데이터 추적 보장
- **AWS Config**: 리소스 구성 변경 사항 기록
- **VPC Flow Logs**: 네트워크 트래픽 정보 캡처
- **Security Hub**: 보안 경고 및 컴플라이언스 상태 종합 대시보드

### 자동화 및 응답
- 특정 이벤트 발생 시 자동화된 조치를 수행하도록 Lambda 함수 설정
- 로그 패턴 기반 자동화된 조치를 수행하여 사용자 정의 로그 분석

### 성능 문제 해결
- **CloudWatch**: 주요 성능 메트릭 추적
- **AWS Health Dashboard**: 서비스 중단 여부 확인
- **애플리케이션 로그 분석**: 오류 메시지, 예외, 경고 확인
- **네트워크 성능 시각화**: 네트워크 지연 시간 및 패킷 손실 모니터링
- **Auto Scaling**: 수요 패턴에 따라 확장 정책 조정

#### Kinesis Data Streams 지연 시간 문제 해결
- **상황**: Kinesis Data Streams를 사용하여 데이터를 기록하고, KCL(Kinesis Client Library) 애플리케이션이 이를 소비하여 분석 및 DynamoDB에 저장
- **조치**: Auto Scaling 그룹의 인스턴스 CPU 사용률 확인, DynamoDB 테이블의 쓰기 용량 증가

#### Amazon Redshift 쿼리 최적화
- **조치**: 워크로드 관리 큐를 조정하여 단기 쿼리가 장기 쿼리의 영향을 받지 않도록 설정

---

## 3.4 데이터 품질 보장

### 데이터 신뢰성 확보
- 데이터를 사용하는 사람들이 데이터를 신뢰할 수 있어야 함
- 데이터를 생성, 처리, 제공하는 모든 단계에서 관찰 가능성을 보장해야 함

### 데이터 프로파일링
- 데이터의 구조, 내용, 품질을 분석하고 이해하는 과정
- 누락된 값, null 값, 데이터 분포, 데이터 품질 문제 식별
- 데이터 분포 및 패턴 이해를 통해 쿼리 성능 및 데이터 저장 최적화

### AWS에서 데이터 프로파일링 도구
- **AWS Glue DataBrew**: 코드 작성 없이 데이터 탐색 및 프로파일링 수행
- **Athena**: SQL 쿼리를 사용한 기본 데이터 프로파일링
- **Amazon Redshift**: SQL 기능을 사용한 데이터 프로파일링
- **Amazon EMR with Spark**: 사용자 정의 데이터 프로파일링 스크립트 작성

### 데이터 검증
- **데이터 완전성 확인**: 누락된 값, null 값, 빈 필드 확인
- **데이터 일관성 확인**: 사전 정의된 규칙이나 제약 조건을 통해 데이터 일관성 검증
- **데이터 정확성 확인**: 데이터가 올바르고 정확한지 확인
- **데이터 무결성 확인**: 데이터의 생성부터 삭제까지 일관성 유지

### 데이터 품질 체크 수행
- **AWS Glue DataBrew**: 레시피를 사용해 검증 규칙 및 체크 정의
- **Amazon EMR with Spark**: 데이터 처리 워크플로에서 사용자 정의 데이터 품질 체크 구축
- **Lambda**: 복잡한 데이터 품질 체크를 위한 사용자 정의 함수
- **Step Functions**: 검증 결과를 바탕으로 처리 작업 오케스트레이션

### 데이터 샘플링
- **Amazon S3 Select**: SQL 유사 쿼리를 사용해 S3 객체에서 특정 데이터 서브셋 검색
- **Athena 및 Amazon Redshift**: SQL 쿼리에서 limit 절을 사용해 데이터 샘플링
- **Amazon EMR with Spark**: 체계적 샘플링, 무작위 샘플링, 층화 샘플링 수행
- **SageMaker Data Wrangler**: 모델 학습 및 테스트를 위한 균형 잡힌 데이터셋 생성

### 데이터 왜곡 해결
- **실시간 모니터링 및 경고 설정**: CloudWatch 사용자 정의 메트릭 및 알람 구성
- **AWS Glue ETL 작업**: CloudWatch 메트릭 및 AWS Glue 작업 북마크 사용
- **Amazon EMR with Spark**: 애플리케이션 로깅 및 모니터링
- **AWS Lambda 및 Step Functions**: 실시간 왜곡 감지 및 처리 작업 오케스트레이션

### 데이터 분할 및 버킷화
- **분할 키 및 해시 함수 사용**: 데이터를 균등하게 분배
- **로드 밸런싱 메커니즘 구현**: 작업량을 모니터링하고 재분배
- **다중 노드 데이터 복제**: 자주 액세스되는 데이터의 영향을 줄이기 위해 데이터 복제

### 데이터 품질 규칙 정의
- **완전성 규칙**: 특정 열에서 누락된 값 또는 null 값을 플래그
- **형식 규칙**: 값이 특정 형식이나 패턴과 일치하는지 확인
- **범위 규칙**: 숫자 값이 지정된 범위 내에 있는지 확인
- **고유성 규칙**: 중복 레코드 또는 열의 값을 식별

### 데이터 품질 문제 해결
- DataBrew를 사용해 정의된 데이터셋에 데이터 품질 규칙을 적용
- 데이터 품질 분석 결과 검토 및 데이터 정제, 변환, 검증 수행
- 프로세스 자동화 및 지속적인 데이터 품질 모니터링 보장


