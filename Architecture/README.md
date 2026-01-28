
Architecture Explanation

This diagram shows a 3-tier architecture deployed inside a VPC.

Users from the internet can only access the Application Load Balancer, which is deployed in public subnets.  
The ALB forwards traffic to EC2 instance in private subnets (application tier).  
EC2 instance then communicate with the RDS database, which is isolated in private subnets (database tier).

This design improves security, scalability, and follows AWS best practice by isolating the application and database layers from direct internet access.
What is deployed in each subnet

### Public Subnets
- Application Load Balancer  
- Internet Gateway route  
- Entry point from the internet

### Private Subnets (Application Tier)
- EC2 instances running the web application  
- Apache installed  
- Only accessible through the ALB
- Private Subnets (Database Tier)
- Amazon RDS (MySQL/MariaDB)  
- No public access  
- Only EC2 security group allowed

---

## Traffic Flow

Internet → ALB (public subnet) → EC2 (private subnet) → RDS (private subnet)
