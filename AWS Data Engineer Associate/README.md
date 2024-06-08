## 취득 배경
작년 11월부터 AWS 데이터 관련 자격증은 모두 취득하자라는 목표를 잡고 시작했으나, 중간에 여러 일들이 있어 잠시 공부를 중단하고 4월부터 본격적으로 하나씩 취득을 하기 시작했습니다. 4월엔 전체적인 AWS 서비스에 대해 두루 알아보고자 AWS Certified Solution Architect Associate를 먼저 취득 후 5월은 AWS Certified Machine Learning Specialty, 6월은 AWS Certified Data Engineer Associate를 순서로 취득하였습니다. 

공부를 하면서 아직 직접적인 AWS 서비스 내에서 데이터를 운영한 경험은 없지만 현재 AWS 기반의 빅데이터 플랫폼을 운영하면서 당시엔 몰랐지만 '그 때 그 개념이 이거였구나'하면서 데이터 거버넌스 및 보안을 관리하고, 데이터를 수집하며 적절히 ETL을 통해 BI로 올릴 Data Mart를 구상하거나 데이터 분석에 필요한 정제된 데이터를 운반했던 과정들이 본 자격증을 준비하는 이론학습 과정 속에서 한번 더 복습을 할 수 있어 유의미한 자격증 공부가 될 수 있었습니다.

## 학습 방법
다음은 AWS Certified Data Engineer  - Associate를 취득하기 위해 참고하였던 내용들입니다.

먼저 시험을 치룰 섹션과 해당 내용에 대한 가이드 문서를 확인해보았습니다.

![](https://velog.velcdn.com/images/seonwook97/post/43fc0e96-1baf-4241-bff8-ee000c0e4bbe/image.png)

- https://d1.awsstatic.com/training-and-certification/docs-data-engineer-associate/AWS-Certified-Data-Engineer-Associate_Exam-Guide.pdf

다음과 같이 크게 도메인 - 도메인 하위 태스크 - 관련 지식, 관련 기술 순으로 해당 도메인에 대한 내용과 함께 그에 관련된 AWS 서비스를 설명해주어 관련 서비스에 대해 바로바로 검색하여 공부하는 데 있어 수월하였습니다.

해당 가이드를 참조하여 어떤 유형에 관련된 문제들이 나오겠구나를 미리 한번 숙지하였고, 준비과정에 있어서 활용을 가장 많이 했던 부분은 **AWS Skill Builder**내 Data Engineer Associate 관련 학습, 공식문제세트를 학습하며 한 도메인이 끝날 때마다 2문제 씩 풀 수 있는 예제와 함께 본인이 부족한 부분에 있어 필요한 백서 또는 FAQ 가이드를 참조하였고 마지막으로는 20문항의 공식문제세트를 2~3회분 정도 반복하여 풀며 모르는 서비스에 대해 검색하여 하나의 데이터 엔지니어링 솔루션을 설계할 때 어떤 부분에 활용되는 지를 서비스별로 나누어 정리하였습니다. 추가적으로 [Udemy의 AWS Certified Data Engineer Associate 2024 - Hands On!](https://www.udemy.com/course/aws-data-engineer/learn/lecture) 강의를 구매하여 서비스에 대한 이해가 떨어지는 부분 또는 심화된 내용 숙지가 필요한 경우 해당 내용과 관련된 강의 및 자료를 함께 참고하였습니다.

![](https://velog.velcdn.com/images/seonwook97/post/8efa4ee6-e425-47b7-98cd-822eb7ac2a33/image.png)
- https://explore.skillbuilder.aws/learn/course/18546/exam-prep-standard-course-aws-certified-data-engineer-associate-dea-c01
- https://explore.skillbuilder.aws/learn/course/18200/exam-prep-official-practice-question-set-aws-certified-data-engineer-associate-dea-c01-korean

마지막으로는 현재까지 시험에 출제되었던 [덤프를](https://www.examtopics.com/exams/amazon/aws-certified-data-engineer-associate-dea-c01/view/) 하나씩 풀어보며 공식문제세트를 풀었던 것처럼 똑같이 모르는 서비스에 대해 데이터 엔지니어링 아키텍처 중심으로 어떤 부분에 쓰이는 지 분류를 하며 정리하였습니다. 2024년 4월에 공식적으로 출시된 시험이라 현재는 80문항 정도가 전부인 것 같습니다.

## 합격 후기
전반적으로 문제를 풀면서 느꼈던 건 **AWS Glue, AWS Redshift, AWS Kinesis, AWS Athena, AWS LakeFormation** 중심으로 파생된 서비스를 통해 데이터 파이프라인을 설계하는 데 있어 어떻게 활용할 건지에 대한 내용이 많았기 때문에 해당 서비스에 대해서는 기본적으로 공식 문서를 통한 서비스 내용을 확인해보는 것도 좋은 것 같습니다. 또한 **AWS Glue 워크플로와 AWS Step function, AWS Kinesis Data Streams와 AWS Kinesis Data Firehose** 등과 같이 비슷한 서비스들이 보기로 주어질 경우 해당 서비스 간 내용을 정확하게 알고 있어야 풀 수 있는 문제도 꽤 있어 서비스 간 차이점에 대해서도 어느정도 숙지하고 가면 수월하게 문제를 풀 수 있을 것이라고 생각합니다.

준비를 하는데 있어 [리눅서님의 기술 블로그 내 AWS Data Engineer Associate 합격 후기](https://linuxer.name/2024/03/aws-certified-data-engineer-associate-review/)와 [융무님의 AWS-DEA 합격후기](https://mjs1995.tistory.com/316) 포스팅을 추가적으로 참고하였습니다.

해당 시험은 크게 4개의 섹션에 대한 평가를 바탕으로 총 1000점 중 720점 이상을 취득해야 합격할 수 있습니다.
- 데이터 수집 및 변환 (34%)
- 데이터 저장소 관리 (26%)
- 데이터 운영 및 지원 (22%)
- 데이터 보안 및 거버넌스 (18%)

![](https://velog.velcdn.com/images/seonwook97/post/d03091b6-9c75-41ce-bea9-27dbd204806a/image.png)


