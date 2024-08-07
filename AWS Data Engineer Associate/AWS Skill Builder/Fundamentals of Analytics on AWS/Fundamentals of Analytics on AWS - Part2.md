## Data Lake
-  **데이터 레이크**는 조직이 대규모의 정형 및 비정형 데이터를 원래 형식으로 저장하는 데 사용할 수 있는 중앙 집중식 저장소
-  데이터베이스, 센서, 소셜 미디어, 문서, 애플리케이션 등 다양한 소스에서 원시 데이터를 수집
 
### Data Lake 이점
- 확장성
- 비용 효율성
- 유연성
- 더 빠른 분석
- 중앙 집중식 보기

### Data Lake 기능
> ![](https://velog.velcdn.com/images/seonwook97/post/49a2cc36-25ea-49f0-bd6d-2481275e0694/image.png)
 
- 수집과 저장
- 카탈로그 및 검색
- 보안과 방화벽
- 분석과 인사이트
   

### Data Lake 아키텍처
> ![](https://velog.velcdn.com/images/seonwook97/post/72f55c5a-f6f3-4d08-996c-f768562febf7/image.png)
 
- 데이터 소스
  - 다양한 소스로부터 정형, 반정형, 비정형 데이터 수집
- 로우 데이터
  - Amazon S3 저장 후 AWS Glue 크롤러를 통해 카탈로그화
  - Amazon S3는 비용 효율적인 스토리지 솔루션이나, 필요에 따라 Amazon Redshift(DW) 및  Amazon DB 서비스 사용
- AWS Glue
  - 데이터 소비 사용 목적에 따라 ETL하는 서비스
- 변환된 데이터
  - 분석 및 보고 목적을 위한 정제된 데이터
  - 다운스트림 데이터 소비자에게 서비스를 제공하기 위해 정리, 검증 및 구조화된 데이터가 보관
- 데이터 분석
  - AWS Athena
    - 데이터 레이크의 데이터를 소비하기 위해 SQL 실행
  - Amazon QuickSight
    - 추가분석 및 시각화 
  - Amazon SageMaker
    - 기계학습 기반의 고급 분석 
  - Amazon OpenSearch
    - 로그 분석 및 검색 솔루션 개발 

### 분석 파이프라인에 사용되는 AWS 서비스
> ![](https://velog.velcdn.com/images/seonwook97/post/4958a3af-e965-4bba-a348-24d5ba4cae5d/image.png)

### 데이터 레이크 구축 시 주요 3가지
  - 데이터 거버넌스
    - 정책 수립, 액세스 제어, 데이터 계보 추적, 메타데이터 관리 등
  - 데이터 품질(DQ)
    - 대용량 데이터에 대한 데이터 품질, 불일치, 중복 및 무결성 문제를 해결하기 위해 ETL  수행 및 정리
  - 보안
    - 대량의 이기종 데이터에 대한 액세스 제어, 암호화, 마스킹 및 감사를 위한 계획 설정
       
### AWS Lake Formation
> ![](https://velog.velcdn.com/images/seonwook97/post/4ace1ccb-7c62-4680-87cf-303223a7880b/image.png)
 
- 주요 이점
  - 완전관리형 서버리스 서비스
  - 몇 주 또는 몇 달이 아닌 며칠 만에 개발된 데이터 레이크
  - 저렴한 비용
  - 간소화된 권한 관리
  - 규정 준수 확인을 위한 액세스 모니터링 및 감사
  - 데이터 공유
  - 다양한 분석 및 기계 학습 도구와의 통합

- 주요 특징
  - 자동화된 빌드 환경
    - 데이터 레이크 생성 시 필요한 복잡한 수동 단계를 자동화
    - 데이터 수집, 정리, 이동 및 분류하고 분석 및 기계 학습에 사용할 수 있도록 하는 작업 포함
  - 메타데이터의 지속적 저장
    - AWS Glue 데이터 카탈로그는 AWS 크롤러가 식별한 원시 및 처리된 데이터 세트의 메타데이터를 지속적으로 저장
  - 스크립트 및 크롤러 조정
    - AWS Glue 작업은 소스 데이터에 연결하고 이를 처리하고 데이터 대상에 쓰는 ETL 스크립트와 같은 스크립트를 캡슐화
    - AWS Glue 트리거는 일정, 이벤트 또는 요청 시 작업을 시작할 수 있음
    - AWS Glue 워크플로는 ETL 작업, 크롤러 및 트리거를 조정
  - 중앙 집중식 액세스 제어
    - 역할별 사용자 및 애플리케이션에 대한 보안 정책 기반 규칙을 포함하여 데이터 레이크에 대한 중앙 집중식 액세스 제어를 제공
    - 데이터 레이크의 데이터에 Amazon S3의 암호화 기능을 사용
    
- Lake Formation의 역할
  - Lake Formation 관리자
    - 리소스에 대한 전체 읽기 액세스 권한이 있음
    - 데이터 위치 권한이 있음
    - 자신을 포함한 리소스에 대한 액세스 권한을 부여하거나 취소할 수 있음
    - 데이터베이스를 생성할 수 있음
    - 데이터베이스 생성 권한을 부여할 수 있음
  - 데이터베이스 생성자
    - 자신이 생성한 데이터베이스에 대한 모든 권한이 있음
    - 자신이 생성한 테이블에 대한 권한이 있음
    - 콘솔이나 API를 사용하여 데이터베이스 생성자를 지정할 수 있음
  - 테이블 생성자
    - 자신이 생성한 테이블에 대한 권한이 있음
    - 자신이 생성한 테이블에 대한 권한을 부여할 수 있음
    - 자신이 생성한 테이블이 포함된 데이터베이스를 볼 수 있음

### Data Lake 사용 사례
 - 의료용 AWS 분석
   - 방대한 양의 의료 데이터를 수집, 저장, 분석
 - 자동차용 AWS 분석
   - 분석 결과를 의미 있고 접근 가능하게 만듦
 - 에너지에 대한 AWS 분석
   - 재생 가능 에너지 자산에 대한 데이터 레이크 및 분석 사용

---

## AWS 최신 데이터 및 분석 아키텍처
> ![](https://velog.velcdn.com/images/seonwook97/post/62e37184-f338-4443-813b-feb5afe3affe/image.png)

- Data sources
- Data ingestion
- Scalable data lake
- Seamless data movement
- Purpose-built analytics and Insights

### 스트리밍 데이터 아키텍처
> ![](https://velog.velcdn.com/images/seonwook97/post/3f9dfae3-f689-41ec-8c45-d4c5be069649/image.png)

- 데이터 소스
  - 애플리케이션 및 클릭 스트림 로그, 모바일 앱, 기존 트랜잭션 관계형 및 NoSQL 데이터베이스, IoT 센서, 측정 장치가 포함
- 스트림 수집 및 생산자
  - 다양한 소스에서 스트리밍 플랫폼에 수집됨
  - 사용자 지정 스트리밍 생산자 또는 Amazon Kinesis, Apache Kafka와 같은 사전 구축 생산자가 있음
- 스트림 저장
  - 스트리밍 데이터는 배치 분석, 기록 분석 및 규정 준수를 위해 저장됨
  - 스트림 스토리지 옵션에는 Kinesis Data Streams, Amazon MSK, Apache Kafka가 포함
- 스트림 처리 및 소비자
  - 데이터가 도착하는 대로 처리하여 필터링, 변환 및 강화할 수 있음
  - Amazon EMR(Spark Structured Streaming, Apache Flink), AWS Glue ETL 스트리밍, Apache Flink용 Amazon Managed Service, 타사 통합, AWS 및 오픈 소스 커뮤니티 SDK 및 라이브러리를 사용하여 자체 사용자 지정 애플리케이션 구축
- 다운스트림 목적지
  - 처리된 스트리밍 데이터를 소비하는 최종 사용자 또는 애플리케이션
  - DB, DW, OpenSearch Service와 같은 특수 구축 시스템, 데이터 레이크, 다양한 타사 통합 등

### 데이터 시각화 아키텍처
>![](https://velog.velcdn.com/images/seonwook97/post/d4de07f0-910a-4637-bcd4-fb31c56153b7/image.png)

- 확장성
  - 인프라는 수직 및 수평으로 확장되어 대량의 데이터와 늘어나는 사용자 수를 처리할 수 있음
- 연결성
  - 기존 DW 및 DB와 같은 데이터 플랫폼과 연결할 수 있어야 함
  - DataLake, 최신 아키텍처 및 SaaS 애플리케이션과 같은 비전통적인 소스에 대한 연결을 지원해야 함
- 중앙 집중식 보안 및 규정 준수
  - 계층화된 보안, 인증 승인, 암호화 등 강력한 보안 기능이 필수적
  - 경계 보안, 전송 중인 데이터와 저장 중인 데이터의 보안, 사용자에 대한 세분화된 권한을 통해 다양한 수준의 액세스 제한이 포함
  - 정부 및 업계 규정을 준수해야 함
- 공유 및 협업
  - 협업 기능과 데이터 민주화를 지원해야 함
    - 데이터 민주화
    `데이터를 조직 내의 모든 구성원이 쉽게 접근하고 활용할 수 있도록 하는 과정`
  - 대시보드 및 시각화를 다른 사람과 공유할 수 있는 기능이 있어야 함
- 로깅, 모니터링, 감사
  - 내장된 모니터링 도구는 사용자 상호 작용, 시스템 성능 및 사용 패턴에 대한 인사이트를 제공
  - 애플리케이션은 보안 및 문제 해결을 위해 사용을 모니터링하고 감사하기 위한 적절한 메커니즘을 제공해야 함
- 고급 분석 수행
  - 조직은 사용자 행동을 분석하고 사용자 기본 설정에 따라 시각화를 최적화 할 수 있음
  - 데이터에서 숨겨진 인사이트를 발견하고, 예측 및 가상 분석을 수행하거나, 이해하기 쉬운 자연어 설명을 대시보드에 추가할 수 있어야 함
  - 조직은 심층적인 통계 및 머신러닝 지식 없이도 분석을 수행할 수 있어야 함
- 셀프 서비스 상호 작용
  - 광범위한 사용자 교육이나 기술적인 이해 없이도 더 많은 사람들이 데이터에 더 쉽게 접근할 수 있도록 하는 것
  - 원시, 반가공, 처리 등 모든 형식으로 제공되어야 함
  - 셀프 서비스 애플리케이션을 사용하면 사용자는 IT의 개입 없이 필요에 따라 데이터와 상호 작용할 수 있어야 함
  
---

## Reference
- AWS 기반 분석의 기초 -2부
  - https://explore.skillbuilder.aws/learn/course/18440/play/100188/fundamentals-of-analytics-on-aws-part-2