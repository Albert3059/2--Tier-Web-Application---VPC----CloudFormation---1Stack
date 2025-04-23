# 2--Tier-Web-Application---VPC----CloudFormation--- one Stack for everthing 

Project Overview:
This project involves the deployment of a highly available, scalable web application infrastructure on AWS using various AWS services such as EC2, Load Balancer (ALB), Auto Scaling Group (ASG), VPC, Subnets, Security Groups, and more. The goal is to create an infrastructure that can automatically scale web application instances based on traffic, while ensuring high availability, security, and fault tolerance.

Key Components:
Amazon VPC (Virtual Private Cloud):

A custom VPC was created with the CIDR block 10.0.0.0/16 to provide isolated networking for the application.

Two types of subnets were created: Public subnets for the bastion host and the Load Balancer, and Private subnets for the EC2 instances running the web application.

An Internet Gateway was attached to the VPC to allow communication between the public subnet and the internet.

Security Groups:

Three security groups were created:

BastionSG: Allows SSH access from any IP to the Bastion Host for management purposes.

ALBSG: Allows HTTP access (port 80) from the internet to the Load Balancer.

AppSG: Allows HTTP (port 8000) traffic from the Load Balancer and SSH (port 22) access from the Bastion Host to the EC2 app instances.

Bastion Host:

A bastion host (EC2 instance) was launched in the public subnet to allow secure SSH access to the private EC2 instances. This instance acts as a gateway to access the instances in the private subnets.

This instance has the BastionSG security group, allowing it to receive SSH connections from any IP.

Elastic Load Balancer (ALB):

An Application Load Balancer (ALB) was set up to distribute incoming HTTP traffic (on port 80) across the app instances in the private subnets.

The ALB forwards requests to a target group, which includes the EC2 instances (web servers) on port 8000.

Listener Rules were configured for the ALB to listen on port 80 and forward traffic to the target group on port 8000.

Auto Scaling Group (ASG):

The Auto Scaling Group (ASG) manages the lifecycle of EC2 instances in response to changes in demand. The instances are automatically scaled up or down depending on the traffic load.

The ASG uses a Launch Template to define the configuration of the EC2 instances (such as instance type, security group, and AMI).

The ASG was configured with a minimum size of 2 instances, a maximum size of 4, and a desired capacity of 2 instances, ensuring high availability and fault tolerance.

Launch Template:

A launch template was created to define the specifications for the EC2 instances that will be managed by the ASG.

The launch template included configurations like the EC2 instance type (t2.micro), key pair for SSH access, and the security group attached to the instances (AppSG).

The EC2 instances run a basic HTTP server using Python (http.server), which serves static content (HTML) on port 8000.

Instance Pages:

Each EC2 instance, when launched, serves a simple HTML page on port 8000, which can be accessed via the Load Balancer.

The instances are healthy and able to serve content, as indicated by the ALB’s Target Group health checks.

Output and Testing:

The public DNS of the ALB was used to test the access to the deployed web application.

Initially, some issues were encountered with security groups and port configurations, but these were resolved by allowing traffic on the correct ports and ensuring that the instances were serving on the proper port.

After testing, the instance served the desired content through HTTP successfully, confirming that the load balancing and scaling mechanisms were working as expected.

Conclusion:
This project successfully deployed a fully functional, highly available, and scalable web application architecture on AWS. The system leverages the capabilities of Auto Scaling, Load Balancer, and EC2 to ensure that the web application can handle varying traffic loads and remain accessible at all times. Additionally, the use of security groups ensures that the infrastructure is properly secured while providing necessary access for management and usage.
 
