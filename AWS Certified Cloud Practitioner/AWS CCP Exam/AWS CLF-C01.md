# AWS CLF-C01

1. Which AWS service provides infrastructure security optimization recommendations?
    - **AWS Trusted Advisor**
2. A file-sharing service uses Amazon S3 to store files uploaded by users.
    
    Files are accessed with random frequency.
    
    Popular ones are downloaded every day whilst others not so often and some rarely.
    
    What is the most cost-effective Amazon S3 object storage class to implement?
    
    - **Amazon S3 Intelligent-Tiering**
3. Which AWS service can be deployed to enhance read performance for applications while reading data from NoSQL database?
    - **Amazon DynamoDB Accelerator**
4. An organization utilizes a software suite that consists of a multitude of underlying microservices hosted on the cloud.
    
    The application is frequently giving runtime errors.
    
    Which service will help in the troubleshooting process?
    
    - **AWS X-Ray**
5. According to the AWS, what is the benefit of Elasticity?
    - **Create systems that scale to the required capacity based on changes in demand**
6. Which tool can you use to forecast your AWS spending?
    - **AWS Cost Explorer**
7. Which of the following is an optional Security layer attached to a subnet within a VPC for controlling traffic in & out of the VPC?
    - **Network ACL**
8. Which of the following is a customer responsibility under AWS Shared Responsibility Model?
    - **Patching of guest OS deployed on Amazon EC2 instance**
9. What is the AWS feature that enables fast, easy and secure transfers of files over long distances between your client and your Amazon S3 bucket?
    - **Amazon S3 Transfer Acceleration**
10. Which of the following services can be used to optimize performance for global users to transfer large-sized data objects to a centralized Amazon S3 bucket in us-west-1 region?
    - **Enable S3 Transfer Acceleration on Amazon S3 bucket**
11. There is a requirement to store objects.
    
    The objects must be downloadable via a URL.
    
    Which storage option would you choose?
    
    - **Amazon S3**
12. There is a requirement to host a database server for a minimum period of one year.
    
    Which of the following would result in the least cost?
    
    - **Partial Upfront costs Reserved**
13. During an organization's information systems audit, the administrator is requested to provide a dossier of security and compliance reports and online service agreements between the organization and AWS.
    
    Which service can they utilize to acquire this information?
    
    - **AWS Artifact**
14. A new department has recently joined the organization and the administrator needs to compose access permissions for the group of users.
    
    Given that they have various roles and access needs, what is the best-practice approach when granting access?
    
    - **The administrator should grant all users the least privilege and add more privileges to only to those who need it.**
15. There is an external audit being carried out on your company.
    
    The IT auditor needs to have a log of 'who made the requests' to the AWS resources in the company's account.
    
    Which of the below services can assist in providing these details?
    
    - **AWS CloudTrail**
16. Which of the following features can be used to preview changes to be made to an AWS resource which will be deployed using the AWS CloudFormation template?
    - **AWS CloudFormation Change Sets**
17. Which of the following is the responsibility of the customer to ensure the availability and backup of the EBS volumes?
    - **Create EBS snapshots**
18. When designing a highly available architecture, what is the difference between vertical scaling (scaling-up) and horizontal scaling (scaling-out)?
    - **Scaling up adds more resources to an instance, scaling out adds more instances**
19. Your company is planning to move to the AWS Cloud.
    
    You need to give a presentation on the cost perspective when moving existing resources to the AWS Cloud.
    
    Considering Amazon EC2, which of the following is an advantage from the cost perspective?
    
    - **The ability to only pay for what you use**
20. When designing a system, you use the principle of “design for failure and nothing will fail”
    
    Which of the following services/features of AWS can assist in supporting this design principle? Choose 3 answers from the options given below.
    
    - **Availability Zones**
    - **Regions**
    - **Elastic Load Balancer**
21. Your design team is planning to design an application that will be hosted on the AWS Cloud.
    
    One of their main non-functional requirements is given below: Reduce inter-dependencies so failures do not impact other components. Which of the following concepts does this requirement relate to?
    
    - **Decoupling**
22. Which of the following security requirements are managed by AWS? Select 3 answers from the options given below.
    - **Physical security**
    - **Disk disposal**
    - **Hardware patching**
23. You are planning on deploying a video-based application onto the AWS Cloud.
    
    Users across the world will access these videos.
    
    Which of the below services can help efficiently stream the content to the users across the globe?
    
    - **Amazon CloudFront**
24. Which of the following AWS services can be used to retrieve configuration changes made to AWS resources causing operational issues?
    - **AWS Config**
25. An organization runs several EC2 instances inside a VPC using three subnets, one for Development, one for Test and one for Production.
    
    The Security team has some concerns about the VPC configuration.
    
    It requires to restrict the communication across the EC2 instances using Security Groups. Which of the following options is true for Security Groups?
    
    - **You can change a Security Group associated to an instance if the instance state is stopped or running**
26. Your company is planning to pay for an AWS Support plan.
    
    They have the following requirements as far as the support plan goes: 24x7 access to Cloud Support Engineers via email, chat & phone Response time of less than 15 minutes for any business-critical system faults Which of the following plans will suffice to keep in mind the above requirement?
    
    - **Enterprise**
27. Your company wants to move an existing Oracle database to the AWS Cloud.
    
    Which of the following services can help facilitate this move?
    
    - **AWS Database Migration Service**
28. On which of the following resources does Amazon Inspector perform network accessibility checks?
    - **Amazon EC2 instance**
29. Which of the following services helps to achieve the computing elasticity in AWS?
    - **AWS EC2 Auto Scaling Group**
30. A live online game uses DynamoDB instances in the backend to store real-time scores of the participants as they compete against each other from various parts of the world.
    
    Which data consistency option is the most appropriate to implement?
    
    - **Strongly consistent**
31. Which of the following services allows you to analyze EC2 Instances against pre-defined security templates to check for vulnerabilities?
    - **AWS Inspector**
32. You are planning to serve a web application on the AWS Platform by using EC2 Instances.
    
    Which of the below principles would you adopt to ensure that even if some of the EC2 Instances crash, you still have a working application?
    
    - **Using a fault tolerant system**
33. Which of the following are best practices when designing cloud-based systems? Choose 2 answers from the options below.
    - **Build loosely-coupled components**
    - **Assume everything will fail**
34. Which services allow the customer to retain full administrative privileges of the underlying virtual infrastructure?
    - **Amazon EC2**
35. You have a mission-critical application that must be globally available at all times.
    
    If this is the case, which of the below deployment mechanisms would you employ?
    
    - **Deployment to multiple Regions**
36. Which of the following can be used to protect against DDoS attacks? Choose 2 answers from the options given below.
    - **AWS Shield**
    - **AWS Shield Advanced**
37. Which of the following is a serverless compute offering from AWS?
    - **AWS Lambda**
38. Which of the following security services can be used to detect users' personal credit card numbers from data stored in Amazon S3?
    - **Amazon GuardDuty**
39. An online streaming company is prohibited from broadcasting its content in certain countries and regions in the world.
    
    Which Amazon Route 53 routing policy would be the most suitable in guaranteeing their compliance?
    
    - **Geolocation**
40. Which AWS service provides a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability?
    - **Dynamo DB**
41. In the AWS Billing and Management service, which tool can provide usage-based forecasts of estimated billing costs and usage for the coming months?
    - **AWS Cost Explorer**
42. Which of the following AWS managed database service provides processing power that is up to 5X faster than a traditional MySQL database?
    - **Aurora**
43. In the AWS Well-Architected Framework, which of the following is NOT a Security design principle to design solutions in AWS?
    - **Apply Security only at the edge of the network**
44. Which of the following options is TRUE for AWS Database Migration Service (AWS DMS)?
    - **AWS DMS can migrate databases from on-premise to AWS**
    - **AWS DMS can migrate databases from AWS to on-premise**
    - **AWS DMS can migrate databases from EC2 to Amazon RDS**
    - **AWS DMS can have Amazon Redshift and Amazon DynamoDB as target databases**
45. Which of the following services helps in governance, compliance, and risk auditing in AWS?
    - **AWS CloudTrail**
46. Project team enhancing the security features of a banking application, requires implementing a threat detection service that continuously monitors malicious activities and unauthorized behaviors to protect AWS accounts, workloads, and data stored in Amazon S3
    
    Which AWS services should the project team select?
    
    - **Amazon GuardDuty**
47. Which of the following are benefits of the AWS's Relational Database Service (RDS)? Choose the 2 correct answers from the options below.
    - **Automated patches and backups**
    - **DB owner can resize the capacity accordingly**
48. Which AWS product provides a unified user interface, enabling easy management of software development activities in one place, along with, quick development, build, and deployment of applications on AWS?
    - **AWS CodeStar**
49. If you want to take a backup of an EBS Volume, what would you do?
    - **Create an EBS snapshot**
50. Your Security Team has some security concerns about the application data stored on S3
    
    The team requires you to introduce two improvements: (i) add “encryption at rest” and (ii) give them the possibility to monitor who has accessed the data and when the data have been accessed. Which of the following AWS solution would you adopt to satisfy the requirement?
    
    - **Server-Side Encryption managed by KMS (SSE-KMS) with CloudTrail**
51. Which of the following statements regarding Amazon Athena are accurate? Select TWO
    - **Amazon Athena queries data directly from Amazon S3 and there are no additional data storage commitments beyond the object storage**
    - **Amazon Athena is compatible with data formats such as CSV, JSON, ORC, AVRO and Parquet**
52. An administrator is running a large deployment of AWS resources that are spread across several AWS Regions.
    
    They would like to keep track of configuration changes on all the resources and maintain a configuration inventory.
    
    What is the best service they can use?
    
    - **AWS Config**
53. A company does not want to manage their database.
    
    Which of the following services is a fully managed NoSQL database provided by AWS?
    
    - **DynamoDB**
54. Whilst working on a collaborative project, an administrator would like to record the initial configuration and several authorized changes that engineers make to the route table of a VPC.
    
    What is the best method to achieve this?
    
    - **Use of AWS Config**
55. Which of the following is a template that contains the software configuration to launch an ec2 instance?
    - **AMI**
56. Security and Compliance is a shared responsibility between AWS and the customer.
    
    Which amongst the below-listed options are AWS responsibilities?(Select TWO.)
    
    - **Security of the AWS cloud**
    - **Patch management within the AWS infrastructure**
57. Which of the following tools can be used to check service limits for resources launched within AWS Cloud Infrastructure?
    - **AWS Trusted Advisor**
58. Which of the following accurately describes a typical use case in which the AWS CodePipeline service can be utilized?
    - **To orchestrate and automate the various phases involved in the release of application updates in-line with a predefined release model**
59. Your organization has planned to decommission its data centers.
    
    You have a task to migrate hundreds of TB of archived data and 22 TB of active data to S3 and EFS, as per the designed solution.
    
    Which of the below service will be best suited for this task?
    
    - **AWS Data Sync**
60. To maximize user satisfaction, you are asked to improve the performance of the application for local and global users.
    
    As part of this initiative, you must monitor the application endpoint health and route traffic to the most appropriate application endpoint.
    
    Which service will you prefer to use?
    
    - **Amazon Global Accelerator**
61. Which AWS service offering uses machine learning and graph theory capability on automatically collected log data to help you conduct faster and efficient security investigations?
    - **Amazon Detective**
62. An administrator is tasked to configure privileges for the new joiners in the department.
    
    The admin is selectively granting privileges and ensuring that not all the team members can access all the resources. Which principle is the administrator following?
    
    - **Principle of least privilege**

63. You are asked to suggest an appropriate Amazon S3 storage class for “data 

with unknown/changing access pattern”

Which one would you suggest?

- **Amazon S3 Intelligent-Tiering**
1. A “Member AWS account” in an AWS Organization (using consolidated billing) wants to receive a cost breakdown report (product-wise daily report) so that the analysis of cost and usage could be done. Where can this report be configured to be delivered?
    - **S3 bucket owned by the master account**
2. Which AWS service allows: 1- Running Docker containers 2- Simple API calls to launch and stop container-based applications.
    - **Amazon Elastic Container Service**
3. Which AWS services can be used to store files? Choose 2 answers from the options given below.
    - **Amazon Simple Storage Service (Amazon S3)**
    - **Amazon Elastic Block Store (Amazon EBS)**
4. When an administrator is looking to deploy shared file access Linux-based workloads which will require up to petabytes of data stores, what is the best-suited file storage option to use?
    - **Amazon EFS**
5. Which of the following is a prerequisite for using AWS OpsWorks to manage applications on servers at the customer data centres (on-premises compute servers)?
    - **Servers should be running Linux OS with connectivity to AWS private endpoints**
6. Which AWS service provides infrastructure security optimization recommendations?
    - **AWS Trusted Advisor**
7. A department in an organization has a stipulated monthly expenditure limit on their AWS account and is anxious about exceeding it.
    
    How can they allay this concern in the best possible way?
    
    - **In AWS Budgets, creating an email alert based on the budget parameters would suffice**
8. A company needs to know which user was responsible for terminating several critical Amazon Elastic Compute Cloud (EC2) Instances.
    
    Where can the customer find this information?
    
    - **AWS CloudTrail logs**
9. I have a client who is moving their on premise workloads to AWS.
    
    Since they are very cost conscious, they would like to get first hand information on their expenses they will incur while using AWS services.
    
    Which of the following will help them do that?
    
    - **AWS Pricing Calculator**
10. What is the value of having AWS Cloud services accessible through an Application Programming Interface (API)?
    - **It allows developers to work with AWS resources programmatically**
11. After moving their workload to AWS eu-central-1 region, an administrator would like to configure their email server on an Amazon EC2 instance in a private subnet of the VPC which will use Amazon SES.
    
    What is the most effective setup to implement?
    
    - **Configure a VPC endpoint powered by AWS PrivateLink**
12. A file-sharing service uses Amazon S3 to store files uploaded by users.
    
    Files are accessed with random frequency.
    
    Popular ones are downloaded every day whilst others not so often and some rarely.
    
    What is the most cost-effective Amazon S3 object storage class to implement?
    
    - **Amazon S3 Intelligent-Tiering**
13. Which AWS service automates infrastructure provisioning and administrative tasks for an analytical data warehouse?
    - **Amazon Redshift**
14. An administrator would like to automate the creation of new AWS accounts for the organization's research and development department.
    
    New workloads need to be spun-up promptly and categorized into groups.
    
    How can this be achieved efficiently?
    
    - **Use of AWS Organizations**
15. An organization utilizes a software suite that consists of a multitude of underlying microservices hosted on the cloud.
    
    The application is frequently giving runtime errors.
    
    Which service will help in the troubleshooting process?
    
    - **AWS X-Ray**
16. An administrator would like to automate the replication and deployment of a specific software configuration existent on one EC2 instance onto four hundred others.
    
    Which AWS service is BEST suited for this implementation?
    
    - **AWS OpsWorks**
17. Which AWS service can be deployed to enhance read performance for applications while reading data from NoSQL database?
    - **Amazon DynamoDB Accelerator**
18. Which AWS service can be used to detect & analyse performance issues related to AWS Lambda applications?
    - **AWS X-Ray**
19. A cloud solutions architect needs to execute urgent mission-critical tasks on the AWS Management console.
    
    But he has left his Windows-based machine at home.
    
    Given that only Non-Graphical User Interface (non-GUI), Linux-based machines are currently available, what would be the most secure option to administer these tasks on the cloud infrastructure?
    
    - **Install and run AWS CLI on one of the non-GUI Linux-based machines, in a shell environment such as bash. The cloud solutions architect will be able to access ALL services just as they can also be accessed from a Windows-based machine**
20. According to the AWS, what is the benefit of Elasticity?
    - **Create systems that scale to the required capacity based on changes in demand**
21. For which of the following scenarios are the Amazon Elastic Compute Cloud (Amazon EC2) Spot instances most appropriate?
    - **Workloads where the availability of the Amazon EC2 instances can be flexible**
22. A financial company with many resources running on AWS would like a machine learning-driven and proactive security solution that would promptly identify security vulnerabilities, particularly flagging suspicious or abnormal data patterns or activity between AWS services.
    
    Which AWS service would best meet this requirement?
    
    - **AWS Detective**
23. Which tool can you use to forecast your AWS spending?
    - **AWS Cost Explorer**
24. Which of the following is an optional Security layer attached to a subnet within a VPC for controlling traffic in & out of the VPC?
    - **Network ACL.**
25. A radio station compiles a list of the most popular songs each year.
    
    The songs are frequently fetched within 180 days.
    
    After that, the users will have a default retrieval time of 12 hours for downloading the files.
    
    The files should be stored for over 10 years.
    
    Which is the most cost-effective object storage after 180 days?
    
    - **Amazon S3 Glacier Deep Archive**
26. Which of the following is a customer responsibility under AWS Shared Responsibility Model?
    - **Patching of guest OS deployed on Amazon EC2 instance**
27. Which of the following is a factor when calculating Total Cost of Ownership (TCO) for the AWS Cloud?
    - **The number of servers migrated to AWS**
28. A group of developers for a startup company store their source code and binary files on a shared open-source repository platform which is publicly accessible over the internet.
    
    They have embarked on a new project in which their client requires high confidentiality and security on all development assets.
    
    Which AWS service can the developers use to store the source code?
    
    - **AWS CodeCommit**
29. An organization has a persistently high amount of throughput.
    
    It requires connectivity with no jitter and very low latency between its on-premise infrastructure and its AWS cloud build to support live streaming and real-time services.
    
    What is the MOST appropriate solution to meet this requirement?
    
    - **AWS Direct Connect**
30. A Professional Educational Institution maintains a dedicated web server and database cluster that hosts an exam results portal undertaken by its students.
    
    The resource is idle for most of the learning cycle and becomes excessively busy when exam results are released.
    
    How can this architecture with servers be improved to be cost-efficient?
    
    - **Configure serverless architecture leveraging AWS Lambda functions**
31. A business analyst would like to move away from creating complex database queries and static spreadsheets when generating regular reports for high-level management.
    
    They would like to publish insightful, graphically appealing reports with interactive dashboards.
    
    Which service can they use to accomplish this?
    
    - **Amazon QuickSight**
32. What is the AWS feature that enables fast, easy and secure transfers of files over long distances between your client and your Amazon S3 bucket?
    - **Amazon S3 Transfer Acceleration**
33. As per the AWS Acceptable Use Policy, how can the penetration testing of EC2 instances be performed?
    - **Can be performed by the customer, provided they work with the list of services mentioned by AWS**
34. In which five categories does Trusted Advisor service provide insight for an AWS account?
    - **Performance**
    - **cost optimization**
    - **security**
    - **fault tolerance and Service Limits**
35. Which of the following AWS services is suitable to be used as a fully managed data warehouse?
    - **Amazon RedShift**
36. What best describes the "Principle of Least Privilege"? Choose the correct answer from the options given below.
    - **Users should be granted permission to access only resources they need to do their assigned job**
37. A developer would like to automate the installation by updating a set of applications on a series of EC2 instances and on-premises servers.
    
    Which is the most appropriate service to use to achieve this requirement?
    
    - **AWS CodeDeploy**
38. As per AWS global infrastructure, which of the following components within an AWS Region provides a low latency redundant connectivity?
    - **Availability Zones**
39. Which of the following routing policies can be used to provide the best performance to global users accessing a static website deployed on Amazon S3 buckets at multiple regions?
    - **Use Route 53 latency routing policy**
40. Which of the following services can be used to optimize performance for global users to transfer large-sized data objects to a centralized Amazon S3 bucket in us-west-1 region?
    - **Enable S3 Transfer Acceleration on Amazon S3 bucket**
41. Which of the following is NOT an area of shared controls (Shared between AWS & Customer in different contexts) within the AWS Shared responsibility Model? (Select TWO.)
    - **Service & communication protection**
    - **IAM User Management**
42. Which of the following services can be used to automate software deployments on a large number of Amazon EC2 instance and on-premise servers?
    - **AWS CodeDeploy**
43. Which of the following statements best describe the AWS Personal Health Dashboard? (Select Two)
    - **User-specific view on the availability and performance of AWS services, underlying their AWS resources**
    - **A service that prompts the user with alerts and notifications on AWS scheduled activities, pending issues, and planned changes.**
44. A startup company that works on social media apps development would like to grant freelance developers temporary access to its Lambda functions setup on AWS.
    
    These developers would be signing-in via Facebook authentication.
    
    Which service is the most appropriate to grant secure access?
    
    - **Use Amazon Cognito for web-identity federation**
45. There is a requirement to store objects.
    
    The objects must be downloadable via a URL.
    
    Which storage option would you choose?
    
    - **Amazon S3**
46. There is a requirement to host a database server for a minimum period of one year.
    
    Which of the following would result in the least cost?
    
    - **Partial Upfront costs Reserved**
47. During an organization's information systems audit, the administrator is requested to provide a dossier of security and compliance reports and online service agreements between the organization and AWS.
    
    Which service can they utilize to acquire this information?
    
    - **AWS Artifact**
48. A new department has recently joined the organization and the administrator needs to compose access permissions for the group of users.
    
    Given that they have various roles and access needs, what is the best-practice approach when granting access?
    
    - **The administrator should grant all users the least privilege and add more privileges to only to those who need it**
49. Which of the following are advantages of having infrastructure hosted on the AWS Cloud? Choose 2 answers from the options given below.
    - **Having the pay as you go model**
    - **No Upfront costs**
50. There is an external audit being carried out on your company.
    
    The IT auditor needs to have a log of 'who made the requests' to the AWS resources in the company's account.
    
    Which of the below services can assist in providing these details?
    
    - **AWS CloudTrail**
51. A web administrator maintains several public and private web-based resources for an organisation.
    
    Which service can they use to keep track of the expiry dates of SSL/TLS certificates as well as updating and renewal?
    
    - **AWS Certificate Manager**
52. Which of the following statements regarding billing, cost optimization and cost management in AWS is accurate?
    - **When using Savings Plans, 72% savings can be made on Amazon EC2, AWS Fargate, and AWS Lambda usage**
53. Which of the following features can be used to preview changes to be made to an AWS resource which will be deployed using the AWS CloudFormation template?
    - **AWS CloudFormation Change Sets**
54. Which option best suits the implementation of an Amazon RDS database instance instead of a NoSQL/non-relational database?
    - **In an organisation where only a finite number of processes query the database in predictable and well-structured Schemas**
55. While making changes to AWS resources e.g.
    
    adding a new Security Group Ingress rule, I need to capture & record all these changes that will be helpful during an audit.
    
    Which of the following AWS service helps me do that?
    
    - **AWS Config**
56. AWS Organizations help manage multiple accounts effectively in a large enterprise.
    
    Which of the following statements related to AWS Organizations are correct? (Select TWO.)
    
    - **An Organizational Unit(OU) can have only one parent**
    - **Organizational level policies are known as Service Control Policies**
57. Which of the following is WRONG for NoSQL databases? (Select TWO.)
    - **They need to have a well defined schema**
    - **DynamoDB Transactions is NOT atomicity, consistency, isolation, and durability (ACID) compliant**
58. What is a valid difference between AWS Global Accelerator and Amazon CloudFront? Choose TWO responses.
    - **AWS Global Accelerator does not include the content caching capability that Amazon CloudFront does**
    - **AWS Global Accelerator is suitable for applications that are non-HTTP/S such as VoIP, MTTQ and gaming whereas Amazon CloudFront enhances the performance of HTTP-based content such as dynamic web applications, images and videos**
59. Which of the following is the responsibility of the customer to ensure the availability and backup of the EBS volumes?
    - **Create EBS snapshots**
60. Which AWS service gives the user the ability to group AWS resources across different AWS Regions by application and then collectively view their operational data for monitoring purposes?
    - **Systems Manager**
61. Which of the following is a situation that would require using both Spot and Reserved EC2 Instances?
    - **One that has a constantly predictable workload with brief unpredictable spikes**
62. When designing a highly available architecture, what is the difference between vertical scaling (scaling-up) and horizontal scaling (scaling-out)?
    - **Scaling up adds more resources to an instance, scaling out adds more instances**
63. A weather tracking system is designed to track weather conditions of any particular flight route.
    
    Flight travellers all over the world make use of this information prior to booking their flights.
    
    Travellers expect quick turnaround time in which the weather display & flight booking will happen which is critical to their business.
    
    You have designed this website and are using AWS Route 53 DNS.
    
    The routing policy that you will apply to this website is
    
    - **Latency based routing policy**
64. Which of the following services can be used as a web application firewall in AWS?
    - **AWS WAF**
65. What can be termed as a user-defined label that has a key-value pair of variable character length? It is assigned to AWS resources as metadata for administration and management purposes.
    - **Resource Tag**
66. A financial Organization has an on-premises Data Center that holds large volumes of customers' financial transaction data on its legacy mainframe systems.
    
    While accessing transaction data, they have implemented a caching solution in the AWS cloud that will hold the customer's financial data due to performance issues.
    
    The transaction data is extremely confidential & is heavy in bandwidth while transferring to the cloud.
    
    What connectivity would you recommend for this data transfer? Select the best answer.
    
    - **Direct Connect with a VPN connection**
67. A start-up organisation would like to deploy a complex web and mobile application development environment instantaneously, complete with the necessary resources and peripheral assets.
    
    How can this be achieved efficiently?
    
    - **Using AWS Quick Starts to identify and provision the appropriate AWS CloudFormation templates**
68. Which of the following can be attached to EC2 Instances to store data?
    - **Amazon EBS Volumes**
69. Which of the following networking component can be used to host EC2 resources in the AWS Cloud?
    - **AWS VPC**
70. I have a web application that has been deployed to the AWS Mumbai region.
    
    My application soon becomes popular.
    
    Now there are users all over the world who would like to access it.
    
    If I use a CloudFront distribution for doing so, which statements are FALSE for CloudFront? (Select TWO.)
    
    - **CloudFront does not cache dynamic content**
    - **CloudFront can use only S3 buckets as their Origin Server from where they can cache content**
71. Which of the following components of the Cloudfront service can be used to distribute content to users across the globe?
    - **Amazon Edge locations**
72. Your company is planning to move to the AWS Cloud.
    
    You need to give a presentation on the cost perspective when moving existing resources to the AWS Cloud.
    
    Considering Amazon EC2, which of the following is an advantage from the cost perspective?
    
    - **The ability to only pay for what you use**
73. Your company is planning to move to the AWS Cloud.
    
    Once it completely moves to the cloud, it wants to ensure that the right security settings are put in place.
    
    Which of the following tools are helpful? (Select TWO.)
    
    - **AWS Inspector**
    - **AWS Trusted Advisor**
74. There is a requirement to collect important metrics from AWS RDS and EC2 Instances.
    
    Which AWS service would be helpful to fulfill this requirement?
    
    - **Amazon CloudWatch**
75. I need to upload a large number of large-size objects from different Geographic locations to an S3 bucket.
    
    What is the best mechanism to do so in a fast & reliable way?
    
    - **I can use S3 Transfer Acceleration from each Geographic location that will route the data from their respective Edge locations to S3**
76. I have developed an application using AWS services that have been deployed to multiple regions.
    
    How do I achieve the best Performance and Availability when users from different locations access my application?
    
    - **Use Global Accelerator for improving performance and Availability**
77. Which statement is accurate about AWS Budgets and Cost Explorer?
    - **AWS Budgets uses the cost visualizations provided by AWS Cost Explorer to show the status of preset budgets and to provide forecasts of estimated costs**
78. When designing a system, you use the principle of “design for failure and nothing will fail”
    
    Which of the following services/features of AWS can assist in supporting this design principle? Choose 3 answers from the options given below.
    
    - **Availability Zones**
    - **Regions**
    - **Elastic Load Balancer**
79. While proposing AWS Cloud solution to a client as a value proposition, which of the following is not an advantage to use the AWS Cloud?
    - **The AWS Cloud gives complete control of Security to its users so that they can replicate their Data Center Security model on the Cloud**
80. You have a DevOps team in your current organization structure.
    
    They are keen to know if there is any service available in AWS which can be used to manage infrastructure as code.
    
    Which of the following can be met with such a requirement?
    
    - **Using AWS Cloudformation**

144.  Which one of the following features does NOT belong to any Well-Architected Framework pillar in AWS?

- **It provides the ability to configure servers with much more CPU resources than required so that users do not need to maintain the CPU resources for a long time.**
1. Which of the following is the responsibility of AWS according to the Shared Security Model? Choose 3 answers from the options given below.
    - **Securing edge locations**
    - **Monitoring physical device security**
    - **Implementing service organization Control (SOC) standards.**
2. Your company has just started using the resources on the AWS Cloud.
    
    They want to get an idea of the costs being incurred so far for the resources being used.
    
    How can this be achieved?
    
    - **By using the AWS Cost Explorer. Here you can see the running and forecast costs.**
3. By default who has complete administrative control over all resources in the respective AWS account?
    - **AWS Account Owner**
4. Your design team is planning to design an application that will be hosted on the AWS Cloud.
    
    One of their main non-functional requirements is given below: Reduce inter-dependencies so failures do not impact other components. Which of the following concepts does this requirement relate to?
    
    - **Decoupling**
5. Which of the following can be used to increase the fault tolerance of an application?
    - **Deploying resources across multiple Availability Zones**
6. Which of the following security requirements are managed by AWS? Select 3 answers from the options given below
    - **Physical security**
    - **Disk disposal**
    - **Hardware patching**
7. Which of the following is not the pillars of AWS Well-Architected Framework?
    - **Automation**
8. Your company is planning to offload some of the batch processing workloads on to AWS.
    
    These jobs can be interrupted and resumed at any time.
    
    Which of the following instance types would be the most cost-effective to use for this purpose?
    
    - **Spot**
9. Which service can be used to create steps required to automate build, test and deployments for a web application?
    - **AWS CodePipeline**
10. Your company is planning to use the AWS Cloud.
    
    But there is a management decision that resources need to split department wise.
    
    And the decision is tending towards managing multiple AWS accounts.
    
    Which of the following would help in the effective management and also provide an efficient costing model?
    
    - **AWS Organizations**
11. Which of the following can be used as an additional security layer for the user name and password when logging into the AWS Console?
    - **Multi-Factor Authentication (MFA)**
12. Which AWS Cloud service helps in the quick deployment of resources which can use different programming languages such as .Net and Java?
    - **AWS Elastic Beanstalk**
13. Your company handles a crucial e-Commerce application.
    
    This application needs to have an uptime of at least 99.5%
    
    There is a decision to move the application to the AWS Cloud.
    
    Which of the following deployment strategies can help build a robust architecture for such an application?
    
    - **Deploying the application across multiple Regions**
14. Your company is moving a large application to AWS using a set of EC2 instances.
    
    A key requirement is reusing existing server-bound software licensing.
    
    Which of the following options is the best for satisfying the requirement?
    
    - **EC2 Dedicated Hosts**
15. You are planning on deploying a video-based application onto the AWS Cloud.
    
    Users across the world will access these videos.
    
    Which of the below services can help efficiently stream the content to the users across the globe?
    
    - **Amazon CloudFront**
16. Using Content Delivery Network (CDN), an administrator would like to serve varying types of content based on the viewer's browser cookies.
    
    Which is the most appropriate serverless technique that can be used to achieve this?
    
    - **AWS Lambda@Edge**
17. For the AWS Shared Responsibility Model, which of the following responsibilities is NOT a part of shared controls by both customer and AWS?
    - **Global infrastructure that runs AWS Cloud services**
18. There is a requirement to host EC2 Instances in the AWS Cloud, wherein the utilization is for a duration of more than 3 years.
    
    Which of the following would you utilize to minimize the costs?
    
    - **Reserved instances**
19. An administrator would like to check if the Amazon CloudFront identity is making access API calls to an S3 bucket where a static website is hosted.
    
    Where can this information be obtained?
    
    - **In AWS CloudTrail Event history, look up access calls and filter for the Amazon CloudFront identity**
20. Which of the following AWS services can be used to retrieve configuration changes made to AWS resources causing operational issues?
    - **AWS Config**
21. A company is deploying a two-tier, highly available web application to AWS.
    
    The application needs a storage layer to store artifacts such as photos and videos.
    
    Which of the following services can be used as the underlying storage mechanism?
    
    - **Amazon S3**
22. An organization runs several EC2 instances inside a VPC using three subnets, one for Development, one for Test and one for Production.
    
    The Security team has some concerns about the VPC configuration.
    
    It requires to restrict the communication across the EC2 instances using Security Groups. Which of the following options is true for Security Groups?
    
    - **You can change a Security Group associated to an instance if the instance state is stopped or running**
23. Which of the below-mentioned services is equivalent to hosting virtual servers on an on-premises location?
    - **AWS EC2**
24. You have a set of EC2 Instances hosted on the AWS Cloud.
    
    The EC2 Instances are hosting a web application.
    
    Which of the following acts as a firewall to your VPC and the instances in it? Choose 2 answers from the options given below
    
    - **Usage of Security Groups**
    - **Usage of Network Access Control Lists**
25. Which of the following can be used to launch EC2 instances on the AWS Cloud?
    - **Amazon Machine Image**
26. Which of the below options cannot be used to upload archives to Amazon Glacier?
    - **AWS Console**
27. Your company is planning to pay for an AWS Support plan.
    
    They have the following requirements as far as the support plan goes: 24x7 access to Cloud Support Engineers via email, chat & phone Response time of less than 15 minutes for any business-critical system faults Which of the following plans will suffice to keep in mind the above requirement?
    
    - **Enterprise**
28. Which of the following are features of an edge location? Choose 3 answers from the options given below.
    - **Distribute content to users**
    - **Cache popular contents**
    - **Used in conjunction with the Cloudfront service**
29. Which of the following storage options provides the option of Lifecycle policies that can be used to move objects to archive storage
    - **Amazon Glacier**
30. Which of the following features of Amazon RDS allows for better availability of databases? Choose the answer from the options given below
    - **Multi-AZ**
31. A client who has adopted AWS Cloud would like to ensure that his systems need to deliver continuous business value & improve supporting processes and procedures.
    
    Which design pillar will he need to focus for achieving this?
    
    - **Operational Excellence**
32. Which of the following encryption techniques is used by AWS KMS for integration with other AWS services?
    - **Envelope Encryption**
33. You are the architect of a custom application running inside your corporate data center.
    
    The application runs with some unresolved bugs that produce a lot of data inside custom log files generating time-consuming activities for the operation team responsible for analyzing them. You want to move the application to AWS using EC2 instances.
    
    At the same time, you want to take the opportunity to improve logging and monitoring capabilities, but without touching the application code. What AWS service should you use to satisfy the requirement?
    
    - **AWS CloudWatch Logs**
34. Your company wants to move an existing Oracle database to the AWS Cloud. Which of the following services can help facilitate this move?
    - **AWS Database Migration Service**
35. Which of the following features of AWS RDS allows you to reduce the load on the database while reading data?
    - **Using Multi-AZ feature**
36. Which of the following terms refers to a physical location around the world where data centers are located in AWS?
    - **Region**
37. A company wants to have a database hosted on AWS.
    
    As much as possible they want to have control over the database itself.
    
    Which of the following would be an ideal option for this?
    
    - **Hosting the database on an EC2 Instance**
38. On which of the following resources does Amazon Inspector perform network accessibility checks?
    - **Amazon EC2 instance**
39. Which of the following services helps to achieve the computing elasticity in AWS?
    - **AWS EC2 Auto Scaling Group**
40. To receive AWS Trusted Advisor Notifications, what actions are required from the customer end?
    - **Set up Notification in Dashboard**
41. Why is Amazon DynamoDB service best-suited for implementation in mobile, Internet of Things (IoT) and gaming applications?
    - **DynamoDB has a flexible data model and single-digit millisecond latency**
42. A client who is using AWS cloud services has multiple environments for the EC2 servers like DEV, QA, PROD respectively.
    
    The client would like to know billing details for each of these environments to make informed decisions related to saving costs.
    
    Using which of the following options the requirements can be achieved?
    
    - **AWS Cost allocation tags**
43. Which of the following does AWS perform on its behalf for EBS volumes to make it less prone to failure?
    - **Replication of the volume in the same Availability Zone**
44. You are requested to expose your serverless application implemented with AWS Lambda to HTTP clients.
    
    ( using HTTP Proxy ) Which of the following AWS services can you use to accomplish the task? (Select TWO)
    
    - **AWS Elastic Load Balancing (ELB)**
    - **AWS API Gateway**
45. You have an EC2 Instance in development that interacts with the Simple Storage Service.
    
    The EC2 Instance is going to be promoted to the production environment.
    
    Which of the following features should be used to grant the EC2 instance suitable permissions to access the Simple Storage Service?
    
    - **IAM Roles**
46. A live online game uses DynamoDB instances in the backend to store real-time scores of the participants as they compete against each other from various parts of the world.
    
    Which data consistency option is the most appropriate to implement?
    
    - **Strongly consistent**
47. Your company is planning to host a large e-commerce application on the AWS Cloud.
    
    One of their major concerns is Internet attacks such as DDoS attacks.
    
    Which of the following services can help mitigate this concern? Choose 2 answers from the options given below.
    
    - **Cloudfront**
    - **AWS Shield**
48. A research team conducting its work in remote locations of the world, without internet access, wishes to leverage Amazon services for their storage.
    
    The team collects petabytes of information at a time.
    
    Which service will best meet to transfer the petabytes of information?
    
    - **AWS Snowball**
49. Which of the following AWS services use serverless technology? Choose 2 answers from the options given below.
    - **DynamoDB**
    - **Simple Storage Service**
50. Which of the following disaster recovery deployment mechanisms has the highest downtime?
    - **Backup and Restore**
51. Which of the following services allows you to analyze EC2 Instances against pre-defined security templates to check for vulnerabilities?
    - **AWS Inspector**
52. Which of the following security services can be used to detect users' personal credit card numbers from data stored in Amazon S3?
    - **Amazon Macie**
53. You are exploring which AWS service will help you to process a large number of data sets.
    
    Choose the correct answer from the given list.
    
    - **EMR**
54. Which of the following services are used by AWS Service Catalog as a combination to create a portfolio of products?
    - **AWS Config & AWS CloudFormation**
55. You are planning to serve a web application on the AWS Platform by using EC2 Instances.
    
    Which of the below principles would you adopt to ensure that even if some of the EC2 Instances crash, you still have a working application?
    
    - **Using a fault tolerant system**
56. Which of the following options would entice a company to use AWS over an on-premises data center? Choose 2 answers from the options given below
    - **Having a highly available infrastructure**
    - **Ability to use resources on demand.**
57. In serverless services such as AWS Lambda, what are the implications of the Shared Responsibility Model?
    - **The user is responsible for IAM roles and identities that can invoke the AWS Lambda functions.**
58. You have 2 accounts in your AWS account- one for the Dev and the other for QA.
    
    Both accounts are configured using consolidated billing.
    
    The management account has purchased 3 reserved instances.
    
    The Dev department is currently using 2 reserved instances.
    
    The QA department is planning to use 3 EC2 instances.
    
    How many reserved instances (purchased by the management account) can be used by the QA Team?
    
    - **One Reserved instance**
59. Which of the following are best practices when designing cloud-based systems? Choose 2 answers from the options below.
    - **Build loosely-coupled components**
    - **Assume everything will fail**
60. Which of the following services can be used to identify an issue with the Amazon CloudWatch service?
    - **AWS Personal Health Dashboard**
61. Which of the following is the amount of storage that can be stored in the Simple Storage Service?
    - **Virtually unlimited storage**
62. You have been hired as an AWS Architect for a company.
    
    There is a requirement to host an application using EC2 Instances.
    
    The Infrastructure needs to scale on-demand and also be fault-tolerant.
    
    Which of the following would you include in the design? (Select TWO)
    
    - **AWS Auto Scaling**
    - **Elastic Load Balancing**
63. A website for an international sport governing body would like to serve its content to viewers from different parts of the world in their vernacular language.
    
    Which is the most suitable service that will allow different language versions of the same website to be served?
    
    - **Amazon CloudFront**
64. You have a mission-critical application that must be globally available at all times.
    
    If this is the case, which of the below deployment mechanisms would you employ?
    
    - **Deployment to multiple Regions**
65. Which of the following can be used to protect against DDoS attacks? Choose 2 answers from the options given below
    - **AWS Shield**
    - **AWS Shield Advanced**
66. Which of the following is a serverless compute offering from AWS?
    - **AWS Lambda**
67. Which of the following are the recommended resources to be deployed in theAmazon VPC private subnet?
    - **Database Servers**
68. A web application co-located in two geographically distinct locations is experiencing degraded service in one of the locations.
    
    What is the most appropriate routing policy to implement in Amazon Route 53?
    
    - **Failover routing policy**
69. What is the concept of an AWS region?
    - **It is a geographical area divided into Availability Zones**
70. In AWS, which security aspects are the customers' responsibility? Choose 4 answers from the options given below
    - **Security Group and ACL (Access Control List) settings**
    - **Patch management on the EC2 instance’s operating system**
    - **Life-cycle management of IAM credentials**
    - **Encryption of EBS (Elastic Block Storage) volumes**
71. Which of the following can be used to manage identities in AWS?
    - AWS IAM
72. You are working on an e-commerce web application running on an EC2 instance.
    
    But it is experiencing a bad performance in browsing and searching use cases when heavy load use-cases are running simultaneously.
    
    The application monitors highlight a bottleneck in the web tier. You decide to re-engineer the application code by decoupling the web tier components from the order's heavy workloads.
    
    What AWS service can support the application change?
    
    - **Amazon SQS**
73. An online streaming company is prohibited from broadcasting its content in certain countries and regions in the world.
    
    Which Amazon Route 53 routing policy would be the most suitable in guaranteeing their compliance?
    
    - **Geolocation**
74. Which of the following are attributes that determine the cost of On-Demand EC2 Instance? Choose 3 answers from the options given below
    - **Instance Type**
    - **AMI Type**
    - **Region**
75. A company wants to utilize AWS storage.
    
    For them, low storage cost is paramount.
    
    The data is rarely retrieved and a data retrieval time of 13-14 hours is acceptable for them.
    
    What is the best storage option to use?
    
    - **S3 Glacier Deep Archive**
76. What are the characteristics of Amazon S3? Choose 2 answers from the options given below
    - **S3 allows you to store virtually unlimited amounts of data**
    - **Objects are directly accessible via a URL**
77. Which AWS service provides a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability?
    - **DynamoDB**
78. In the AWS Billing and Management service, which tool will allow the user to graphically visualize billing and usage over time, particularly monthly running costs?
    - **AWS Cost Explorer**
79. A company is deploying a three-tier, highly available web application to AWS.
    
    Which service provides durable storage for static content while utilizing lower Overall CPU resources for the web tier?
    
    - **Amazon S3**
80. In the AWS Billing and Management service, which tool can provide usage-based forecasts of estimated billing costs and usage for the coming months?
    - **AWS Cost Explorer**
81. Which of the below AWS services allows you to increase the number of resources based on the demand of the application or users?
    - **AWS Autoscaling**
82. Which of the following AWS managed database service provides processing power that is up to 5X faster than a traditional MySQL database?
    - **Aurora**
83. A company is planning to adopt AWS Cloud services to migrate their on-premises workloads.
    
    For that, they require technical support from AWS to design the cloud infrastructure in a better way.
    
    Which of the following features related to AWS Support Plans is correct? (Select THREE)
    
    - **Developer Support plan does not support 3rd Party application services like Ruby on Rails**
    - **Enterprise Support plan should be used for Business Critical use cases with a response time of less than 15 minutes**
    - **Trusted Advisor checks are available for all plans**
84. Which of the following services helps in governance, compliance, and risk auditing in AWS?
    - **AWS CloudTrail**
85. When using On-Demand instances in AWS, which of the following is a false statement when it comes to the costing for the Instance?
    - **You have to pay the termination fees if you terminate the instance**
86. A website that I have designed On Premise has a consistent increase in traffic during certain occasions like Christmas & Thanksgiving.
    
    The first year saw a 20% average increase while the second year saw a 40% average increase.
    
    It is observed that every year I need to spend on new Servers which lie idle after usage.
    
    If I use AWS Cloud resources instead, the advantage that I will get is.
    
    (Choose the best answer)
    
    - **I can save on costs due to the elastic nature of the cloud**
87. Which of the following statements are FALSE when it comes to AWS DataSync? (Choose TWO.)
    - **Can work only over AWS Direct: Connect**
    - **It is an agentless data transfer service**
88. In the AWS Well-Architected Framework, which of the following is NOT a Security design principle to design solutions in AWS?
    - **Apply Security only at the edge of the network**
89. What is the key difference between an availability zone and an edge location?
    - **An availability zone is an isolated location within an AWS region, whereas an edge location will deliver cached content to the closest location to reduce latency**
90. Which of the following security features is associated with a Subnet in a VPC to protect against incoming traffic requests?
    - **Network ACL**

235. In AWS billing, what option can be used to ensure costs can be reduced if you have multiple accounts     

        managed by AWS Organizations?

- **Consolidated billing - Volume Discounts**
1. You have a Web application hosted in an EC2 Instance that needs to send notifications based on events.
    
    Which of the below services can assist in sending notifications?
    
    - **AWS SNS**
2. Which of the following options is TRUE for AWS Database Migration Service (AWS DMS)?
    - **AWS DMS can migrate databases from on-premise to AWS.**
    - **AWS DMS can migrate databases from AWS to on-premise.**
    - **AWS DMS can migrate databases from EC2 to Amazon RDS.**
    - **AWS DMS can have Amazon Redshift and Amazon DynamoDB as target**
3. Which of the following services can be used to automate application code deployment to Amazon EC2 instance?
    - **AWS CodeDeploy**
4. Which of the following are benefits of the AWS's Relational Database Service (RDS)? Choose the 2 correct answers from the options below
    - **Automated patches and backups**
    - **DB owner can resize the capacity accordingly**
5. While using IAM within AWS, they recommend a list of best practices to be used while managing Users & their permissions.
    
    Which of the IAM practices are best to be chosen? Select TWO.
    
    - **Within AWS, services should use roles for accessing other services**
    - **While creating an AWS Account, its best to create an IAM user & use that Account**
6. A company wants to create standard templates for the deployment of their Infrastructure.
    
    Which AWS service can be used in this regard?
    
    - **AWS CloudFormation**
7. You have a distributed application that periodically processes large volumes of data across multiple Amazon EC2 Instances.
    
    The application is designed to recover gracefully from Amazon EC2 instance failures.
    
    You are required to accomplish this task most cost-effectively. Which of the following will meet your requirements?
    
    - **Spot Instances**
8. You want to create a stream processing solution to process and query real-time streaming data using a SQL-based solution.
    
    You are looking for the simplest approach available that AWS provides. What AWS service should you use?
    
    - **Amazon Kinesis Data Analytics**
9. What of the following AWS services allows developers to deploy and manage web applications on the cloud easily?
    - **AWS Elastic Beanstalk**
10. A company is deploying a new two-tier web application in AWS.
    
    The company wants to store their most frequently used data to improve the response time for the application.
    
    Which AWS service provides the caching solution for the company's requirements?
    
    - **Amazon ElastiCache**
11. If you want to take a backup of an EBS Volume, what would you do?
    - **Create an EBS snapshot**
12. Basant & Josiah are transferring 8 TB & 4 TB of data into S3 in a month respectively.
    
    Basant's AWS account is the Management account who's consolidated bill includes Basant's own Account & Josiah's Account.
    
    How much of the total S3 cost will the Management account be charged for both accounts? (Given below are the charges for S3) Price per TB (first 10 TB) = 0.17 * 1024 = $174.08 Price per TB (Next 40 TB) = 0.13 * 1024 = $133.12
    
    - **174.08 * 10 + 133.12 * 2**
13. Which of the following options of AWS RDS allows for AWS to failover to a secondary database in case the primary one fails?
    - **Amazon RDS Multi-AZ deployments**
14. For which of the following AWS resources, the Customer is responsible for the infrastructure-related security configurations?
    - **Amazon EC2**
15. Which of the following statements regarding Amazon Athena are accurate? Select TWO.
    - **Amazon Athena queries data directly from Amazon S3 and there are no additional data storage commitments beyond the object storage**
    - **Amazon Athena is compatible with data formats such as CSV, JSON, ORC, AVRO and Parquet**
16. An administrator is running a large deployment of AWS resources that are spread across several AWS Regions.
    
    They would like to keep track of configuration changes on all the resources and maintain a configuration inventory.
    
    What is the best service they can use?
    
    - **AWS Config**
17. Whilst working on a collaborative project, an administrator would like to record the initial configuration and several authorized changes that engineers make to the route table of a VPC.
    
    What is the best method to achieve this?
    
    - **Use of AWS Config**
18. A company does not want to manage their database.
    
    Which of the following services is a fully managed NoSQL database provided by AWS?
    
    - **DynamoDB**
19. Which of the following tools can be used to create an estimated cost for a new solution to be deployed on AWS Cloud infrastructure?
    - **AWS Pricing Calculator**
20. Your Security Team has some security concerns about the application data stored on S3
    
    The team requires you to introduce two improvements: (i) add “encryption at rest” and (ii) give them the possibility to monitor who has accessed the data and when the data have been accessed. Which of the following AWS solution would you adopt to satisfy the requirement?
    
    - **Server-Side Encryption managed by KMS (SSE-KMS) with CloudTrail**
21. Which of the following services helps provide a connection from on-premises infrastructure to resources hosted in the AWS Cloud? Choose 2 answers from the options given below
    - **AWS VPN**
    - **AWS Direct Connect**
22. Which of the following is a template that contains the software configuration to launch an ec2 instance?
    - **AMI**
23. There is a requirement to host a set of servers in the Cloud for a short period of 3 months.
    
    The instances should be highly available and cost-effective.
    
    The instances can not be interrupted during processing.
    
    Which of the following types of instances should be chosen?
    
    - **On-Demand**
24. Which three actions can Amazon Macie perform on the users' data with artificial intelligence (AI) and machine learning (ML)?
    - **Discover, Monitor, Protect**
25. Which of the following is not a disaster recovery deployment technique?
    - **Single Site**
26. A start-up organization is using the cost explorer tool to view and analyze its costs and usage.
    
    Which of the below statements are correct with regards to the cost explorer tool? (Select TWO)
    
    - **Provides Usage-Based Forecasting**
    - **Provides trends that you can use to understand your costs**
27. The project team requires an AWS service that provides a filesystem simultaneously mounted from different instances of EC2
    
    Which AWS service will satisfy this requirement?
    
    - **Amazon EFS**
28. Which of the below statements is incorrect with regards to the advantages of moving to cloud?
    - **Trade variable expense for capital expense**
29. Project team enhancing the security features of a banking application, requires implementing a threat detection service that continuously monitors malicious activities and 
    unauthorized behaviors to protect AWS accounts, workloads, and data stored in Amazon S3
    
    Which AWS services should the project team select?
    
    - **Amazon GuardDuty**
30. Which of the following support plans offer 24*7 technical support via phone, email, and chat access to Cloud Support Engineers? (Select TWO.)
    - **Business**
    - **Enterprise**