# SAA-C03 덤프 노트 1

**S3 Transfer Acceleration** 
- 모든 글로벌 사이트의 데이터를 단일 Amazon S3 버킷에 최대한 빨리 집계
- 솔루션 운영 복잡성 최소화
    
    → **대상 S3 버킷에서 S3 Transfer Acceleration을 켭니다. 멀티파트 업로드를 사용하여 사이트 데이터를 대상 S3 버킷에 직접 업로드**
    
    - 여러 글로벌 사이트의 데이터를 단일 Amazon S3 버킷으로 신속하게 집계하는 가장 효율적이고 운영상 간단한 솔루션을 제공
    - S3 Transfer Acceleration 및 멀티파트 업로드를 활용하여 회사는 복잡성을 최소화하면서 빠른 데이터 수집을 달성할 수 있음

**Amazon S3, Amazon Athena**
- 로그는 Amazon S3 버킷에 JSON 형식으로 저장
- 쿼리는 간단하고 주문형으로 실행
- 기존 아키텍처에 대한 최소한의 변경으로 분석을 수행
- 최소한의 운영 오버헤드로 이러한 요구 사항을 충족
    
    → **Amazon S3와 함께 Amazon Athena Athena를 직접 사용하여 필요에 따라 쿼리를 실행**
    
    - S3에 쿼리하는 건 Athena
    - Athena가 사용 가능한 모든 리전에서 Amazon Athena를 사용하여 표준 SQL로 Amazon S3 인벤토리를 쿼리할 수 있음
    - Athena로 JSON 쿼리 가능
    - Athena를 사용하면 JSON 인코딩 값을 구문 분석하고, JSON에서 데이터를 추출하고, 값을 검색하고, JSON 배열의 길이와 크기를 찾을 수 있음

**AWS PrincipalOrgID**
- 회사는 AWS Organizations를 사용하여 여러 부서의 여러 AWS 계정을 관리
- 관리 계정에는 프로젝트 보고서가 포함된 Amazon S3 버킷이 있음
- S3 버킷에 대한 액세스를 AWS Organizations의 조직 내 계정 사용자로만 제한하려고 함
- 최소한의 운영 오버헤드로 이러한 요구 사항을 충족
    
    → **조직 ID에 대한 참조와 함께 aws PrincipalOrgID 전역 조건 키를 S3 버킷 정책에 추가함**
    
    - PrincipalOrgID라는 새로운 조건 키를 권한 정책에 사용하여 조직 내의 계정에 해당하는 IAM 보안 주체(사용자 및 역할)만 리소스에 액세스할 수 있도록 함
    - PrincipalOrgID 전역 키는 조직의 모든 AWS 계정에 대한 모든 계정 ID를 나열하는 대신 사용할 수 있음. 예를 들어 다음 Amazon S3 버킷 정책은 XXX 조직의 모든 계정 구성원이 시험 주제 버킷에 객체를 추가하도록 허용
    
**S3 VPC Gateway Endpoint**
- 애플리케이션은 VPC의 Amazon EC2 인스턴스에서 실행
- Amazon S3 버킷에 저장된 로그를 처리
- EC2 인스턴스는 인터넷 연결 없이 S3 버킷에 액세스해야 함
- Amazon S3에 대한 프라이빗 네트워크 연결을 제공하는 솔루션
    
    → **S3 버킷에 대한 게이트웨이 VPC 엔드포인트를 생성**
    
    - VPC-S3 간 인터넷을 통하지 않는 연결 = S3 VPC Gateway Endpoint
    - VPC 종단점을 사용하면 공용 인터넷을 사용하는 대신 사설 네트워크를 사용하여 AWS 서비스에 연결할 수 있음

**Amazon EFS**
- 사용자 업로드 문서를 Amazon EBS 볼륨에 저장하는 단일 Amazon EC2 인스턴스를 사용하여 AWS에서 웹 애플리케이션을 호스팅
- 더 나은 확장성과 가용성을 위해 이 회사는 아키텍처를 복제하고 다른 가용 영역에 두 번째 EC2 인스턴스와 EBS볼륨을 생성하여 Application Load Balancer 뒤에 배치
- 변경을 완료한 후 사용자는 웹 사이트를 새로 고칠 때마다 문서의 일부 또는 다른 하위 집합을 볼 수 있지만 모든 문서를 동시에 볼 수는 없음
- 사용자가 모든 문서를 한 번에 볼 수 있도록 무엇을 제안
    
    → **두 EBS 볼륨의 데이터를 Amazon EFS로 복사합니다. 새 문서를 Amazon EFS에 저장하도록 애플리케이션을 수정**
    
    - EBS와 EFS의 가장 큰 차이점 중 하나는 EBS는 단일 AZ안에서만 접근이 가능한 저장소인 반면, EFS는 다중 AZ안에서도 접근이 가능한 저장소라는 점
    - 초기 단일 AZ에서 운영하던 EC2 및 EBS를 복제한뒤 AZ를 2중화하여 멀티 EC2 및 EBS 시스템으로 구성하였지만, 각 AZ 내에서 공유되지 않는 EBS 저장소를 별도로 운영하였기 때문에 고객들에게 일관성 있는 데이터를 제공할 수 없었음
    - 초기 EBS에 저장되어있던 데이터들을 일관성 있게 보정하여 EFS로 일회성 마이그레이션을 수행한 뒤 EC2 어플리케이션 서버 인스턴스가 EBS가 아닌 EFS에 데이터를 저장하도록 변경하는 것이 바람직 함
    - 여러 NFS 클라이언트에서 동시에 Amazon EFS 파일 시스템에 액세스할 수 있으므로 단일 연결 이상으로 확장되는 애플리케이션이 파일 시스템에 액세스할 수 있습니다. 동일한 AWS 리전 내의 여러 가용 영역에서 실행되는 Amazon EC2 인스턴스는 파일 시스템에 액세스할 수 있으므로 많은 사용자가 공통 데이터 원본에 액세스하고 공유할 수 있음

**Amazon Snowball, Snowball Edge**
- 회사는 NFS를 사용하여 온프레미스 네트워크 연결 스토리지에 대용량 비디오 파일을 저장
- 각 비디오 파일의 크기 범위는 1MB에서 500GB, 총 스토리지는 70TB이며 더 이상 증가하지 않음
- 회사는 비디오 파일을 Amazon S3로 마이그레이션하기로 결정
- 가능한 한 최소한의 네트워크 대역폭을 사용하면서 가능한 한 빨리 비디오 파일을 마이그레이션해야 함
    
    → **AWS Snowball Edge 작업을 생성합니다. 온프레미스에서 Snowball Edge 장치를 받습니다. Snowball Edge 클라이언트를 사용하여 장치로 데이터를 전송합니다. AWS가 데이터를 Amazon S3로 가져올 수 있도록 디바이스를 반환**
    
    - 가능한 한 최소한의 네트워크 대역폭을 사용하라 했으니 아예 오프라인에서 Snowball Edge로 올리는 게 맞음
    - AWS Snowball 및 AWS Snowball Edge는 기존 저장소에서 네트워크 대역폭이 충분하지 않을 때, 대용량 데이터 세트를 클라우드로 이전하는데 도움이 됨.
    - Snowball 장치는 80TB, Snowball Edge Edge는 100TB까지 한번에 이동 가능함.
    - Snowball과 Snowball Edge의 기본적인 차이점은 제공하는 용량
        - Snowball Snowball은 총 50TB 또는 80TB를 제공하며 그 중 42TB 또는 72TB를 사용할 수 있고 Amazon Snowball Edge는 100TB를 제공하며 그 중 83TB를 사용할 수 있음

**Amazon SQS**
- 회사에 들어오는 메시지를 수집하는 응용 프로그램
- 수십 개의 다른 애플리케이션과 마이크로서비스가 이러한 메시지를 빠르게 소비
- 메시지 수는 급격하게 변하며 때로는 초당 100,000개로 갑자기 증가
- 솔루션을 분리하고 확장성을 높이고자 함
    
    → **여러 Amazon Simple Queue Service(Amazon SQS) 구독이 있는 Amazon Simple Notification Service(Amazon SNS) 주제에 메시지를 게시합니다 . 대기열의 메시지를 처리하도록 소비자 애플리케이션을 구성함**
    
    - 들어오는 요청을 Amazon SQS로 라우팅함으로써 회사는 처리 인스턴스에서 작업 요청을 분리할 수 있음
    - 이를 통해 대기열 크기에 따라 인스턴스 수를 확장하여 필요할 때 더 많은 리소스를 제공할 수 있습니다. 또한 대기열 크기를 기반으로 하는 Auto Scaling 그룹을 사용하면 워크로드에 따라 자동으로 인스턴스 수를 늘리거나 줄일 수 있음
    - 대기열에서 읽을 수 있도록 소프트웨어를 업데이트하면 보다 효율적인 방식으로 작업 요청을 처리할 수 있어 시스템 성능이 향상
    - 솔루션을 분리 = SQS

**Amazon SQS**
- 회사에서 분산 애플리케이션을 AWS로 마이그레이션 하고 있음
- 애플리케이션은 다양한 워크로드를 처리
- 레거시 플랫폼은 여러 컴퓨팅 노드에서 작업을 조정하는 기본 서버로 구성
- 탄력성과 확장성을 극대화하는 솔루션으로 애플리케이션을 현대화
    
    → **작업의 대상으로 Amazon Simple Queue Service(Amazon SQS) 대기열을 구성합니다. Auto Scaling 그룹에서 관리되는 Amazon EC2 인스턴스로 컴퓨팅 노드를 구현합니다. 대기열 크기에 따라 EC2 Auto Scaling을 구성**
    
    - SQS Queue로 갑작스레 작업이 몰려도 추후 처리하도록 보관 가능. Auto Scaling 그룹으로 여러 EC2 인스턴스의 확장 축소를 적절하게 지원
    - 복원력과 확장성을 극대화하기 위한 최상의 솔루션은 Amazon SQS 대기열을 작업의 대상으로 사용하는 것
    - 이렇게 하면 컴퓨팅 노드에서 기본 서버가 분리되어 독립적으로 확장할 수 있음
    - 이는 또한 실패 시 일자리 손실을 방지하는 데 도움
    - 컴퓨팅 노드에 대해 Amazon EC2 인스턴스의 Auto Scaling 그룹을 사용하면 워크로드에 따라 자동 조정이 가능
    - 이 경우 Amazon SQS 대기열의 크기를 기반으로 Auto Scaling 그룹을 구성하는 것이 좋음
    - 이는 기본 서버 또는 컴퓨팅 노드의 로드보다 실제 워크로드를 더 잘 나타내는 지표
    - 이 접근 방식은 애플리케이션이 가변 워크로드를 처리할 수 있도록 하는 동시에 필요에 따라 컴퓨팅 노드를 자동으로 확장 또는 축소하여 비용을 최소화함
    
**Amazon S3 File Gateway, Amazon S3 Glacier Deep Archive**
- 회사는 데이터 센터에서 SMB 파일 서버를 실행
- 파일 서버는 파일이 생성된 후 처음 며칠 동안 자주 액세스하는 대용량 파일을 저장
- 7일이 지나면 파일에 거의 액세스하지 않음
- 총 데이터 크기가 증가하고 있으며 회사의 총 저장 용량에 가까움
- 가장 최근에 액세스한 파일에 대한 저지연 액세스를 잃지 않으면서 회사의 사용 가능한 저장 공간을 늘려야 함
- 향후 스토리지 문제를 방지하기 위해 파일 수명 주기 관리도 제공해야 함
    
    → **Amazon S3 파일 게이트웨이를 생성하여 회사의 스토리지 공간을 확장합니다. S3 수명 주기 정책을 생성하여 7 일 후에 데이터를 S3 Glacier Deep Archive 로 전환합니다.**
    
    - 사용 가능한 스토리지 공간을 늘림 = Storage Gateway
    - 스토리지 게이트웨이는 온프레미스 스토리지와 AWS 스토리지를 합쳐 사실상
    무제한의 스토리지를 향유하는 것을 목적으로 하는 서비스
    - 최근에 액세스한 데이터에 대해 빠른 로컬 액세스를 유지하면서 온프레미스 파일 데이터를 Amazon S3 로 마이그레이션
    - SMB(서버메시지 블록) 버전 2 및 3 을 사용하여 게이트웨이에 연결하는 Windows 클라이언트를
    지원
    - Amazon S3 File Gateway 는 온프레미스 애플리케이션이 Amazon S3 클라우드 스토리지를
    원활하게 사용할 수 있도록 하는 하이브리드 클라우드 스토리지 서비스
    - Amazon S3 에 대한 파일 인터페이스를 제공하고 SMB 및 NFS 프로토콜을 지원
    - 지정된 기간이 지나면 데이터를 S3 Standard 에서 S3 Glacier Deep Archive 로 자동 전환할 수 있는
    S3 수명 주기 정책을 지원
    - 짧은 대기 시간 액세스를 유지하면서 회사의 사용 가능한 저장 공간을 늘리는 요구 사항을 충족
    - 가장 최근에 액세스한 파일에 저장하고 파일 수명 주기 관리를 제공하여 향후 스토리지
    문제를 방지

**Amazon Simple Queue Servise FIFO, AWS Lambda**
- 회사는 AWS 에서 전자 상거래 웹 애플리케이션을 구축
- 애플리케이션은 처리할 Amazon API Gateway REST API 에 새 주문에 대한 정보를 보냄
- 회사는 주문이 접수된 순서대로 처리되기를 원함
    
    → **API Gateway 통합을 사용하여 애플리케이션이 주문을 수신할 때 Amazon Simple Queue Service(Amazon SQS) FIFO 대기열에 메시지를 보냅니다. 처리를 위해 AWS Lambda 함수를 호출하도록 SQS FIFO 대기열을 구성합니다.**
    
    - 주문이 접수된 순서대로 처리되도록 하기 위한 최상의 솔루션은 Amazon SQS FIFO(선입선출) 대기열을 사용하는 것
    - 애플리케이션은 새 주문에 대한 정보를 Amazon API Gateway REST API 로 보낼 수 있음
    - API Gateway 통합을 사용하여 처리를 위해 메시지를 Amazon SQS FIFO 대기열로 보낼 수 있음
    - AWS Lambda 함수를 호출하여 각 주문에 필요한 처리를 수행하도록 대기열을 구성

**AWS Secrets Manager**
- 회사는 Amazon EC2 인스턴스에서 실행되고 Amazon Aurora 데이터베이스를 사용
- EC2 인스턴스는 파일에 로컬로 저장된 사용자 이름과 암호를 사용하여 데이터베이스에 연결
- 회사는 자격 증명 관리의 운영 오버헤드를 최소화하려고
    
    → **Secrets Manager 는 자격증명을 저장해두고 관리할 수 있는 서비스**
    
    - 자격증명을 저장해두고 관리할 수 있는 서비스
    - 앱, 서비스 및 IT 리소스에 대한 액세스를 보호하는 데 도움이 되는 보안 정보 관리 서비스
    - 수명 주기 동안 DB 자격 증명, API 키 및 기타 보안 정보를 손쉽게 교체, 관리 및 검색할 수 있음
    - 보안 암호에 대한 자동 교체를 설정할 수 있음

**AWS ALB, S3, Route53, CloudFront**
- 글로벌 회사는 ALB(Application Load Balancer) 뒤의 Amazon EC2 인스턴스에서 웹 어플을 호스팅
- 웹 애플리케이션에는 정적 데이터와 동적 데이터가 있음
- 정적 데이터를 Amazon S3 버킷에 저장
- 정적 데이터 및 동적 데이터의 성능을 개선하고 대기 시간을 줄이기를 원함
- Amazon Route 53 에 등록된 자체 도메인 이름을 사용하고 있음
    
    → **S3 버킷과 ALB 를 오리진으로 포함하는 Amazon CloudFront 배포를 생성합니다. CloudFront 배포로 트래픽을 라우팅하도록 Route 53 을 구성합니다.**
    
    - 배포를 만들 때 CloudFront 가 파일에 대한 요청을 보내는 원본을 지정
    - CloudFront 에서 여러 원본을 사용할 수 있음
    - Amazon S3 버킷, MediaStore 컨테이너, MediaPackage 채널, Application Load Balancer 또는 AWS Lambda 함수 URL 을 사용할 수 있음
    - Amazon Route 53 을 구성하여 CloudFront 배포로 트래픽을 라우팅함
    - 정적 콘텐츠는 S3 의 클라우드 프런트 엣지 위치와 ALB 뒤의 동적 콘텐츠 EC2 에서 캐싱할 수 있음
    - 그 성능은 하나의 엔드포인트가 ALB 이고 다른 클라우드 프런트인 Global Accelerator 에 의해 개선될 수 있음
    - 사용자 지정 도메인 이름 끝점과 관련하여 웹 응용 프로그램은 웹 응용 프로그램에 대한 사용자 지정 도메인 지점에 대한 R53 별칭 레코드

**AWS Secrets Manager**
- 회사는 AWS 인프라에 대한 월별 유지 관리를 수행
- 여러 AWS 리전에서 MySQL 용 Amazon RDS 데이터베이스에 대한 자격 증명을 교체해야
- 최소한의 운영 오버헤드로 이러한 요구 사항을 충족
    
    → **자격 증명을 AWS Secrets Manager 에 암호로 저장합니다. 필요한 리전에 대해 다중 리전 비밀 복제를 사용합니다. 일정에 따라 보안 암호를 교체하도록 Secrets Manager를 구성합니다.**
    
    - 다중 리전 애플리케이션에 필수 리전의 복제된 암호에 대한 액세스 권한을 부여
    - Secrets Manager 를 사용하여 복제본이 기본 암호와 동기화된 상태를 유지할 수 있음
    - 데이터베이스 자격 증명, API 키 및 기타 비밀을 포함한 비밀을 저장, 검색, 관리 및 교체할 수 있음

**AWS Aurora**
- 회사는 Application Load Balancer 뒤의 Amazon EC2 인스턴스에서 전자 상거래 애플리케이션을 실행
- 인스턴스는 여러 가용 영역에 걸쳐 Amazon EC2 Auto Scaling 그룹에서 실행됨
- Auto Scaling 그룹은 CPU 사용률 메트릭을 기반으로 확장
- 전자 상거래 애플리케이션은 대규모 EC2 인스턴스에서 호스팅되는 MySQL 8.0 데이터베이스에 트랜잭션 데이터를 저장
- 애플리케이션 로드가 증가하면 데이터베이스의 성능이 빠르게 저하
- 애플리케이션은 쓰기 트랜잭션보다 더 많은 읽기 요청을 처리함
- 고가용성을 유지하면서 예측할 수 없는 읽기 워크로드의 수요를 충족하도록 데이터베이스를 자동으로 확장하는 솔루션
    
    → **다중 AZ 배포와 함께 Amazon Aurora를 사용합니다. Aurora 복제본을 사용하여 Aurora Auto Scaling을 구성합니다.**
    
    - Aurora는 자동으로 3개의 AZ에 6개의 복제본을 생성. 이러한 복제본은 읽기 부하 분산 효과가 있음
    - Aurora는 RDS 에서 MySQL 보다 5배 향상된 성능을 제공하며 쓰기보다 더 많은 읽기 요청을 처리
    - 고가용성 유지 = 다중 AZ 배포

**AWS Network Firewall**
- AWS로 마이그레이션한 회사가 프로덕션 VPC로 들어오고 나가는 트래픽을 보호하는 솔루션을 구현하려고 함
- 사내 데이터 센터에 검사 서버를 가지고 있음.
- 검사 서버는 트래픽 흐름 검사 및 트래픽 필터링과 같은 특정 작업을 수행
- 회사는 AWS 클라우드에서 동일한 기능을 갖기를 원함
    
    → **AWS 네트워크 방화벽을 사용하여 프로덕션 VPC 에 대한 트래픽 검사 및 트래픽 필터링에 필요한 규칙을 생성합니다.**
    
    - AWS Network Firewall 은 필요에 따라 검사와 필터링을 모두 지원
    - AWS Network Firewall 을 사용하면 VPC 경계에서 네트워크 트래픽을 필터링할 수 있음

**Amazon QuickSight**
- 회사는 AWS 에서 데이터 레이크를 호스팅
- 데이터 레이크는 Amazon S3 및 PostgreSQL 용 Amazon RDS 의 데이터로 구성
- 데이터 시각화를 제공하고 데이터 레이크 내의 모든 데이터 소스를 포함하는 보고 솔루션이 필요
- 회사의 관리팀만 모든 시각화에 대한 전체 액세스 권한을 가져야 함
- 나머지 회사는 제한된 액세스 권한만 가져야
    
    → **Amazon QuickSight 에서 분석을 생성합니다. 모든 데이터 소스를 연결하고 새 데이터 세트를 만듭니다. 대시보드를 게시하여 데이터를 시각화합니다. 적절한 사용자 및 그룹과 대시보드를 공유합니다.**
    
    - 시각화 = QuickSight. A,B 둘 중 하나가 정답. 대시보드를 그룹과 사용자와 공유
    - 기본적으로 Amazon QuickSight 의 대시보드는 누구와도 공유되지 않으며 소유자만
    액세스할 수 있음
    - 대시보드를 게시한 후에는 QuickSight 계정의 다른 사용자 또는 그룹과 공유할 수 있음
    - Amazon QuickSight 는 PostgreSQL 용 Amazon S3 및 Amazon RDS 를 비롯한 다양한
    데이터 소스에서 대화형 대시보드 및 보고서를 생성할 수 있는 데이터 시각화 서비스
    - 데이터 소스를 연결하고 QuickSight 에서 새 데이터 세트를 만든 다음 대시보드를
    게시하여 데이터를 시각화할 수 있음
    - 적절한 사용자 및 그룹과 대시보드를 공유하고 IAM 역할 및 권한을 사용하여 액세스 수준을 제어할 수 있음
**AWS IAM 역할**
- 두 개의 Amazon EC2 인스턴스에서 실행되며 문서 저장을 위해 Amazon S3 버킷을 사용
- EC2 인스턴스가 S3 버킷에 액세스할 수 있는지 확인해야 함
    
    → **S3 버킷에 대한 액세스 권한을 부여하는 IAM 역할을 생성합니다. 역할을 EC2 인스턴스에 연결합니다.**
    
    - EC2 인스턴스가 S3 버킷에 액세스할 수 있는 권한이 있어야 하므로 IAM 역할을 부여해야 함

**AWS S3, Amazon Simple Queue Service, AWS Lambda**
- 애플리케이션 개발 팀은 큰 이미지를 더 작은 압축 이미지로 변환하는 마이크로 서비스를
설계하고 있음
- 사용자가 웹 인터페이스를 통해 이미지를 업로드하면 마이크로 서비스는 이미지를 Amazon S3 버킷에 저장하고, AWS Lambda 함수로 이미지를 처리 및 압축하고, 다른 S3 버킷에 압축된 형태로 이미지를 저장해야함
- 내구성이 있는 상태 비저장 구성 요소를 사용하여 이미지를 자동으로 처리하는 솔루션을 설계해야 함
    
    → **Amazon Simple Queue Service(Amazon SQS) 대기열을 생성합니다. 이미지가 S3 버킷에 업로드될 때 SQS 대기열에 알림을 보내도록 S3 버킷을 구성합니다.**
    
    → **Amazon Simple Queue Service(Amazon SQS) 대기열을 호출 소스로 사용하도록 Lambda 함수를 구성합니다. SQS 메시지가 성공적으로 처리되면 대기열에서 메시지를 삭제합니다.**
    
    - Amazon Simple Queue Service(SQS) 대기열을 생성하고 이미지가 S3 버킷에 업로드될 때
    SQS 대기열에 알림을 보내도록 S3 버킷을 구성하면 Lambda 함수가 상태 비저장 및
    내구성 방식으로 트리거 됨
    - SQS 대기열을 호출 소스로 사용하도록 Lambda 함수를 구성하고 성공적으로 처리된 후
    대기열에서 메시지를 삭제하면 Lambda 함수가 상태 비저장 및 내구성 방식으로 이미지를
    처리

**AWS Gateway Load Balancer**
- 회사에 AWS 에 배포된 3 계층 웹 애플리케이션이 있음
- 웹 서버는 VPC 의 퍼블릭 서브넷에 배포
- 애플리케이션 서버와 데이터베이스 서버는 동일한 VPC 의 프라이빗 서브넷에 배포
- 회사는 AWS Marketplace 의 타사 가상 방화벽 어플라이언스를 검사 VPC 에 배포
- 어플라이언스는 IP 패킷을 수락할 수 있는 IP 인터페이스로 구성
- 트래픽이 웹 서버에 도달하기 전에 애플리케이션에 대한 모든 트래픽을 검사하기 위해 웹 애플리케이션을 어플라이언스와 통합해야 함
- 최소한의 운영 오버헤드로 이러한 요구 사항을 충족
    
    → **검사 VPC 에 게이트웨이 로드 밸런서를 배포합니다. 게이트웨이 로드 밸런서 엔드포인트를 생성하여 수신 패킷을 수신하고 패킷을 어플라이언스로 전달합니다.**
    
    - AWS Gateway Load Balancer 를 사용하면 방화벽, 침입 탐지 및 방지 시스템, 심층 패킷 검사
    시스템과 같은 가상 어플라이언스를 배포, 확장 및 관리할 수 있음
    - Gateway Load Balancer 는 Gateway Load Balancer 엔드포인트를 사용하여 VPC 경계 전체에서 트래픽을 안전하게 교환함

**AWS EBS**
- 회사에서 동일한 AWS 리전의 테스트 환경에 대량의 프로덕션 데이터를 복제하는 기능을
    
    개선하려고 함
    
- 데이터는 Amazon Elastic Block Store(Amazon EBS) 볼륨의 Amazon EC2 인스턴스에 저장됨
- 복제된 데이터를 수정해도 프로덕션 환경에 영향을 주지 않아야 함
- 이 데이터에 액세스하는 소프트웨어는 일관되게 높은 I/O 성능을 요구함
- 프로덕션 데이터를 테스트 환경에 복제하는 데 필요한 시간을 최소화해야
    
    → **프로덕션 EBS 볼륨의 EBS 스냅샷을 만듭니다. EBS 스냅샷에서 EBS 빠른 스냅샷 복원기능을 켭니다. 스냅샷을 새 EBS 볼륨으로 복원합니다. 테스트 환경의 EC2 인스턴스에 새 EBS 볼륨을 연결합니다.**
    

**Amazon S3, Amazon CloudFront, Amazon API Gateway, AWS Lambda, Amazon DynamoDB**
- 전자 상거래 회사는 AWS 에서 하루 1 회 웹 사이트를 시작하려고 함
- 매일 24 시간동안 정확히 하나의 제품을 판매
- 피크 시간 동안 밀리초 지연 시간으로 시간당 수백만 개의 요청을 처리할 수 있기를 원함
- 최소한의 운영 오버헤드로 이러한 요구 사항을 충족
    
    → **Amazon S3 버킷을 사용하여 웹 사이트의 정적 콘텐츠를 호스팅합니다. Amazon CloudFront 배포를 배포합니다. S3 버킷을 오리진으로 설정합니다. 백엔드 API 에 Amazon API Gateway 및 AWS Lambda 함수를 사용합니다. Amazon DynamoDB 에 데이터를 저장합니다.**
    
    - 정적인 웹사이트 요소들은 S3 + CloudFront 로 빠르게 제공
    - API Gateway 에서 Lambda 함수를 호출해 DynamoDB 에 데이터 저장 가능
    - DynamoDB 는 확장성이 뛰어나고 밀리초 단위 액세스를 지원하는 데이터베이스 유형
    - HTTPS 엔드포인트를 통해 API 를 호출하면 API Gateway 가 Lambda 함수를 호출
    - DynamoDB 를 사용해 최신 서버리스 애플리케이션을 구축하여 우선 작은
    규모에서 시작했다가 전역적으로 확장하여 초당 페타바이트 단위의 데이터와 수천만 건의
    읽기 및 쓰기 요청을 지원하도록 할 수 있음
    - DynamoDB 는 용량에 맞게 테이블을 자동으로 조정하므로 별도로 관리하지 않아도 성능을 유지

**Amazon S3 Intelligent-Tiering**
- Amazon S3 를 사용하여 새로운 디지털 미디어 애플리케이션의 스토리지 아키텍처를 설계
- 미디어 파일은 가용 영역 손실에 대한 복원력이 있어야 함
- 일부 파일은 자주 액세스되는 반면 다른 파일은 예측할 수 없는 패턴으로 거의 액세스되지 않음
- 미디어 파일을 저장하고 검색하는 비용을 최소화해야 함
    
    → **S3 Intelligent-Tiering (S3 지능형 계층화)**
    
    - S3 Intelligent-Tiering - 액세스 빈도 또는 불규칙한 사용 패턴을 모를 때 완벽한 사용사례

**AWS S3 Glacier Deep Archive** 
- 회사에서 Amazon S3 Standard 스토리지를 사용하여 백업 파일을 저장하고 있음
- 1개월 동안 파일에 자주 액세스
- 단, 1개월 이후에는 파일에 접근하지 않음
- 회사는 파일을 무기한 보관해야 함
- 요구 사항을 가장 비용 효율적으로 충족하는 스토리지 솔루션
    
    → **S3 수명 주기 구성을 생성하여 1개월 후에 S3 Standard에서 S3 Glacier Deep Archive로 객체를 전환합니다**
    
    - 1개월 후에 객체를 S3 Standard에서 S3 Glacier Deep Archive로 전환하는 S3 수명 주기 구성을 생성
    - Amazon S3 Glacier Deep Archive는 거의 액세스하지 않고 몇 시간의 검색 시간이 허용되는 데이터의 장기 보존을 위한 안전하고 내구성이 있으며 매우 저렴한 Amazon S3 스토리지 클래스
    - Amazon S3에서 가장 저렴한 스토리지 옵션이므로 1개월 후에 액세스하지 않는 백업 파일을 저장하는 데 비용 효율적인 선택입니다.
    - S3 수명 주기 구성을 사용하여 1개월 후에 객체를 S3 Standard에서 S3 Glacier Deep Archive 자동 전환할 수 있습니다. 이렇게 하면 자주 액세스하지 않는 백업 파일의 저장 비용이 최소화

**Cost Explorer**
- 회사는 가장 최근 청구서에서 Amazon EC2 비용 증가를 관찰
- EC2 인스턴스에 대한 인스턴스 유형의 원치 않는 수직적 확장을 발견
- 지난 22개월간의 EC2 비용을 비교하는 그래프를 생성하고 심층 분석을 수행하여 수직적 확장의 근본 원인을 식별해야 함
    
    → **Cost Explorer의 세분화된 필터링 기능을 사용하여 인스턴스 유형을 기반으로 EC2 비용에 대한 심층 분석을 수행합니다.**
    
    - AWS Cost Explorer는 비용과 사용량을 보고 분석할 수 있는 도구
    - 기본 그래프, Cost Explorer 비용 및 사용량 보고서 또는 Cost Explorer RI보고서를 사용하여 사용량 및 비용을 탐색할 수 있음
    - 최대 지난 12개월 동안의 데이터를 보고 향후 12개월 동안 지출할 가능성이 있는 금액을 예측하고 구매할 예약 인스턴스에 대한 추천을 받을 수 있음
    - 추가 조사가 필요한 영역을 식별하고 비용을 이해하는 데 사용할 수 있는 추세를 볼 수 있음

**AWS Lambda, Amazon Simple Queue Service**
- 애플리케이션은 AWS Lambda 함수를 사용하여 Amazon API Gateway를 통해 정보를 수신하고 Amazon Aurora PostgreSQL 데이터베이스에 정보를 저장
- 개념 증명 단계에서 회사는 데이터베이스에 로드해야 하는 대용량 데이터를 처리하기 위해 Lambda 할당량을 크게 늘려야 함
- 확장성을 개선하고 구성 노력을 최소화하기 위해 새로운 설계를 권장해야 함
    
    → **두 개의 Lambda 함수를 설정합니다. 정보를 수신할 하나의 기능을 구성하십시오. 정보를 데이터베이스에 로드하도록 다른 기능을 구성하십시오. Amazon Simple Queue Service(Amazon SQS) 대기열을 사용하여 Lambda 함수를 통합합니다.**
    
    - 대기열로 병목 현상을 방지할 수 있습니다
    - 대량의 데이터 처리 + 확장성 개선 = SQS queue + Lambda 조합

**AWS Config**
- 회사는 AWS 클라우드 배포를 검토하여 Amazon S3 버킷에 무단 구성 변경이 없는지 확인해야 함
    
    → **적절한 규칙으로 AWS Config를 켭니다.**
    
    - AWS Config는 AWS 리소스 구성을 측정, 감사 및 평가할 수 있는 서비스
    - Config는 AWS 리소스 구성을 지속적으로 모니터링 및 기록하고, 원하는 구성을 기준으로 기록된 구성을 자동으로 평가해 줌

**Amazon CloudWatch**
- Amazon CloudWatch 대시보드에 애플리케이션 지표를 표시함
- 제품 관리자는 이 대시보드에 주기적으로 액세스해야 함
- 제품 관리자에게 AWS 계정이 없음
- 최소 권한 원칙에 따라 제품 관리자에 대한 액세스를 제공해야 함
    
    → **CloudWatch 콘솔에서 대시보드를 공유합니다. 제품 관리자의 이메일 주소를 입력하고 공유 단계를 완료합니다. 대시보드에 대한 공유 가능한 링크를 제품 관리자에게 제공하십시오.**
    
    - AWS 계정에 직접 액세스할 수 없는 사람들과 CloudWatch 대시보드를 공유할 수 있습니다.
    - 대시보드를 공유할 때 다음 세 가지 방법으로 대시보드를 볼 수 있는 사람을 지정할 수 있습니다.

**AWS Managed Microsoft AD**
- 회사는 AWS Organizations를 사용하여 중앙에서 계정을 관리
- 회사의 보안 팀은 회사의 모든 계정에 SSO(Single Sign On) 솔루션이 필요
- 사내 자체 관리 Microsoft Active Directory에서 사용자 및 그룹을 계속 관리해야 함
    
    → **AWS SSO 콘솔에서 AWS Single Sign On(AWS SSO) 을 활성화합니다. Microsoft Active Directory 용 AWS Directory Service를 사용하여 회사의 자체 관리형 Microsoft Active Directory를 AWS SSO와 연결하는 양방향 포리스트 트러스트를 생성합니다.**
    
    - AWS Organizations 로 SSO 설정하여 Active Directory 사용 가능
    - AWS IAM Identity Center(AWS SSO의 후속 서비스)를 설정하여 Active Directory를 통해 AWS 계정 및 리소스에 대한 액세스를 제공하며, 별도의 작업 역할에 따라 권한을 사용자 지정
    - AWS Managed Microsoft AD는 수신, 발신 및 양방향의 세 가지 신뢰 관계 방향을 모두 지원
    - AWS Managed Microsoft AD는 외부 및 포리스트 트러스트를 모두 지원

**NLB, AWS Global Acceleratior**
- 회사는 UDP 연결을 사용하는 VoIP(Voice over Internet Protocol) 서비스를 제공
- 이 서비스는 Auto Scaling 그룹에서 실행되는 Amazon EC2 인스턴스로 구성
- 여러 AWS 리전에 배포
- 지연 시간이 가장 짧은 리전으로 사용자를 라우팅
- 지역 간 자동 장애 조치가 필요
    
    → **NLB(Network Load Balancer) 및 연결된 대상 그룹을 배포합니다. 대상 그룹을 Auto Scaling 그룹과 연결합니다. 각 리전에서 NLB를 AWS Global Accelerator 엔드포인트로 사용합니다.**
    
    - UDP 연결을 사용한다고 했으므로 NLB.
    - 대기 시간이 가장 짧은 리전으로 라우팅 + UDP 사용 = AWS Global Accelerator
    - AWS Global Accelerator에서 제공하는 고정 IP 주소와 AWS 엣지 로케이션의 애니캐스트를 리전별 AWS 리소스 또는 엔드포인트(예 : Network Load Balancer, Application Load Balancer EC2 인스턴스 및 탄력적 IP 주소)에 연결할 수 있음
    - IP 주소는 AWS 엣지 로케이션에서 애니캐스트 되므로 사용자와 가까운 AWS 글로벌 네트워크에 온보딩 기능을 제공

**Q30**
- 개선 도우미가 활성화된 MySQL DB 인스턴스용 범용 Amazon RDS RDS에서 매월 리소스 집약적 테스트를 실행
- 테스트는 한 달에 한 번 48시간 동안 지속되며 데이터베이스를 사용하는 유일한 프로세스
- DB 인스턴스의 컴퓨팅 및 메모리 속성을 줄이지 않고 테스트 실행 비용을 줄이려고 함
    
    → **테스트가 완료되면 스냅샷을 만듭니다. DB 인스턴스를 종료하고 필요한 경우 스냅샷을 복원합니다.**
    
    - 스냅샷으로 보관해서 저장하면 스냅샷 용량만큼만 비용이 부과됨

**AWS Config**
- AWS에서 웹 애플리케이션을 호스팅하는 회사는 모든 Amazon EC2 인스턴스를 보장하기를 원함
- Amazon RDS DB 인스턴스. Amazon Redshift 클러스터는 태그로 구성
- 이 검사를 구성하고 운영하는 노력을 최소화
    
    → **AWS Config 규칙을 사용하여 적절하게 태그가 지정되지 않은 리소스를 정의하고 감지합니다.**
    
    - 사후 대응적 거버넌스는 Resource Groups Tagging API, AWS Config Rules, 사용자 지정 스크립트 등의 도구를 사용하여 제대로 태그가 지정되지 않은 리소스를 찾음
    - 모든 Amazon EC2 인스턴스, Amazon RDS DB 인스턴스 및 Amazon Redshift 클러스터가 태그로 구성되도록 하려면 솔루션 설계자가 AWS Config 규칙을 사용하여 적절하게 태그가 지정되지 않은 리소스를 정의하고 감지해야 함

**Amazon S3**
- 개발 팀은 다른 팀이 액세스할 웹사이트를 호스팅해야 함
- 웹사이트 콘텐츠는 HTML, CSS, 클라이언트 측 JavaScript 및 이미지로 구성
- 웹 사이트 호스팅에 가장 비용 효율적인 방법
    
    → **Amazon S3 버킷을 생성하고 거기에서 웹 사이트를 호스팅합니다.**
    
    - 정적 웹 사이트에서 웹 페이지는 사전 구축된 서버에 의해 반환
    - 웹 페이지는 변경 없이 서버에 의해 반환되므로 정적 웹 사이트는 빠름
    - 호스트가 다른 언어로 서버 측 처리를 지원할 필요가 없기 때문에 비용이 적게 듬
    - Amazon S3를 사용하여 웹 서버를 구성하거나 관리할 필요 없이 정적 웹 사이트를 호스팅할 수 있음