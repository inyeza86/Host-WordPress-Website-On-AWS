![Alt text](/2._Host_a_WordPress_Website_on_AWS.png)

---

# Host a WordPress Website on AWS

This repository contains the resources, scripts, and reference architecture for deploying a highly available, scalable, and secure WordPress website on Amazon Web Services (AWS). The project utilizes several AWS services, including EC2, VPC, Auto Scaling, RDS, EFS, and Route 53, among others.

## Architecture Overview

The WordPress website is deployed within a secure and highly available AWS infrastructure, leveraging multiple AWS services for scalability, security, and fault tolerance. Below are the key components used in the deployment:

1. **Virtual Private Cloud (VPC)**: A VPC is configured with both public and private subnets across two different Availability Zones (AZs) for high availability and fault tolerance.
   
2. **Internet Gateway**: An Internet Gateway is deployed to provide connectivity between instances in the VPC and the Internet.

3. **Security Groups**: Security Groups are established as virtual firewalls to control inbound and outbound traffic for different resources within the VPC.

4. **Multiple Availability Zones (AZs)**: Leveraged two AZs to ensure system reliability and minimize downtime in case of failure in one AZ.

5. **Public Subnets**: Public subnets are used for infrastructure components such as the NAT Gateway and the Application Load Balancer (ALB).

6. **Private Subnets**: The EC2 instances hosting the WordPress website are positioned in private subnets for enhanced security.

7. **NAT Gateway**: Instances in private subnets access the Internet securely via the NAT Gateway for software updates and other outbound traffic.

8. **EC2 Instances**: WordPress is hosted on EC2 instances positioned in private subnets, ensuring that the web servers are secure and isolated from public access.

9. **EC2 Instance Connect Endpoint**: This enables secure SSH access to EC2 instances within both public and private subnets.

10. **Application Load Balancer (ALB)**: An ALB is used to distribute incoming web traffic across multiple EC2 instances in different AZs, ensuring high availability and load balancing.

11. **Auto Scaling Group**: An Auto Scaling Group is configured to automatically adjust the number of EC2 instances based on incoming traffic, ensuring scalability, fault tolerance, and elasticity.

12. **Amazon Elastic File System (EFS)**: EFS is used for shared storage across multiple EC2 instances to store WordPress files, making it easier to scale the application across multiple servers.

13. **Amazon Relational Database Service (RDS)**: Amazon RDS is utilized for a managed MySQL database instance, providing reliable and scalable database services for the WordPress website.

14. **AWS Certificate Manager (ACM)**: Used to secure communication between the ALB and users by providing SSL/TLS certificates for HTTPS.

15. **Amazon Route 53**: Route 53 is used for domain registration and DNS management, allowing users to access the WordPress website via a custom domain name.

16. **AWS Simple Notification Service (SNS)**: Configured SNS for sending notifications related to Auto Scaling Group activities, allowing for real-time alerts on system events.

17. **GitHub**: The web files (WordPress source code and configuration) are stored in a GitHub repository for version control and collaboration.

---

## Prerequisites

To deploy this project, you'll need the following:
- An AWS account with sufficient privileges to create VPCs, EC2 instances, RDS databases, EFS, and other required services.
- A registered domain name for your WordPress site (can be managed via AWS Route 53 or another provider).
- AWS CLI or AWS Management Console access.

---

## Deployment Guide

Follow these steps to deploy your WordPress website on AWS:

### Step 1: Clone the Repository
```bash
git clone https://github.com/inyeza86/Host-WordPress-Website-On-AWS.git
cd Host-WordPress-Website-On-AWS
```

### Step 2: Set Up AWS Infrastructure
1. **VPC and Subnets**:
   - Create a VPC with public and private subnets across two Availability Zones.
   - Deploy an Internet Gateway and NAT Gateway in the public subnets.
   - Ensure the private subnets are connected to the NAT Gateway for Internet access.
   
2. **Security Groups**:
   - Create security groups for the EC2 instances, ALB, and RDS with appropriate inbound/outbound rules.

3. **EC2 Instances**:
   - Deploy EC2 instances in the private subnets.
   - Use the provided startup script to install and configure WordPress on these instances.
   - Attach an EFS volume to store WordPress files across instances.

4. **Application Load Balancer**:
   - Deploy an ALB in the public subnets to balance traffic across EC2 instances in different AZs.

5. **Auto Scaling Group**:
   - Create an Auto Scaling Group to automatically scale the number of EC2 instances based on load.

### Step 3: Configure RDS and EFS
1. **Amazon RDS**:
   - Launch an RDS MySQL instance for WordPress, ensuring it's within the VPC and accessible to the EC2 instances.
   
2. **Amazon EFS**:
   - Set up Amazon EFS for shared storage between your EC2 instances.

### Step 4: SSL Configuration
- Use **AWS Certificate Manager (ACM)** to issue and attach an SSL certificate to your ALB, securing your website with HTTPS.

### Step 5: Set Up DNS with Route 53
- Register your domain name with Route 53 (or transfer an existing domain).
- Create the necessary DNS records (A, CNAME, etc.) pointing to the ALB's DNS name.

### Step 6: Deploy WordPress
- Use the EC2 instances to deploy WordPress by downloading and setting up the WordPress files, configuring the `wp-config.php` file with the RDS MySQL details.
- Ensure that WordPress can read/write to the EFS-mounted directory for shared file access.

---

## Usage

Once the deployment is complete, you can access your WordPress website via the custom domain name you registered with Route 53. The ALB will ensure traffic is distributed evenly across the EC2 instances, and Auto Scaling will manage the instance count based on demand.

---

## Monitoring and Notifications

- AWS **CloudWatch** will monitor your EC2 instances and Auto Scaling Group.
- **AWS SNS** will send notifications for any activities related to scaling events.

---

## Contributing

Contributions to this project are welcome! Feel free to fork the repository and submit pull requests with enhancements or bug fixes.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Resources

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [AWS Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/)
- [WordPress Installation Guide](https://wordpress.org/support/article/how-to-install-wordpress/)
  
---

By following the steps outlined in this README, you'll be able to successfully host a WordPress website on AWS using best practices for high availability, scalability, and security.

--- 
