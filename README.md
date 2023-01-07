

### STEP 1: The company's AWS account should be accessible and managed by the following groups:

-Engineers Team: They should have full admin access except for billing in the company's AWS account.)

-Security Team: They should have full admin access with billing included in the company's AWS account.)

-Operations Team: They should only have full admin access to deploy ONLY in the us-east-1 region and should NOT be able to launch in any other region.(Don't give Billing access). 


### STEP 2: Build a publicly available, highly available, and secure Dynamic website:

-Because of PCI compliance, all traffic from users to the website should be encrypted. (The site should be highly available and fault tolerant)

-Because of GDPR compliance only USA customers should be able to access the dynamic website. But users in Europe and other continents should land on a static website. (The site should be able to self heal and adapt to the volume of traffic from customers. For disaste rrecovery, the application tier and database tier should be backed up in a different location. There should be at least 1 monitoring systems in place to notify us in case the website is down. And finally, the management of th eweb server should only be done by the Engineering team using the most secured methods as per AWS best practices.)


### STEP 3: Build a Dynamic application that is not publicly accessible (intranet):

-Make sure the server hosting the intranet has the ability to download and update packages on the internet. And users within the company should access the application through the HTTP.


### STEP 4: The company recently hired an auditing company named AUDIT CO, to provide visibility and autiding to the company's internal application.

-AUDIT CO should only have access to the intranet application through its web interface using HTTP and the underline database from their own AWS account.

### STEP 5: Storage requirements:

-The company stores files of customer information and that information contains PII and therefore should be encrypted at rest. The files are regularly accessed for 30 days and then need to be archived and records kept for 5 years. (Recommend a storage solution that will help NAS meet this requirement.) 



---------------------------------------------------------------


![AWS-PROJECT-1 drawio](https://user-images.githubusercontent.com/94193627/210157976-9961e081-7522-4641-9c97-b04d87711035.svg)



