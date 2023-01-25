# Use Case: Application Migration using AWS Management Console
A company is running their workloads on-premise and would like to migrate some of their applications to the AWS cloud platform. Design, implement, and manage a solution that will meet the company's requirements.

## Task 1: Create a company account and assign users to the following groups
#### Engineer: They should have full admin access except for billing in the company's AWS account.
#### Security: They should have full admin access with billing included in the company's AWS account.
#### Operations: They should only have full admin access to deploy ONLY in the us-east-1 region and should NOT be able to launch in any other region. And they should not have access to billing.
<img width="1464" alt="AWS project #step1" src="https://user-images.githubusercontent.com/94193627/211228706-eba91bdc-0650-42c3-9e35-777bc87e89d3.png">

After creating a "Root user" account in the management console and making sure to secure the account by enabling MFA, and creating an "Administrator" user that has full admin and billing access for security best practice. I then created the three user groups (Engineer, Security, and Operation) teams with specific permissions that will allow them to manage the account's resources. 





## Task 2: Build a publicly available, highly available, and secure Dynamic website with the following requirements:

- Follow the PCI (Payment Card Industry) complience.
- Dynamic application
- Access website based on location 
- Self-healing website
- Disaster recovery 
- Service monitoring of the web server
------------------------------------------------------------------------------------------------------------------------------------------------
## Task 2.1: 

All traffic from users to the website should be encrypted because of PCI (Payment Card Industry) complience.
- To achieve this, I created a certificate and attached it to the domain name
## Task 2.2:
The dynamic web application should be highly available and fault tolerant
- To achieve this, I launched the web application server in two different availability zones. Then created an application load balancer to distribute traffic between the servers. I created a replication of the database in a different region in case of a diasater. And finally, I created an image and snapshot of the web application. 
## Task 2.3:
Because of GDPR (General Data Protection Regulation)compliance only USA customers should be able to access the dynamic website. But users in Europe and other continents should land on a static website. 
- To achieve this, I created an S3 static website and created a Route53 record (subdomain) and modified the permission based on geographical location.
## Task 2.4:
The website should be able to self heal and adapt to the volume of traffic from customers.
- To achieve this, I created a launch template application server and an auto-scaling group
## Task 2.5:
For disaster recovery, the application tier and database tier should be backed up in a different location.
- To achieve this, I created a replication of the database in another region. And created an image of the website server, took a snapshot and stored it to another region.
## Task 2.6:
There should be at least 1 monitoring systems in place to notify the company in case the website is down. 
- I created a Cloudwatch alarm and an SNS topic to alert the company

## Task 3: Build a Dynamic application that is not publicly accessible (Intranet)
- Make sure the server hosting the intranet has the ability to download and update packages on the internet. And users within the company should access the application through the HTTP.

To achieve this, I did the following:
-Launched two servers in private subnets
-Followed the same configuration as Task 2.2
-Created an NAT gateway and attached it to the private servers' route table to allow the servers to download and make updates over the internet.
-Used session manager to allow users to access the web application through HTTP

## Task 4: Allow a third party company to access the company's internal application for auditing purposes
- The third party company should only have access to the intranet application through its web interface using HTTP and the underline database from their own AWS account.
-To achieve this, I created a VPC peering connection with the third party comapny's AWS account. Then created an IAM role and granted full permission access of the "Trusted Advisor" service to the company.

## Task 5: Storage requirements
- The company stores files of customer information and that information contains PII (Personally Identifiable Information) and therefore should be encrypted at rest. The files are regularly accessed for 30 days and then need to be archived and records kept for 5 years. (Recommend a storage solution that will help the company meet this requirement.) 
To achieve this, I created an S3 bucket where the files will be stored and encrypted it using SSE-S3. And then, I created a lifecycle policy on the bucket to transition the files from S3 standard after 30 days then move to Deep Glacier and remain there for 5 years.

# ARCHITECTURE SOLUTION:

![original-aws-project-1 drawio](https://user-images.githubusercontent.com/94193627/211176980-e5955e94-04c1-434f-b6c3-d2df0ebe1604.svg)

## Areas Of Improvement:
#### Make this solution serverless
#### Add more services
