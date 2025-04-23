# 2--Tier-Web-Application---VPC----CloudFormation--- one Stack for everthing 

# AWS Scalable Web Application Infrastructure

## Project Overview

This project demonstrates the deployment of a **highly available and scalable web application infrastructure** on AWS using key services like EC2, Load Balancer (ALB), Auto Scaling Group (ASG), VPC, Security Groups, and more. The infrastructure automatically scales web app instances based on traffic, ensuring high availability, security, and fault tolerance.

## Key Components

### **Amazon VPC**
- **CIDR block**: 10.0.0.0/16 for isolated networking.
- **Subnets**: 
  - Public: For Bastion Host & Load Balancer.
  - Private: For EC2 instances running the web app.
- **Internet Gateway**: Enables communication between the public subnet and the internet.

### **Security Groups**
- **BastionSG**: SSH access from any IP to the Bastion Host.
- **ALBSG**: HTTP access (port 80) to the Load Balancer.
- **AppSG**: HTTP (port 8000) from Load Balancer to EC2 instances & SSH (port 22) from Bastion Host to app instances.

### **Bastion Host**
- EC2 instance in the public subnet for secure SSH access to private EC2 instances.
- Uses **BastionSG** for SSH access from any IP.

### **Elastic Load Balancer (ALB)**
- Distributes HTTP traffic (port 80) to EC2 instances in the private subnets.
- Configured to forward traffic to EC2 instances on port 8000.

### **Auto Scaling Group (ASG)**
- Manages the lifecycle of EC2 instances based on traffic load.
- Minimum of 2 instances, maximum of 4, with a desired capacity of 2 for high availability.

### **Launch Template**
- Defines EC2 instance configurations, including instance type (t2.micro), security groups, and SSH key pairs.
- EC2 instances run a simple HTTP server on port 8000 to serve static content.

### **Instance Pages**
- Each EC2 instance serves an HTML page on port 8000, accessed through the Load Balancer.
- Health checks ensure all instances are serving content correctly.

## Output & Testing
- **Testing**: Accessed the app using the ALB's public DNS to verify correct load balancing and scaling.
- **Issues**: Fixed security group and port configuration issues to allow traffic on the correct ports.

## Conclusion
This project successfully deployed a scalable and highly available web application on AWS. It uses Auto Scaling, Load Balancer, and EC2 to manage traffic and ensure accessibility. Security groups provide necessary access control, ensuring a secure deployment.
