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
    
    → **Amazon S3와 함께 Amazon Athena를 직접 사용하여 필요에 따라 쿼리를 실행**
    
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

**Amazon Kinesis Data Streams**
- 회사는 AWS에서 온라인 마켓플레이스 웹 애플리케이션을 실행
- 이 애플리케이션은 피크 시간에 수십만 명의 사용자에게 서비스를 제공
- 회사는 수백만 건의 금융 거래 세부 정보를 다른 여러 내부 애플리케이션과 공유할 수 있는 확장 가능한 거의 실시간 솔루션이 필요
- 지연 시간이 짧은 검색을 위해 문서 데이터베이스에 저장하기 전에 민감한 데이터를 제거하기 위해 트랜잭션을 처리해야 함
    
     → **트랜잭션 데이터를 Amazon Kinesis Data Streams로 스트리밍합니다. AWS Lambda 통합을 사용하여 모든 트랜잭션에서 민감한 데이터를 제거한 다음 Amazon DynamoDB에 트랜잭션 데이터를 저장합니다. 다른 애플리케이션은 Kinesis 데이터 스트림의 트랜잭션 데이터를 사용할 수 있습니다.**
    
    - 피크 시간에 수십만 명의 사용자에게 서비스 제공 = Kinesis 사용
    - Amazon Kinesis DataStreams를 사용하면 특수 요구에 맞춰 스트리밍 데이터를 처리 또는 분석하는 사용자 지정 애플리케이션을 구축
    - 수십 만개의 소스에서 클릭 스트림, 애플리케이션 로그, 소셜 미디어와 같은 다양한 유형의 데이터를 Kinesis 데이터 스트림에 추가할 수 있음
    - 몇 초 안에 애플리케이션에서 스트림의 해당 데이터를 읽고 처리할 수 있음
    - 확장성과 내구성이 뛰어난 실시간 데이터 스트리밍 서비스
    - 웹사이트 클릭 스트림, 데이터베이스 이벤트 스트림, 금융 거래, 소셜 미디어 피드, IT 로그 및 위치 추적 이벤트와 같은 수십만 개의 소스에서 초당 기가바이트의 데이터를 지속적으로 캡처할 수 있음

**AWS Config, AWS CloudTrail**
- 회사는 AWS에서 다중 계층 애플리케이션을 호스팅
- 규정 준수, 거버넌스, 감사 및 보안을 위해 회사는 AWS 리소스의 구성 변경 사항을 추적하고 이러한 리소스에 대한 API 호출 기록을 기록해야 함
    
    → **AWS Config를 사용하여 구성 변경을 추적하고 AWS CloudTrail을 사용하여 API 호출을 기록합니다.**
    
    - 리소스 구성 사항 변경 추적 = AWS Config
    - 리소스 내역 기록 = CloudTrail
    - AWS Config는 AWS 리소스 인벤토리, 구성 기록, 구성 변경 알림을 제공하여 보안 및 거버넌스를 실현하는 완벽한 관리형 서비스
    - AWS Cloudtrail은 사용자 활동 및 API 사용을 추적하여 감사, 보안 모니터링 및 운영 문제 해결을 지원
    - CloudTrail은 AWS 인프라 전체에서 작업과 관련된 계정 활동을 로그하고 지속적으로 모니터링하고 보존하여 스토리지, 분석 및 해결 작업을 제어할 수 있도록 함

**AWS Shield Advanced**
- 한 회사가 AWS 클라우드에서 공개 웹 애플리케이션 출시를 준비하고 있음
- 아키텍처는 Elastic Load Balancer(ELB) 뒤의 VPC 내 Amazon EC2 인스턴스로 구성
- DNS에는 타사 서비스가 사용
- 회사의 솔루션 설계자는 대규모 DDoS 공격을 감지하고 보호하기 위한 솔루션을 권장해야 함
    
    → **AWS Shield Advanced를 활성화하고 ELB를 할당합니다.**
    
    - AWS Shield Advanced는 정교한 대규모 DDoS 공격에 대한 추가 보호 및 완화, 실시간에 가까운 공격에 대한 가시성, 웹 애플리케이션 방화벽 AWS WAF와의 통합을 제공
    - DDoS 관련 급증 시 Amazon Elastic Compute Cloud(EC2), Elastic Load
    Balancing(ELB), Amazon CloudFront, AWS Global Accelerator 및 Amazon Route 53 요금 보호를 제공합니다.

**AWS KMS**
- 애플리케이션은 두 AWS 리전의 Amazon S3 버킷에 데이터를 저장
- 회사는 AWS Key Management Service(AWS KMS) 고객 관리형 키를 사용하여 S3 버킷에 저장된 모든 데이터를 암호화해야 함
- 두 S3 버킷의 데이터는 동일한 KMS 키로 암호화 및 복호화해야 합니다.
- 데이터와 키는 두 지역 각각에 저장되어야 합니다
    
    → **고객 관리형 다중 지역 KMS 키를 생성합니다. 각 리전에서 S3 버킷을 생성합니다. S3 버킷 간의 복제를 구성합니다. 클라이언트 측 암호화와 함께 KMS 키를 사용하도록 애플리케이션을 구성합니다.**

**AWS IAM, AWS Session Manager**
- 회사는 최근 AWS 계정의 Amazon EC2 인스턴스에서 다양한 새로운 워크로드를 출시
- 회사는 인스턴스에 원격으로 안전하게 액세스하고 관리하는 전략을 수립해야 함
- 회사는 기본 AWS 서비스와 함께 작동하고 AWS Well-Architected 프레임워크를 따르는 반복 가능한 프로세스를 구현해야 함
- 최소한의 운영 오버헤드로 요구 사항을 충족하는 솔루션
    
    → **각 기존 인스턴스와 새 인스턴스에 적절한 IAM 역할을 연결합니다. AWS Session Manager 를 사용하여 원격 SSH 세션을 설정**
    
    - 세션 관리자는 사용자 인스턴스에 SSH 키 또는 인증서를 유지하거나 인바운드 포트를 열도록 요구하지 않고 보안 태세를 강화함
    - AWS IAM 을 사용하여 인스턴스 액세스를 중앙에서 관리
    - 세션 관리자를 사용하면 Linux 또는 Windows EC2 인스턴스와 연결하여 각 인스턴스에서 세션을 시작한 각 사용자를 추적할 수 있음
    - 인스턴스에 액세스한 사용자와 AWS CloudTrail 을 사용한 시점을 감사할 수 있으며, 인스턴스에서 실행된 각 명령을 Amazon S3 또는 Amazon CloudWatch Logs 에 기록할 수 있음
    - Session Manager 를 사용하면 배스쳔 호스트를 운영하고 관리하기 위한 초기 투자 비용이 들지 않음

**AWS CloudFront**
- 회사는 Amazon S3 에서 정적 웹 사이트를 호스팅하고 DNS 에 Amazon Route 53을 사용하고 있음
- 웹 사이트는 전 세계적으로 수요가 증가하고 있음
- 웹사이트에 액세스하는 사용자의 대기 시간을 줄여야
- 요구 사항을 가장 비용 효율적으로 충족
    
    → **S3 버킷 앞에 Amazon CloudFront 배포를 추가합니다. CloudFront 배포를 가리키도록 Route 53 항목을 편집**
    
    - 비용을 효과적으로 관리하는 동시에 애플리케이션의 성능과 보안까지 최적화 하려면 Amazon CloudFront를 설정해 S3 버킷과 함께 사용하면서
        
        콘텐츠를 제공하고 보호하는 것이 좋음
        
    - CloudFront 는 전 세계의 정적/동적 웹 콘텐츠, 비디오 스트림 및 API 를 안전하게 대규모로 전송할 수 있는 콘텐츠 전송 네트워크(CDN) 서비스
    - CloudFront 에서 데이터를 전송하면 설계상 S3 에서 직접 사용자에게 전송하는 것보다 더욱 비용 효율적임
    - Amazon CloudFront 는 전 세계 엣지 로케이션에서 콘텐츠를 캐싱하여 콘텐츠에 액세스하는 사용자에게 짧은 지연 시간과 빠른 전송 속도를 제공하는 콘텐츠 전송 네트워크(CDN)
    - S3 버킷 앞에 CloudFront 배포를 추가하면 전 세계 엣지 위치에서 정적 웹 사이트의 콘텐츠를 캐싱하여 웹 사이트에 액세스하는 사용자의 지연 
    시간을 줄임
    - CloudFront 엣지 로케이션에서 콘텐츠에 액세스하는 사용자의 데이터 전송 및 요청에 대해서만 비용을 청구
    - CloudFront 가 자동으로 확장하여 수요 증가를 처리하고 웹 사이트에 고가용성을 제공할 수 있으므로 확장성과 안정성 이점을 제공
    
**AWS** **IOPS SSD**
- 회사는 웹 사이트에서 검색 가능한 항목 저장소를 유지 관리
- 데이터는 천만 개 이상의 행이 포함된 Amazon RDS for MySQL 데이터베이스 테이블에 저장
- 데이터베이스에는 2TB 의 범용 SSD 스토리지가 있음
- 회사 웹 사이트를 통해 이 데이터에 대한 수백만 건의 업데이트가 매일 있음
- 이 회사는 일부 삽입 작업이 10 초 이상 걸리는 것을 확인. 회사는 데이터베이스 스토리지 성능이 문제라고 판단
- 이 성능 문제를 해결하는 솔루션
    
    → **스토리지 유형을 프로비저닝된 IOPS SSD 로 변경**
    
    - 프로비저닝된 IOPS 볼륨은 솔리드 스테이트 드라이브(SSD)로 지원되며 중요한 I/O 집약적인 데이터베이스 애플리케이션을 위해 설계된 
    최고 성능의 EBS 볼륨
    - 극히 짧은 대기 시간이 필요한 IOPS 집약적 워크로드와 처리량 집약적 워크로드 모두에 이상적
    - '삽입' 작업이라고 했으므로 I/O 성능과 관련되어있음을 유추할 수 있음
    - '저장소 성능'이 문제라고 판단했고, 범용 'SSD' 스토리지가 있다고 했음

**Amazon Kinesis Data Firehose, S3 Glacier**
- 회사에는 매일 1TB 의 상태 알림을 집합적으로 생성하는 수천 개의 에지 장치가 있음
- 각 경고의 크기는 약 2KB. 솔루션 설계자는 향후 분석을 위해 경고를 수집하고 저장하는 솔루션을 구현해야 함
- 회사는 고가용성 솔루션을 원함. 그러나 회사는 비용을 최소화해야 하며 추가 인프라 관리를 원하지 않음
- 회사는 즉각적인 분석을 위해 14 일 동안의 데이터를 유지하고 14 일이 지난 데이터를 보관하기를 원함
- 요구 사항을 충족하는 가장 운영 효율성이 높은 솔루션
    
    → **Amazon Kinesis Data Firehose 전송 스트림을 생성하여 알림을 수집합니다. Amazon S3 버킷에 알림을 전달하도록 Kinesis Data Firehose 스트림을 구성. 14 일 후에 데이터를 Amazon S3 Glacier 로 전환하도록 S3 수명 주기 구성을 설정**
    
    - 수 천 개의 Edge 장치로부터 경고 수집 및 저장 = Kinesis
    - Kinesis Firehose Delivery Stream 에서 데이터 수집
        - 다양한 유형의 소스를 사용하여 Kinesis Data Firehose 전송 스트림으로 데이터를 보낼 수 있음
    - Kinesis Firehose 에서 S3 로 데이터 전송
        - Kinesis Data Firehose 전송 스트림을 설정할 때 데이터의 최종 대상을 선택
        - 대상 옵션은 Amazon S3, Amazon OpenSearch Service 및 Amazon Redshift
    - S3 에서 Life Cycle Policy 를 사용해 S3 Glacier 로 객체 이전
        - 수명 주기 규칙을 사용하여 객체 수명 주기 동안 Amazon S3 에서 수행하려는 작업을 정의할 수 있음
        - 객체를 다른 스토리지 클래스로 이전, 객체 보관, 지정된 기간이 경과한 후 객체 삭제

**Amazon AppFlow, Amazon SNS**
- 회사의 애플리케이션은 데이터 수집을 위해 여러 SaaS(Software-as-a-Service) 소스와 통합됨
- Amazon EC2 인스턴스를 실행하여 데이터를 수신하고 분석을 위해 데이터를 Amazon S3 버킷에 업로드 함
- 데이터를 수신하고 업로드하는 동일한 EC2 인스턴스도 업로드가 완료되면 사용자에게 알림을 보냄
- 느린 응용 프로그램 성능을 발견했으며 가능한 한 성능을 개선하려고 함
- 최소한의 운영 오버헤드로 이러한 요구 사항을 충족하는 솔루션
    
    → **Amazon AppFlow 흐름을 생성하여 각 SaaS 소스와 S3 버킷 간에 데이터를 전송합니다. S3 버킷에 업로드가 완료되면 Amazon Simple Notification Service(Amazon SNS) 주제에 이벤트를 보내도록 S3 이벤트 알림을 구성**
    
    - Amazon AppFlow 는 Salesforce, SAP, Zendesk, Slack 및 ServiceNow 와 같은 SaaS(Software-as-a-Service) 애플리케이션과 Amazon S3 및 Amazon Redshift 와 같은 AWS 서비스 간에 데이터를 안전하게 전송할 수 있는 완전 관리형 통합 서비스
    - SaaS = Appflow. Appflow 는 완전 관리형 통합 서비스이기 때문에 운영 오버헤드가 적음. Amazon AppFlow 는 클릭 몇 번으로 Salesforce, Marketo, Slack 및 ServiceNow 와 같은 SaaS(Software-as-a-Service) 애플리케이션과 Amazon S3 및 Amazon Redshift 와 같은 AWS 서비스 간에 
    데이터를 안전하게 전송할 수 있게 해 주는 완전 관리형 통합 서비스

**Amazon VPC Gateway Endpoint**
- 회사는 단일 VPC 의 Amazon EC2 인스턴스에서 고가용성 이미지 처리 애플리케이션을 실행
- EC2 인스턴스는 여러 가용 영역의 여러 서브넷 내에서 실행됨
- EC2 인스턴스는 서로 통신하지 않음
- 그러나 EC2 인스턴스는 Amazon S3 에서 이미지를 다운로드하고 단일 NAT 게이트웨이를 통해 Amazon S3 에 이미지를 업로드함
- 회사는 데이터 전송 요금에 대해 우려하고 있음
- 회사가 지역 데이터 전송 요금을 피할 수 있는 가장 비용 효율적인 방법
    
    → **Amazon S3 용 게이트웨이 VPC 엔드포인트를 배포함**
    
    - 데이터 전송 요금이 걱정되니 전용 전송 통로를 뚫으면 됨. VPC-S3 간 전용 통로는 S3 VPC Gateway Endpoint.
    - S3 용 게이트웨이 VPC 엔드포인트를 배포함으로써 회사는 인터넷 게이트웨이나 NAT 게이트웨이를 거치지 않고 VPC 와 S3 사이에 직접 연결을 설정할 수 있음
    - 이렇게 하면 EC2 와 S3 사이의 트래픽이 Amazon 네트워크 내에 머물면서 지역 데이터 전송 요금을 피할 수 있음

**AWS Direct Connect**
- 회사에 Amazon S3 에 백업 되는 시간에 민감한 대량의 데이터를 생성하는 온프레미스 애플리케이션이 있음
- 애플리케이션이 성장했고 인터넷 대역폭 제한에 대한 사용자 불만이 있음
- 솔루션 설계자는 Amazon S3 에 대한 적시 백업을 허용하고 내부 사용자의 인터넷 연결에 미치는 영향을 최소화하는 장기 솔루션을 설계해야 함
    
    → **새 AWS Direct Connect 연결을 설정하고 이 새 연결을 통해 백업 트래픽을 직접 연결함**
    
    - Direct Connect 는 전용선을 통과하기 때문에 인터넷에 전송중인 데이터가 노출되지 않음
    - 회사의 온프레미스 애플리케이션에 대한 대역폭 제한 문제를 해결하고 내부 사용자 연결에 대한 영향을 최소화하려면 이 새로운 연결을 통해 
    백업 트래픽을 전달하도록 새로운 AWS Direct Connect 연결을 설정해야 함
    - 회사의 데이터 센터와 AWS 간에 안전한 고속 연결을 제공하여 회사가 인터넷 대역폭을 사용하지 않고 데이터를 빠르게 전송할 수 있도록 함

**Amazon S3 버전 관리 및 MFA 삭제**
- 회사에 중요한 데이터가 포함된 Amazon S3 버킷이 있음
- 회사는 우발적인 삭제로부터 데이터를 보호해야 함
    
    → **S3 버킷에서 버전 관리를 활성화함, S3 버킷에서 MFA 삭제를 활성화함**
    
    - 버전 관리는 실수로 삭제했을 때 이전 버전의 파일을 불러올 수 있도록 해줌
    - S3 버킷의 데이터를 실수로 삭제하지 않도록 보호하려면 S3 버킷에 있는 모든 객체의 모든 버전을 보존, 검색 및 복원할 수 있는 버전 관리를 
    활성화해야 함
    - Amazon S3 의 버전 관리는 동일 버킷 내에 여러 개의 객체 변형을 보유하는 수단
    - MFA Delete 는 함부로 삭제하지 못하도록 막음
    - MFA Delete 는 다음 작업에 대해 추가 인증을 요구함
        - 버킷의 버전 관리 상태 변경, 객체 버전 영구 삭제
    - S3 버킷에서 MFA(다단계 인증) 삭제를 활성화하면 버킷의 객체를 삭제하기 위해 사용자의 액세스 키 외에 인증 토큰을 요구함으로써 추가 
    보호 계층이 추가됨

**AWS Simple Queue Service, AWS Lambda**
- 회사에는 다음으로 구성된 데이터 수집 워크플로가 있음
    - 새로운 데이터 전송에 대한 알림을 위한 Amazon Simple Notification Service(Amazon SNS) 주제
    - 데이터를 처리하고 메타데이터를 기록하는 AWS Lambda 함수
- 회사는 네트워크 연결 문제로 인해 수집 워크플로가 때때로 실패하는 것을 관찰함
- 이러한 장애가 발생하면 회사에서 수동으로 작업을 다시 실행하지 않는 한 Lambda 함수는 해당 데이터를 수집하지 않음
- Lambda 함수가 향후 모든 데이터를 수집하도록 하려면 솔루션 설계자가 취해야 하는 작업 조합은
    
    → **Amazon Simple Queue Service(Amazon SQS) 대기열을 생성하고 SNS 주제를 구독
        Amazon Simple Queue Service(Amazon SQS) 대기열에서 읽도록 Lambda 함수를 수정함**
    
    - 네트워크 연결 문제로 데이터 수집이 잠시 실패하는 현상이 일어남. 이런 경우 데이터 손실이 일어날 위험성이 크므로 데이터를 보관해둘 곳이 
    필요하고, 대책으로는 SQS Queue 가 적절. 또한 SQS Queue 에 머물러 있는 작업들은 Lambda로 처리 가능
    - SQS를 사용하면 메시지 손실 위험을 감수하거나 다른 서비스를 가동할 필요 없이 소프트웨어 구성 요소 간에 모든 볼륨의 메시지를 전송, 
    저장 및 수신할 수 있음
    - Lambda 함수를 사용하여 Amazon Simple Queue Service(Amazon SQS) 대기열의 메시지를 처리할 수 있음
    - SQS를 통해 알림과 처리를 분리할 수 있으므로 처리 Lambda 함수가 실패하더라도 나중에 추가 처리를 위해 메시지가 대기열에 남아 있음
    - SNS에서 직접 읽지 않고 SQS 대기열에서 읽도록 Lambda 함수를 수정함. 이 분리는 재시도 및 내결함성을 허용하고 모든 메시지가 Lambda 
    함수에 의해 처리되도록 함

**Amazon Macie, Amazon SNS**
- 회사에 매장에 마케팅 서비스를 제공하는 애플리케이션이 있음
- 서비스는 매장 고객의 이전 구매를 기반
- 상점은 SFTP를 통해 거래 데이터를 회사에 업로드하고 데이터를 처리 및 
분석하여 새로운 마케팅 제안을 생성함
- 일부 파일의 크기는 200GB를 초과할 수 있음
- 최근에 회사는 일부 상점에서 포함되어서는 안 되는 개인 식별 정보(PII)가 포함된 파일을 업로드했음을 발견
- 회사는 PII가 다시 공유될 경우 관리자에게 경고를 주기를 원합니다. 회사는 또한 문제 해결을 자동화하기를 원함
- 최소한의 개발 노력으로 이러한 요구 사항을 충족해야 함
    
    → Amazon S3 버킷을 보안 전송 지점으로 사용합니다. Amazon Macie를 사용하여 버킷의 객체를 스캔합니다. 객체에 PII가 포함된 경우 Amazon Simple Notification Service(Amazon SNS)를 사용하여 관리자에게 PII가 포함된 객체를 제거하라는 알림을 트리거
    
    - Amazon Macie는 AWS에서 PII와 같은 민감한 데이터를 자동으로 검색, 분류 및 보호하는 관리형 서비스
    - S3에서 Macie를 활성화하면 업로드된 객체에서 PII를 검색할 수 있음
    - Amazon Macie는 기계 학습 및 패턴 일치를 사용하여 Amazon S3에 저장된 중요한 데이터를 검색하고 보호하는 완전 관리형 데이터 보안 및 데이터 개인 정보 보호 서비스
    - Amazon Macie에는 이미 다양한 형식의 PIIPII를 탐지할 수 있는 사전 구축된 데이터 분류 규칙이 있으므로 이 접근 방식은 최소한의 개발 노력이 필요
    
**AWS Region, AWS Availability Zone**
- 회사는 1주일 동안 진행될 예정된 이벤트를 위해 특정 AWS 리전의 3개의 
특정 가용 영역에서 보장된 Amazon EC2 용량이 필요
- EC2 용량을 보장하기 위해 회사는 무엇을 해야
    
    → **필요한 지역과 33개의 가용 영역을 지정하는 온디맨드 용량 예약을 생성함**
    
    - 용량 예약을 생성할 때 가용 영역을 지정

**Amazon Elastic File System(Amazon EFS)**
- 회사 웹 사이트는 항목 카탈로그에 Amazon EC2 인스턴스 스토어를 사용
- 회사는 카탈로그의 가용성이 높고 카탈로그가 내구성 있는 위치에 저장되기를 원함
    
    → **카탈로그를 Amazon Elastic File System(Amazon EFS) 파일 시스템으로 이동함**
    
    - Amazon EFS는 필요에 따라 확장할 수 있도록 구축된 완전 관리형, 가용성 및 내구성이 뛰어난 파일 시스템
    - Amazon EFS를 사용하면 다양한 가용 영역에 있는 여러 EC2 인스턴스에서 카탈로그 데이터를 저장하고 액세스할 수 있으므로 고가용성이 보장
    - Amazon EFS EFS는 여러 가용 영역 내에서 파일을 자동으로 중복 저장하므로 내구성 있는 스토리지 옵션이 됨

**Amazon S3 Glacier Instant Retrieve**
- 회사는 매월 통화 기록 파일을 저장함
- 사용자는 통화 후 1년 이내에 파일에 무작위로 액세스하지만 1년 이후에는 파일에 자주 액세스하지 않음
- 회사는 사용자에게 1년 미만의 파일을 가능한 한 빨리 쿼리하고 검색할 수 있는 기능을 제공하여 솔루션을 최적화하려고 함
- 오래된 파일을 검색하는 데 있어 지연은 허용
- 이러한 요구 사항을 가장 비용 효율적으로 충족해야 함
    
    → **Amazon S3 Intelligent Tiering에 개별 파일을 저장함. S3 수명 주기 정책을 사용하여 1년 후 파일을 S3 Glacier Flexible Retrieval로 이동함. Amazon Athena를 사용하여 Amazon S3에 있는 파일을 쿼리하고 검색함. S3 Glacier Select를 사용하여 S3 Glacier에 있는 파일을 쿼리하고 검색함**
    
    - 의료 이미지, 뉴스 미디어 자산 또는 유전체학 데이터와 같이 즉각적인 액세스가 필요한 아카이브 데이터의 경우 S3 Glacier Instant Retrieve 스토리지 클래스를 선택
    - S3 Glacier Instant Retrieve 스토리지 클래스는 밀리초 검색으로 최저 
    비용의 스토리지를 제공함
    - 즉각적인 액세스가 필요하지는 않지만 백업 또는 재해 복구 사용 사례와 같이 비용 없이 대용량 데이터 세트를 검색할 수 있는 유연성이 필요한 아카이브 데이터의 경우 S3 Glacier Flexible Retrieve(이전의 S3 Glacier) 를 선택함
    - 몇 분 내에 검색하거나 5-12시간 내에 대량 검색을 무료로 제공

**AWS Systems Manager Run Command**
- 회사에 1,000개의 Amazon EC2 Linux 인스턴스에서 실행되는 프로덕션 워크로드가 있음
- 워크로드는 타사 소프트웨어에 의해 구동됨
- 회사는 중요한 보안 취약성을 수정하기 위해 가능한 한 빨리 모든 EC2 
인스턴스에서 타사 소프트웨어를 패치해야 함
- 이러한 요구 사항을 충족하려면
    
    → **AWS Systems Manager Run Command를 사용하여 모든 EC2 인스턴스에 패치를 적용하는 사용자 지정 명령을 실행**
    
    - 리소스 그룹을 통해 한 번에 여러 인스턴스를 업데이트 가능함
    - 리소스 그룹이 명령 대상으로 지원됨에 따라 해당 리소스 그룹에 속한 모든 관리형 인스턴스에서 관리 및 임시 작업을 자동화할 수 있음

**AWS Simple Email Service, AWS Lambda, AWS EvenetBridge**
- 회사는 REST API로 검색하기 위해 주문 배송 통계를 제공하는 애플리케이션을 개발 중
- 회사는 배송 통계를 추출하고 데이터를 읽기 쉬운 HTML 형식으로 구성하고 매일 아침 여러 이메일 
주소로 보고서를 보내려고 함
    
    → **Amazon Simple Email Service(Amazon SES)를 사용하여 데이터 형식을 지정하고 보고서를 이메일로 보냄
    → AWS Lambda 함수를 호출하여 데이터에 대한 애플리케이션의 API를 쿼리하는 Amazon EventBridge(Amazon CloudWatch Events) 예약 이벤트를 생성함**
    
    - AWS Lambda를 사용하여 배송 통계를 추출하고 데이터를 HTML 형식으로 구성할 수 있음
    - AWS Lambda를 사용하여 배송 통계를 추출하고 데이터를 HTML 형식으로 구성할 수 있음

**AWS 다중 AZ Auto Scaling, AWS Elastic File System**
- 회사에서 온프레미스 애플리케이션을 AWS로 마이그레이션하려고 함
- 애플리케이션은 수십 기가바이트에서 수백 테라바이트까지 다양한 크기의 출력 파일을 생성함
- 애플리케이션 데이터는 표준 파일 시스템 구조로 저장되어야 함
- 회사는 자동으로 확장되는 솔루션을 원함. 고가용성이며 최소한의 운영 오버헤드가 필요
    
    → **다중 AZ Auto Scaling 그룹의 Amazon EC2 인스턴스로 애플리케이션을 마이그레이션함. 스토리지에 Amazon Elastic File System(Amazon EFS)을 사용함**
    
    - EFS 는 표준 파일 시스템으로 자동 확장되며 가용성이 높음
    - EBS는 여러 EC2 인스턴스에서 동시 접속할 수 없다는 단점이 치명적임
    - Amazon Elastic File System 은 전체 파일 시스템 액세스 의미 체계를 지원하는 표준 파일 시스템 
    인터페이스를 제공함

**Amazon S3 Standard, Glacier Deep Archive, Object Lock**
- 회사는 Amazon S3 에 회계 기록을 저장해야 함
- 기록은 1년 동안 즉시 액세스할 수 있어야 하며 그 후 추가로 9년 동안 보관해야 함
- 관리자 및 루트 사용자를 포함하여 회사의 그 누구도 전체 10년 동안 기록을 삭제할 수 없음
- 기록은 최대한의 복원력으로 저장해야 함
    
    → **S3 수명 주기 정책을 사용하여 1 년 후에 S3 Standard 에서 S3 Glacier Deep Archive로 레코드를 전환함. 10년 동안 규정 준수 모드에서 S3 Object Lock을 사용함**
    
    - S3 Standard: 즉시 액세스 가능
    - S3 Glacier Deep Archive: 콜드 스토리지 보관용으로 사용됨
    - Object Lock으로 객체 삭제 방지

**AWS FSx for Windows File Server**
- 회사는 AWS에서 여러 Windows 워크로드를 실행함
- 회사 직원은 두 개의 Amazon EC2 인스턴스에서 호스팅 되는 Windows 파일 공유를 사용함
- 파일 공유는 서로 간에 데이터를 동기화하고 중복 복사본을 유지함
- 회사는 사용자가 현재 파일에 액세스하는 방식을 보존하는 고가용성 및 내구성 스토리지 솔루션을
원함
    
    → **다중 AZ 구성을 사용하여 파일 공유 환경을 Windows 파일 서버용 Amazon FSx로 확장함. 모든 
    데이터를 Windows 파일 서버용 FSx 로 마이그레이션함**
    
    - Amazon FSx for Windows File Server는 완전히 네이티브로 지원되는 완전히 관리되는
    Microsoft Windows 파일 서버를 제공함

**AWS Private Subnet**
- 솔루션 설계자는 여러 서브넷을 포함하는 VPC 아키텍처를 개발 중
- Amazon EC2 인스턴스 및 Amazon RDS DB 인스턴스를 사용하는 애플리케이션을 호스팅함
- 아키텍처는 2 개의 가용 영역에 있는 6 개의 서브넷으로 구성됨
- 각 가용영역에는 퍼블릭 서브넷, 프라이빗 서브넷 및 데이터베이스용 전용 서브넷이 포함됨
- 프라이빗 서브넷에서 실행되는 EC2 인스턴스만 RDS 데이터베이스에 액세스할 수 있음
    
    → **프라이빗 서브넷의 인스턴스에 할당된 보안 그룹의 인바운드 트래픽을 허용하는 보안 그룹을 생성함. 보안 그룹을 DB 인스턴스에 연결함**
    
    - 프라이빗 서브넷의 인스턴스에 할당된 보안 그룹의 인바운드 트래픽을 허용하는 보안 그룹을 생성하면 프라이빗 서브넷에서 실행되는 EC2만 RDS 데이터베이스에 액세스할 수 있음.
    - 보안 그룹을 DB 와 연결하여 지정된 보안 그룹에 속한 인스턴스로만 접근을 제한함

**Amazon Certificate Manager**
- 회사는 Amazon Route 53에 도메인 이름을 등록함
- 회사는 ca-central-1 리전의 Amazon API Gateway를 백엔드 마이크로서비스 API의 공용 인터페이스로 사용함
- 타사 서비스는 API를 안전하게 사용함
- 회사는 타사 서비스에서 HTTPS를 사용할 수 있도록 회사의 도메인 이름 및 해당 인증서로 API 게이트웨이 URL을 설계하려고 함
    
    → **리전 API 게이트웨이 엔드포인트를 생성함. API Gateway 엔드포인트를 회사의 도메인 이름과 연결함. 회사의 도메인 이름과 연결된 공인 인증서를 동일한 리전의 AWS Certificate Manager(ACM)로 가져옴. API Gateway 엔드포인트에 인증서를 연결함. API Gateway 엔드포인트로 트래픽을 라우팅하도록 Route 53 을 구성함.**
    
    - 지역 API 게이트웨이 엔드포인트 생성
        - 이를 통해 회사는 지역에 특정한 엔드포인트를 생성할 수 있음
    - API 게이트웨이 엔드포인트를 회사의 도메인 이름과 연결
        - 이렇게 하면 회사에서 API 게이트웨이 URL 에 자체 도메인 이름을 사용할 수 있음
    - 회사의 도메인 이름과 연결된 공인 인증서를 동일한 리전의 AWS Certificate Manager(ACM)로 가져옴
        - 이렇게 하면 회사에서 API 와의 보안 통신을 위해 HTTPS를 사용할 수 있음
    - API Gateway 엔드포인트에 인증서 첨부
        - 회사에서 API Gateway URL 보안을 위해 인증서를 사용할 수 있음
    - 트래픽을 API 게이트웨이 엔드포인트로 라우팅하도록 Route 53 구성
        - 이를 통해 회사는 Route 53을 사용하여 회사의 도메인 이름을 사용하는 API 게이트웨이 URL로 트래픽을 라우팅할 수 있음

**Amazon Rekognition**
- 회사에서 인기 있는 소셜 미디어 웹사이트를 운영하고 있음
- 웹사이트는 사용자에게 이미지를 업로드하여 다른 사용자와 공유할 수 있는 기능을 제공함
- 회사는 이미지에 부적절한 콘텐츠가 포함되지 않았는지 확인하고 싶음
    
    → **Amazon Rekognition을 사용하여 부적절한 콘텐츠를 감지함. 신뢰도가 낮은 예측에는 인적 검토를 사용함**
    
    - Amazon Rekognition을 사용하여 부적절하거나 원치 않거나 불쾌감을 주는 콘텐츠를 감지할 수 있음

**Amazon Fargate, Amazon Elastic Container Service**
- 회사는 확장성 및 가용성에 대한 요구 사항을 충족하기 위해 컨테이너에서 중요한 응용프로그램을 실행하려고 함
- 회사는 중요한 응용 프로그램의 유지 관리에 집중하는 것을 선호함
- 회사는 컨테이너화된 워크로드를 실행하는 기본 인프라의 프로비저닝 및 관리에 대한 책임을 원하지 않음
    
    → **AWS Fargate 에서 Amazon Elastic Container Service(Amazon ECS)를 사용함**
    
    - AWS에서 컨테이너라고 하면 ECS, ECS라고 하면 일단 Fargate부터 떠올리면 됨
    - Amazon EC2 인스턴스의 서버나 클러스터를 관리할 필요 없이 컨테이너를 실행하기 위해 Amazon ECS에 사용할 수 있는 기술

**Amazon Kinesis Data Streams, Amazon Kinesis Data Firehose, Amazon Redshift**
- 회사는 300 개 이상의 글로벌 웹사이트 및 애플리케이션을 호스팅 함
- 회사는 매일 30TB 이상의 클릭스트림 데이터를 분석할 플랫폼이 필요
- 솔루션 설계자 클릭스트림 데이터를 전송하고 처리하기 위해 해야할 일
    
    → **Amazon Kinesis Data Streams 에서 데이터를 수집함. Amazon Kinesis Data Firehose를 사용하여 Amazon S3 데이터 레이크로 데이터를 전송함.  분석을 위해 Amazon Redshift 에 데이터를 로드함**
    
    - 대량의 스트림 데이터 수집 = Kinesis Data Streams
    - Amazon Kinesis Firehose는 버퍼링된 데이터를 Amazon Kinesis Data Streams에서 Amazon Simple Storage Service (Amazon S3) 의 영구 
    스토리지로 자동 이동함
    - 분석 쿼리 및 복잡한 데이터 과학 작업을 위해 Amazon Redshift로 전송

**AWS Application Load Balancer**
- 회사에 AWS 에서 호스팅 되는 웹 사이트가 있음
- 웹 사이트는 HTTP 와 HTTPS 를 별도로 처리하도록 구성된 ALB(Application Load Balancer) 뒤에 있음
- 회사는 요청이 HTTPS 를 사용하도록 모든 요청을 웹사이트로 전달하려고 함
    
    → **ALB 에서 리스너 규칙을 생성하여 HTTP 트래픽을 HTTPS 로 리디렉션함**
    
    - 쿼리 문자열 조건을 사용하여 쿼리 문자열의 키/값 페어 또는 값을 기반으로 요청을 라우팅하는 규칙을 구성할 수 있음
    - HTTP 요청을 HTTPS 로 리디렉션하는 HTTP 리스너 규칙 생성
    - HTTPS 리스너 생성
    - Application Load Balancer 의 보안 그룹이 443 의 트래픽을 허용하는지 확인

**AWS Application Load Balancer**
- 회사에 AWS 에서 호스팅 되는 웹 사이트가 있음
- 웹 사이트는 HTTP 와 HTTPS 를 별도로 처리하도록 구성된 ALB(Application Load Balancer) 뒤에 있음
- 회사는 요청이 HTTPS 를 사용하도록 모든 요청을 웹사이트로 전달하려고 함
    
    → **ALB 에서 리스너 규칙을 생성하여 HTTP 트래픽을 HTTPS 로 리디렉션함**
    
    - 쿼리 문자열 조건을 사용하여 쿼리 문자열의 키/값 페어 또는 값을 기반으로 요청을 라우팅하는 규칙을 구성할 수 있음
    - HTTP 요청을 HTTPS 로 리디렉션하는 HTTP 리스너 규칙 생성
    - HTTPS 리스너 생성
    - Application Load Balancer 의 보안 그룹이 443 의 트래픽을 허용하는지 확인

**AWS Secrets Manager**
- 회사가 AWS 에서 2 계층 웹 애플리케이션을 개발하고 있습니다
- 회사 개발자는 백엔드 Amazon RDS 데이터베이스에 직접 연결되는 Amazon EC2 인스턴스에 애플리케이션을 배포했습니다
- 회사는 애플리케이션에 데이터베이스 자격 증명을 하드코딩해서는 안 됩니다
- 회사는 정기적으로 데이터베이스 자격 증명을 자동으로 교체하는 솔루션을 구현해야합니다
    
    → **데이터베이스 자격 증명을 AWS Secrets Manager 에 암호로 저장합니다. 보안 비밀에 대한 자동 순환을 켭니다. EC2 역할에 필요한 권한을 연결하여 보안 암호에 대한 액세스 권한을 부여합니다.**
    
    - 애플리케이션에 자격증명 하드코딩 안 됨 = Secrets Manager
    - Secrets Manager를 사용하면 애플리케이션 소스 코드에서 하드 코딩된 자격 증명을 제거하고 애플리케이션 자체에 자격 증명을 저장하지 않음으로써 보안 태세를 개선할 수 있습니다.
    - 사용자의 개입 없이 지정한 일정에 따라 자동으로 보안 암호를 교체하도록 Secrets Manager를 구성할 수 있습니다. 교체는 AWS Lambda 함수를 사용하여 정하고 실행합니다.

**AWS Certificate Manager, Amazon EventBridge**
- 회사에서 AWS 에 새로운 공개 웹 애플리케이션을 배포하고 있습니다. 애플리케이션은 ALB(Application Load Balancer) 뒤에서 실행됩니다
- 애플리케이션은 외부 CA(인증기관)에서 발급한 SSL/TLS 인증서를 사용하여 에지에서 암호화해야 합니다
- 인증서가 만료되기 전에 매년 인증서를 교체해야 합니다
    
    → **AWS Certificate Manager(ACM)를 사용하여 SSL/TLS 인증서를 가져옵니다. 인증서를 ALB 에 적용합니다. Amazon EventBridge(Amazon CloudWatch Events)를 사용하여 인증서가 만료될 때 알림을 보냅니다. 인증서를 수동으로 교체합니다.**
    

**Amazon S3, AWS Lambda**
- 회사는 AWS 에서 인프라를 실행하고 문서 관리 애플리케이션에 대해 700,000 명의 등록 기반을 보유하고 있습니다
- 회사는 큰 .pdf 파일을 .jpg 이미지 파일로 변환하는 제품을 만들려고 합니다
- .pdf 파일의 크기는 평균 5MB 입니다
- 회사는 원본 파일과 변환 파일을 보관해야 합니다
- 솔루션 설계자는 시간이 지남에 따라 빠르게 증가할 수요를 수용할 수 있는 확장 가능한 솔루션을 설계해야 합니다
    
    → **.pdf 파일을 Amazon S3 에 저장합니다. AWS Lambda 함수를 호출하여 파일을 .jpg 형식으로 변환하고 Amazon S3 에 다시 저장하도록 S3 PUT 
    이벤트를 구성합니다.**
    

**Amazon FSx File Gateway**
- 회사는 온프레미스에서 실행되는 Windows 파일 서버에 5TB 이상의 파일 데이터를 가지고 있습니다
- 사용자와 애플리케이션은 매일 데이터와 상호 작용합니다
- 회사는 Windows 워크로드를 AWS 로 이전하고 있습니다
- 회사가 이 프로세스를 계속함에 따라 회사는 최소 지연 시간으로 AWS 및 온프레미스 파일 스토리지에 액세스할 수 있어야 합니다
- 회사는 운영 오버헤드를 최소화하고 기존 파일 액세스 패턴을 크게 변경할 필요가 없는 솔루션이 필요합니다
- 회사는 AWS 연결을 위해 AWS Site-to-Site VPN 연결을 사용합니다
    
    → **AWS 에서 Windows 파일 서버용 Amazon FSx 를 배포 및 구성합니다. 온프레미스에 Amazon FSx 파일 게이트웨이를 배포하고 구성합니다. 온프레미스 파일 데이터를 FSx 파일 게이트웨이로 이동합니다. AWS 의 Windows 파일 서버용 FSx 를 사용하도록 클라우드 워크로드를 구성합니다. FSx 파일 게이트웨이를 사용하도록 온프레미스 워크로드를 구성합니다**
    
    - Windows File Server + AWS 로 이동 = Amazon FSx File Gateway
    - Amazon FSx 파일 게이트웨이는 Amazon FSx 의 Windows 파일 공유에 대한 온프레미스 액세스를 최적화하여 사용자가 짧은 지연 시간과 공유 대역폭을 유지하면서 Windows 파일 서버용 FSx 데이터에 쉽게 액세스할 수 있도록 합니다.
    - 사용자는 액세스할 수 있는 자주 사용하는 데이터의 로컬 캐시를 활용하여 성능을 높이고 데이터 전송 트래픽을 줄일 수 있습니다.
    - 파일 읽기 및 쓰기와 같은 파일 시스템 작업은 모두 로컬 캐시에 대해 수행되는 반면 Amazon FSx 파일 게이트웨이는 변경된 데이터를 백그라운드에서 Windows 파일 서버용 FSx 와 동기화합니다.
    - 이러한 기능을 사용하면 Windows 파일 서버용 FSx에서 AWS 의 모든 온프레미스 파일 공유 데이터를 통합하고 보호되고 탄력적인 완전 관리형 파일 시스템의 이점을 누릴 수 있습니다.

**Amazon Textract, Amazon Comprehend Medical**
- 병원은 최근 Amazon API Gateway 및 AWS Lambda 와 함께 RESTful API 를 배포했습니다
- 병원은 API Gateway 및 Lambda 를 사용하여 PDF 형식 및 JPEG 형식의 보고서를 업로드합니다
- 병원은 보고서에서 보호되는 건강 정보(PHI)를 식별하기 위해 Lambda 코드를 수정해야 합니다
    
    → **Amazon Textract를 사용하여 보고서에서 텍스트를 추출합니다. Amazon Comprehend Medical을 사용하여 추출된 텍스트에서 PHI를 식별합니다**
    
    - Textract 는 OCR 같은 서비스.
    - Comprehend 는 의료용 텍스트 식별 서비스.
    - Amazon Textract 는 스캔한 문서에서 텍스트, 필기 및 데이터를 자동으로 추출하는 기계학습(ML) 서비스입니다.
    - 단순한 광학 문자 인식(OCR) 이상으로 양식 및 표의 데이터를 식별하고 이해하며 추출합니다.
    - Amazon Comprehend Medical 은 HIPAA 적격 자연어 처리(NLP) 서비스로, 미리 학습된 기계 학습을 사용하여 처방전, 처치, 진단과 같은 의료 
    텍스트에서 의료 데이터를 파악하고 추출합니다.

**Amazon S3 Standard, Amazon S3 Standard-Infrequent Access**
- 회사에 각각 크기가 약 5MB 인 많은 수의 파일을 생성하는 응용 프로그램이 있습니다
- 파일은 Amazon S3 에 저장됩니다
- 회사 정책에 따라 파일을 삭제하려면 4 년 동안 보관해야 합니다
- 파일에는 재생산하기 쉽지 않은 중요한 비즈니스 데이터가 포함되어 있으므로 즉각적인 액세스가 항상 필요합니다
- 파일은 객체 생성 후 처음 30 일 동안 자주 액세스 되지만 처음 30 일 후에는 거의 액세스 되지 않습니다
    
    → **객체 생성 후 30 일 동안 S3 Standard 에서 S3 Standard-Infrequent Access(S3 Standard-IA)로 파일을 이동하는 S3 버킷 수명 주기 정책을 생성합니다. 객체 생성 후 4 년이 지나면 파일을 삭제합니다**
    
    - 30 일 동안은 자주 액세스하므로 S3 Standard, 30 일 이후에는 자주 액세스하진 않지만 즉각적인 액세스가 필요하므로 S3 Standard-IA, 4 년이 지나면 중요한 비즈니스 데이터므로 함부로 보관해서는 안됨.

**AWS ChangeMessageVisibility API**
- 회사는 여러 Amazon EC2 인스턴스에서 애플리케이션을 호스팅합니다
- 애플리케이션은 Amazon SQS 대기열의 메시지를 처리하고 Amazon RDS 테이블에 쓰고 대기열에서 메시지를 삭제합니다
- RDS 테이블에서 가끔 중복 레코드가 발견됩니다
- SQS 대기열에는 중복 메시지가 없습니다
- 메시지가 한 번만 처리되도록 설계
    
    → **ChangeMessageVisibility API 호출을 사용하여 가시성 시간 초과를 늘립니다**
    
    - 가시성 제한 시간은 Amazon SQS 가 메시지를 반환할 때 시작됩니다.
    - 이 시간 동안 소비자는 메시지를 처리하고 삭제합니다.
    - 그러나 메시지를 삭제하기 전에 소비자가 실패하고 가시성 제한 시간이 만료되기 전에 시스템에서 해당 메시지에 대한 DeleteMessage 작업을 호출하지 않으면 메시지가 다른 소비자에게 표시되고 메시지가 다시 수신됩니다.
    - 메시지를 한 번만 수신해야 하는 경우 소비자는 가시성 제한 시간 내에 메시지를 삭제해야 합니다.

**AWS Direct Connect, AWS Site-To-Site VPN**
- 회사의 온프레미스 인프라를 AWS 로 확장하기 위해 새로운 하이브리드 아키텍처를 설계하고 있습니다
- 회사는 AWS 리전에 대해 일관되게 짧은 지연 시간과 고가용성 연결이 필요합니다
- 회사는 비용을 최소화해야 하며 기본 연결이 실패할 경우 더 느린 트래픽을 기꺼이 받아들입니다
    
    → **리전에 대한 AWS Direct Connect 연결을 프로비저닝합니다. 기본 Direct Connect 연결이 실패하는 경우 백업으로 VPN 연결을 프로비저닝합니다**
    
    - 어떤 경우에는 이 연결만으로는 충분하지 않습니다.
    - 항상 DX 의 백업으로 폴백 연결을 보장하는 것이 좋습니다.
    - 여러 옵션이 있지만 AWS Site-To-Site VPN 으로 구현하는 것이 비용 효율적입니다.
    - 비용을 줄이기 위해 활용하거나 그 동안 두 번째 DX 설정을 기다릴 수 있는 솔루션입니다.
    - VPN 과 Direct Connect 는 같이 사용할 수 있음.

**다중 AZ, Auto Scaling**
- 회사는 Application Load Balancer 뒤의 Amazon EC2 인스턴스에서 비즈니스 크리티컬 웹 애플리케이션을 실행하고 있습니다
- EC2 인스턴스는 Auto Scaling 그룹에 있습니다
- 애플리케이션은 단일 가용 영역에 배포된 Amazon Aurora PostgreSQL 데이터베이스를 사용합니다
- 회사는 다운타임과 데이터 손실을 최소화하면서 애플리케이션의 고가용성을 원합니다
    
    → **여러 가용 영역을 사용하도록 Auto Scaling 그룹을 구성합니다. 데이터베이스를 다중 AZ 로 구성합니다. 데이터베이스에 대한 Amazon RDS 프록시 인스턴스를 구성합니다**
    
    - 다중 AZ + Auto Scaling 으로 고가용성 확보.
    - 최소한의 가동 중지 시간과 최소한의 데이터 손실로 고가용성을 달성하려면 단일 장애 지점이 없도록 여러 가용 영역을 사용하도록 Auto Scaling 그룹을 구성해야 합니다.
    - 기본 가용 영역에서 정전이 발생한 경우 자동 장애 조치를 활성화하려면 데이터베이스를 다중 AZ 로 구성해야 합니다.
    - 또한 Amazon RDS Proxy 인스턴스를 사용하여 연결 실패를 줄이고 장애 조치 시간을 개선하여 데이터베이스의 확장성과 가용성을 개선할 수 
    있습니다.

**AWS Application Load Balancer**
- 회사의 HTTP 애플리케이션은 NLB(Network Load Balancer) 뒤에 있습니다
- NLB 의 대상 그룹은 웹 서비스를 실행하는 여러 EC2 인스턴스와 함께 Amazon EC2 Auto Scaling 그룹을 사용하도록 구성됩니다
- 회사는 NLB 가 애플리케이션에 대한 HTTP 오류를 감지하지 못한다는 것을 알게 되었습니다
- 이러한 오류는 웹 서비스를 실행하는 EC2 인스턴스를 수동으로 다시 시작해야 합니다
- 회사는 사용자 정의 스크립트나 코드를 작성하지 않고 애플리케이션의 가용성을 개선해야 합니다
    
    → **NLB 를 Application Load Balancer 로 교체합니다. 회사 애플리케이션의 URL을 제공하여 HTTP 상태 확인을 활성화합니다. 비정상 인스턴스를 
    교체하도록 Auto Scaling 작업을 구성합니다**
    
    - Application Load Balancer 는 등록된 대상으로 요청을 주기적으로 전송하여 상태를 확인합니다.
    - 이러한 테스트를 바로 상태 확인이라고 합니다.
    - HTTP, HTTPS 등의 프로토콜이 여기에 해당됩니다. HTTP 프로토콜이 기본 설정값입니다.

**Amazon Dynamo DB**
- 회사는 Amazon DynamoDB 를 사용하여 고객 정보를 저장하는 쇼핑 애플리케이션을 실행합니다
- 데이터 손상의 경우 솔루션 설계자는 15 분의 RPO(복구 시점 목표)와 1 시간의 RTO(복구 시간 목표)를 충족하는 솔루션을 설계해야 합니다
    
    → **DynamoDB 지정 시간 복구를 구성합니다. RPO 복구의 경우 원하는 시점으로 복원합니다**
    
    - DynamoDB 는 주문형 백업 기능을 제공합니다.
    - 이를 통해 규정 준수 요구 사항에 대한 장기 보존 및 보관을 위해 테이블의 전체 백업을 생성할 수 있습니다.
    - 주문형 백업을 생성하고 Amazon DynamoDB 테이블에 대한 특정 시점 복구를 활성화할 수 있습니다.
    - 지정 시간 복구는 우발적인 쓰기 또는 삭제 작업으로부터 테이블을 보호하는 데 도움이 됩니다.
    - 특정 시점 복구를 사용하면 지난 35 일 동안의 특정 시점으로 테이블을 복원할 수 있습니다.

**AWS Transit Gateway**
- 회사는 동일한 AWS 리전에 있는 Amazon S3 버킷에서 사진을 자주 업로드 및 다운로드해야 하는 사진 처리 애플리케이션을 실행합니다
- 솔루션 설계자는 데이터 전송 비용이 증가한다는 사실을 알게 되었고 이러한 비용을 줄이기 위한 솔루션을 구현해야 합니다
    
    → **S3 VPC 게이트웨이 엔드포인트를 VPC 에 배포하고 S3 버킷에 대한 액세스를 허용하는 엔드포인트 정책을 연결합니다**
    
    - Transit Gateway 는 동일한 리전 내에 있는 여러 VPC 들을 연결하는 전송 '허브'이므로 Transit Gateway 를 거쳐 VPC 끼리 통신이 가능
    - AWS Transit Gateway 는 동일한 리전의 VPC 를 상호 연결하여 Amazon VPC 라우팅 구성을 한 곳에 통합하는 네트워크 전송 허브입니다.
    - S3 VPC 게이트웨이 엔드포인트를 배포하면 애플리케이션이 VPC 내의 프라이빗 네트워크 연결을 통해 S3 버킷에 액세스할 수 있으므로 인터넷을 통한 데이터 전송이 필요하지 않습니다.
    - 이를 통해 데이터 전송 비용을 줄이고 애플리케이션의 성능을 향상시킬 수 있습니다.
    - 엔드포인트 정책을 사용하여 애플리케이션이 액세스할 수 있는 S3 버킷을 지정할 수 있습니다.

**AWS VPC Subnet, Bastion Host**
- 회사는 최근 프라이빗 서브넷의 Amazon EC2 에서 Linux 기반 애플리케이션 인스턴스를 시작하고 VPC 의 퍼블릭 서브넷에 있는 Amazon EC2 인스턴스에서 Linux 기반 배스천 호스트를 시작했습니다
- 솔루션 설계자는 사내 네트워크에서 회사의 인터넷 연결을 통해 배스천 호스트 및 애플리케이션 서버에 연결해야 합니다
- 솔루션 설계자는 모든 EC2 인스턴스의 보안 그룹이 해당 액세스를 허용하는지 확인해야 합니다
    
    → **배스천 호스트의 현재 보안 그룹을 회사의 외부 IP 범위에서만 인바운드 액세스를 허용하는 보안 그룹으로 교체합니다
        애플리케이션 인스턴스의 현재 보안 그룹을 배스천 호스트의 개인 IP 주소에서만 인바운드 SSH 액세스를 허용하는 보안 그룹으로 교체합니다**
    
    - 전체적인 프로세스는 사내 네트워크 -> 외부 인터넷 -> Bastion Host(퍼블릭서브넷 내에 NAT 게이트웨이와 함께 위치) -> Application(프라이빗서브넷 내에 위치)으로 이루어짐.
    - Bastion Host 는 내부네트워크(여기서는 Application 이 있는 곳)에 접속할 수 있는 유일한 창구로, SSH 접속도 여길 통과해야만 가능함.

**2 계층 웹 애플리케이션 보안 그룹 구성**
- 솔루션 설계자는 2 계층 웹 애플리케이션을 설계하고 있습니다
- 애플리케이션은 퍼블릭 서브넷의 Amazon EC2 에서 호스팅되는 퍼블릭 웹 티어로 구성됩니다
- 데이터베이스 계층은 프라이빗 서브넷의 Amazon EC2 에서 실행되는 Microsoft SQL Server 로 구성됩니다
- 보안은 회사의 최우선 과제입니다
    
    → **0.0.0.0/0 에서 포트 443 의 인바운드 트래픽을 허용하도록 웹 계층에 대한 보안 그룹을 구성합니다
        웹 계층에 대한 보안 그룹에서 포트 1433 의 인바운드 트래픽을 허용하도록 데이터베이스 계층에 대한 보안 그룹을 구성합니다**
    
    - 전체적인 구조는 EC2 인스턴스에서 실행되는 웹 애플리케이션(퍼블릭 서브넷 내에 위치)---->EC2 인스턴스에서 실행되는 데이터베이스(프라이빗 서브넷 내에 위치)으로 되어있고, 인스턴스 단위의 보안은 보안 그룹이 담당.
    - 보안 그룹은 기본적으로 인바운드 트래픽에 관해서는 허용만 지정할 수 있고, 허용하지 않은 건 기본적으로 모두 차단하기 때문에 외부 인터넷->웹 애플리케이션으로의 액세스를 허용하려면 0.0.0.0/0 으로부터 온 포트 443(HTTPS)를 허용해야 함.
    - 그 다음으로 웹 애플리케이션->데이터베이스로의 액세스를 허용하려면 웹 애플리케이션이 있는 웹 계층에서 오는 포트 1433(MySQL) 인바운드 트래픽을 허용하도록 보안 그룹 설정을 해야 함.

**Amazon API Gateway, AWS Lambda, Amazon Simple Queue Service**
- 회사에서 애플리케이션의 성능을 개선하기 위해 다계층 애플리케이션을 온프레미스에서 AWS 클라우드로 이동하려고 합니다
- 애플리케이션은 RESTful 서비스를 통해 서로 통신하는 애플리케이션 계층으로 구성됩니다
- 한 계층이 오버로드되면 트랜잭션이 삭제됩니다
- 솔루션 설계자는 이러한 문제를 해결하고 애플리케이션을 현대화하는 솔루션을 설계해야 합니다
    
    → **Amazon API Gateway 를 사용하고 애플리케이션 계층으로 AWS Lambda 함수에 트랜잭션을 전달합니다. Amazon Simple Queue Service(Amazon SQS)를 애플리케이션 서비스 간의 통신 계층으로 사용합니다**
    
    - AWS Lambda, Amazon API Gateway, AWS Amplify, Amazon DynamoDB 및 Amazon Cognito 를 사용하여 서버리스 웹 애플리케이션을 구축
    - 이 예에서는 AWS Lambda, Amazon API Gateway, AWS Amplify, Amazon DynamoDB 및 Amazon Cognito 를 사용하여 서버리스 웹 애플리케이션 구축 질문과 유사한 설정을 보여줍니다.
    - RESTful API = API Gateway 사용. 트랜잭션 삭제되는 문제 = SQS.

**AWS Direct Connect, AWS DataSync**
- 회사는 단일 공장에 있는 여러 기계에서 매일 10TB 의 계측 데이터를 수신합니다
- 데이터는 공장 내에 위치한 온프레미스 데이터 센터의 SAN(Storage Area Network)에 저장된 JSON 파일로 구성됩니다
- 회사는 이 데이터를 Amazon S3 로 전송하여 중요한 실시간에 가까운 분석을 제공하는 여러 추가 시스템에서 액세스할 수 있기를 원합니다.
- 데이터가 민감한 것으로 간주되기 때문에 안전한 전송이 중요합니다
- 가장 안정적인 데이터 전송을 제공하는 솔루션
    
    → **AWS Direct Connect 를 통한 AWS DataSync**
    
    - Direct Connect 는 전용선 연결로 온프레미스-AWS 간 통신하는 것이고, DataSync 는 데이터 전송/마이그레이션에 사용되는 서비스.
    - AWS DataSync 는 온프레미스와 AWS 스토리지 서비스 사이에서 데이터 이동을 자동화 및 가속화하는 안전한 온라인 서비스입니다.
    - Amazon Simple Storage Service(S3) 버킷 간에 데이터를 복사할 수 있습니다.

**Amazon Kinesis Data Stream, Amazon API Gateway API Firehose, AWS Lambda, Amazon S3**
- 회사는 애플리케이션에 대한 실시간 데이터 수집 아키텍처를 구성해야 합니다
- 회사에는 데이터가 스트리밍될 때 데이터를 변환하는 프로세스인 API 와 데이터를 위한 스토리지 솔루션이 필요합니다
    
    → **Amazon Kinesis 데이터 스트림으로 데이터를 보내도록 Amazon API Gateway API 를 구성합니다. Kinesis 데이터 스트림을 데이터 원본으로 사용하는 Amazon Kinesis Data Firehose 전송 스트림을 생성합니다. AWS Lambda 함수를 사용하여 데이터를 변환합니다. Kinesis Data Firehose 전송 스트림을 사용하여 데이터를 Amazon S3 로 보냅니다**
    
    - API Gateway API 를 Kinesis Data Streams 와 같이 사용 가능
        - API Gateway API를 Kinesis와 통합하려면 API Gateway와 Kinesis 서비스를 모두 사용할 수 있는 리전을 선택해야 합니다.
    - Kinesis Data Streams 로 데이터 수집.
        - Amazon Kinesis Data Streams 를 사용하면 특수 요구에 맞춰 스트리밍 데이터를 처리 또는 분석하는 사용자 지정 애플리케이션을 구축할 수 있습니다. 수십 만개의 소스에서 클릭스트림, 애플리케이션 로그, 소셜 미디어와 같은 다양한 유형의 데이터를 Kinesis 데이터 스트림에 추가할 수 있습니다.
    - Kinesis Data Streams -> Kinesis Data Firehose
        - Amazon Kinesis Data Firehose 전송 스트림에 정보를 전송하도록 Amazon Kinesis Data Streams 를 구성할 수 있습니다.
    - Lambda 로 데이터 변환
        - Kinesis Data Firehose Firehose 는 Lambda 함수를 호출하여 수신되는 소스 데이터를 변환하고 변환된 데이터를 대상으로 전송할 수 있음.
    - S3 로 전송
        - Amazon Kinesis Data Firehose 는 실시간 스트리밍 데이터를 Amazon S3, Amazon RedShift, Amazon OpenSearch Service, Splunk 및 사용자 지정 HTTP 엔드포인트 또는 Datadog, Dynatrace, LogicMonitor, MongoDB, New Relic, Sumo Logic 을 포함한 지원되는 서드파티 소유의 HTTP 엔드포인트 대상에 전달하기 위한 완전관리형 서비스입니다.