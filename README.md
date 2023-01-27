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

## Task 2.1: 

All traffic from users to the website should be encrypted because of PCI (Payment Card Industry) complience.
- To achieve this, I created a certificate and attached it to the domain name

## Task 2.2:
The dynamic web application should be highly available and fault tolerant
- To achieve this, I launched the web application server in two different availability zones. 
<img width="1424" alt="Screenshot 2023-01-25 at 11 46 45 AM" src="https://user-images.githubusercontent.com/94193627/214679043-3569be0e-26ef-4512-8400-dccc2109eef1.png">

<img width="920" alt="Screenshot 2023-01-25 at 12 32 45 PM" src="https://user-images.githubusercontent.com/94193627/214679079-c295e0dd-44fa-4471-b03c-ad7c1dc6931e.png">

<img width="904" alt="Screenshot 2023-01-25 at 12 33 20 PM" src="https://user-images.githubusercontent.com/94193627/214679101-95282fdd-467d-4671-b41c-947bcf34d6fc.png">

I created an application load balancer that is routed by a target group, then a launch template to ensure access to the latest features and improvements of Amazon EC2. and then finally, I created an auto scaling group to distribute traffic between the servers.  

<img width="1051" alt="Screenshot 2023-01-25 at 5 12 42 PM" src="https://user-images.githubusercontent.com/94193627/215172650-1c9f8a9c-c30b-4cdf-b00e-1585e9531f2b.png">

<img width="1015" alt="Screenshot 2023-01-25 at 5 15 37 PM" src="https://user-images.githubusercontent.com/94193627/215165145-600aaa3c-cd78-4a1a-ab0c-8f8334b2ed94.png">

## Task 2.3:
Because of GDPR (General Data Protection Regulation)compliance only USA customers should be able to access the dynamic website. But users in Europe and other continents should land on a static website. 
- To achieve this, I created an S3 static website and created a Route53 record (subdomain) and modified the permission based on geographical location.

<img width="1212" alt="Screenshot 2023-01-25 at 5 30 46 PM" src="https://user-images.githubusercontent.com/94193627/215164766-9988988f-2863-4481-a3e3-3a60a01fd817.png">

Because of cost constraints, I did not register a domain, instead i will be explaining the steps thst need to be taken

## Task 2.4:
The website should be able to self-heal and adapt to the volume of traffic from customers.
- To achieve this, I created a launch template application server and an auto-scaling group

<img width="1194" alt="Screenshot 2023-01-25 at 5 19 09 PM" src="https://user-images.githubusercontent.com/94193627/215165067-fee17cd1-6cf3-4f56-89e6-57e7447b5b22.png">

<img width="1220" alt="Screenshot 2023-01-25 at 5 23 37 PM" src="https://user-images.githubusercontent.com/94193627/215164916-001e07cd-ae54-4645-8ce1-ec0793414406.png">

## Task 2.5:
For disaster recovery, the application tier and database tier should be backed up in a different location.
- To achieve this, I created a replication of the database in another region. And created an image of the website server, took a snapshot and stored it to the other region.

## Task 2.6:
There should be at least 1 monitoring systems in place to notify the company in case the website is down. 
- I created a Cloudwatch alarm and an SNS topic to alert the company

<img width="1303" alt="Screenshot 2023-01-25 at 5 49 39 PM" src="https://user-images.githubusercontent.com/94193627/215164731-e6075788-3acf-438e-98a5-57a908c09709.png">

<img width="1232" alt="Screenshot 2023-01-25 at 5 49 13 PM" src="https://user-images.githubusercontent.com/94193627/215164560-aa5182bb-58ea-4e35-9ee8-c22d669b21e7.png">

## Task 3: Build a Dynamic application that is not publicly accessible (Intranet)
- Make sure the server hosting the intranet has the ability to download and update packages on the internet. And users within the company should access the application through the HTTP.

To achieve this, I did the following:
- Launched two servers in private subnets
- Followed the same configuration as Task 2.2
- Created an NAT gateway and attached it to the private servers' route table to allow the servers to download and make updates over the internet.
- Used session manager to allow users to access the web application through HTTP

## Task 4: Allow a third party company to access the company's internal application for auditing purposes
- The third party company should only have access to the intranet application through its web interface using HTTP and the underline database from their own AWS account.
- To achieve this, I created a VPC peering connection with the third party comapny's AWS account. Then created an IAM role and granted full permission access of the "Trusted Advisor" service to the company.

## Task 5: Storage requirements
- The company stores files of customer information and that information contains PII (Personally Identifiable Information) and therefore should be encrypted at rest. The files are regularly accessed for 30 days and then need to be archived and records kept for 5 years. (Recommend a storage solution that will help the company meet this requirement.) 
To achieve this, I created an S3 bucket where the files will be stored and encrypted it using SSE-S3. And then, I created a lifecycle policy on the bucket to transition the files from S3 standard after 30 days then move to Deep Glacier and remain there for 5 years.

# ARCHITECTURE SOLUTION:

![original-aws-project-1 drawio](https://user-images.githubusercontent.com/94193627/211176980-e5955e94-04c1-434f-b6c3-d2df0ebe1604.svg)

## Areas Of Improvement:
#### Make this solution serverless
#### Add more services
