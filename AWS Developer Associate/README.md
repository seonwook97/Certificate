## 취득 배경
작년 6월 AWS Certified Data Engineer Associate 취득 이후 실제 AWS 서비스의 운영 시 개발자가 다뤄야 할 중점적인 내용들에 대해서 알아봄과 함께 현재 AWS에서 [Associate 챌린지](https://pages.awscloud.com/GLOBAL-other-GC-Traincert-Foundational-and-Associate-Certification-Challenge-2025-reg.html)를 진행하고 있어 50% 할인된 응시료로 시험을 볼 수 있어 취득하게 되었습니다. 
![](https://velog.velcdn.com/images/seonwook97/post/a6b42023-ffe5-4247-9311-1289ff495afd/image.png)

조건으로는 5월 21일 전까지 해당 시험을 통과해야 하나 AWS에서 제공하는 Certification 취득 관련 학습 영상들과 공식 문서 그리고 기출문제들을 충분히 활용하여 준비하면 취득하기 어렵지는 않다고 생각합니다. 응시료가 저렴하지는 않기 때문에 이런 이벤트들이 있을 때 적절히 활용하는 것도 나쁘지 않은 것 같습니다. 

## 시험 개요
[시험 안내서](https://d1.awsstatic.com/ko_KR/training-and-certification/docs-dev-associate/AWS-Certified-Developer-Associate_Exam-Guide.pdf)의 경우 측정하는 섹션별 측정 항목 비율, 섹션별 관련 지식 및 기술에 대한 하위 내용이 전부 명시되어 있기 때문에 학습하기 전 시험 준비 계획을 세울 때 필수적으로 활용해야 하는 내용입니다.
![](https://velog.velcdn.com/images/seonwook97/post/28b3d26c-cb9d-4ea3-932a-760bd0260386/image.png)

## 학습 방법
준비 시 활용했던 AWS 공식 자료들입니다. 
![](https://velog.velcdn.com/images/seonwook97/post/f0345586-57e9-4918-be5f-b97508c0ac3e/image.png)
- Skill Builder
    - https://explore.skillbuilder.aws/learn/external-ecommerce;view=none;redirectURL=?ctldoc-catalog-0=l-_ko~field16-_20~field17-_44~field14-_5

- 연습문제 
  - https://explore.skillbuilder.aws/learn/courses/18851/exam-prep-standard-course-aws-certified-developer-associate-dva-c02-korean-na
 
- 그 외 서비스 공식 문서
  - Amazon DynamoDB 
    - https://aws.amazon.com/ko/dynamodb/faqs/?da=sec&sec=prep
  - AWS Lambda 
    - https://aws.amazon.com/ko/lambda/faqs/?da=sec&sec=prep
  - Amazon API Gateway
    - https://aws.amazon.com/ko/api-gateway/faqs/?da=sec&sec=prep
  - AWS CloudFormation
    - https://aws.amazon.com/ko/cloudformation/faqs/
  - AWS Secrets Manager
    - https://aws.amazon.com/ko/secrets-manager/faqs/
  - AWS Systems Manager
    - https://aws.amazon.com/ko/systems-manager/
    - Parameter Store: https://docs.aws.amazon.com/ko_kr/systems-manager/latest/userguide/systems-manager-parameter-store.html
  - Amazon Cognito
    - https://aws.amazon.com/ko/cognito/faqs/
  - AWS IAM
    - https://aws.amazon.com/ko/iam/faqs/?da=sec&sec=prep
  - AWS KMS 
    - https://aws.amazon.com/ko/kms/faqs/?da=sec&sec=prep
  - AWS SQS
    - https://aws.amazon.com/ko/sqs/faqs/?da=sec&sec=prep
  - AWS ECS
    - https://aws.amazon.com/ko/ecs/faqs/
  - AWS ECR
    - https://aws.amazon.com/ko/ecr/faqs/
  - AWS EKS
    - https://aws.amazon.com/ko/eks/faqs/
  - Amazon ElastiCache
    - https://aws.amazon.com/ko/elasticache/faqs/?da=sec&sec=prep
  - AWS CodeBuild
    - https://aws.amazon.com/ko/codebuild/faqs/
  - AWS CodeDeploy
    - https://aws.amazon.com/ko/codedeploy/faqs/?nc=sn&loc=6
  - AWS CodeCommit(서비스 종료)
    - https://aws.amazon.com/ko/codecommit/faqs/
  - AWS CodePipeline
    - https://aws.amazon.com/ko/codepipeline/faqs/?nc=sn&loc=5
  - AWS SAM
    - https://aws.amazon.com/ko/serverless/sam/faqs/
  - AWS Step Functions
    - https://aws.amazon.com/ko/step-functions/faqs/
  - AWS CDK
    - https://aws.amazon.com/ko/cdk/faqs/
  
추가적으로 활용했던 자료는 Udemy의 [Stephane Maarek의 AWS Certified Developer Associate 강의](https://www.udemy.com/course/best-aws-certified-developer-associate/?kw=aws+certified&src=sac&couponCode=KRLETSLEARNNOW)를 수강하였습니다. 서비스에 대한 세부 내용까지 다루기 때문에 영상의 길이가 길어 저같은 경우는 익숙하지 않은 서비스 혹은 기업사례로 자주 언급되는 서비스(AWS Lambda, API Gateway, DynamoDB 등)의 세부 내용에 대해 골라 활용하는 편입니다. 특히 강의 이외에 서비스 내용에 대한 슬라이드 자료가 매우 좋다고 생각하며, 강의 마지막 챕터의 실전 모의고사 문제도 직전의 풀어보면 좋은 과정입니다.


마지막으로는 [Examtopics](https://www.examtopics.com/exams/amazon/aws-certified-developer-associate-dva-c02/)에서 현재까지 응시되었던 기출문제들에 대해서 반복해서 문제풀이를 진행하였으며, 잘 이해가 가지 않은 서비스들은 위에 소개드렸던 자료들을 참조하며 개인적으로 필기하며 학습했습니다.

## 합격 후기
AWS Certification 문제들의 특징은 실제 기업사례에서 최적의 아키텍처 설계 방법 혹은 기존보다 비용 효율적인 서비스 도입 등 기존 서비스와 유사한 서비스들의 조합을 통해 현재보다 더 개선된 구현 방법을 도출하는 것이 중요합니다. 따라서 실제 유사 서비스들 간 장/단점, 차이점에 대해 명확히 구분이 된다면 실제 시험에서 적절한 답안을 도출할 수 있을 것입니다.

해당 시험은 크게 4개의 섹션에 대한 평가를 바탕으로 총 1000점 중 720점 이상을 취득해야 합격할 수 있습니다.
- AWS 서비스를 사용한 개발(32%) 
- 보안(26%) 
- 배포(24%) 
- 문제 해결 및 최적화(18%)

![](https://velog.velcdn.com/images/seonwook97/post/a689d925-7248-4fdb-bfd8-b296d72c1614/image.png)
