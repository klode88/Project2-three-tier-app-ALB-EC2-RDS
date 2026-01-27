# Project2-three-tier-app-ALB-EC2-RDS
Aws 3 tier web app project using EC2 ,ALB and RDS with public and private subnets 

AWS Three-Tier Architecture Project (EC2 + ALB + RDS)
📌 Project Overview;
   In this project, I built a three-tier web application architecture on AWS from scratch.

The goal was to understand how real cloud applications are structured, how traffic flows securely, and how different AWS services work together.
This project uses:
VPC for networking
Public and private subnets for isolation
EC2 for the application server
Application Load Balancer (ALB) for web access
RDS (MariaDB/MySQL) for the database
Security Groups & Route Tables for security and traffic control

- I built everything manually (ClickOps) to fully understand how each component works before automating it later.
What is a Three-Tier Architecture?

A three-tier architecture separates an application into three layers:
Presentation tier (Web) – where users connect (browser / ALB)
Application tier (App) – where logic runs (EC2)
Data tier (Database) – where data is stored (RDS)

****In my project:

The ALB is in public subnets
The EC2 instance is in private subnets
The RDS database is in private subnets
This design is industry standard because it improves:

✅ Security
✅ Scalability
✅ High availability
✅ Maintainability
**** Services I Used and Why

VPC – to fully control networking
*6 subnets (2 public, 4 private) – for high availability and isolation
*Internet Gateway – to allow public internet access
*Route tables – to control how traffic flows
*Security groups – to control who can talk to who
*EC2 – to host the web application
*Apache – to serve the web app
*ALB – to expose the app securely
*RDS (MariaDB) – managed database
*Target group – to register EC2 with ALB

🛠️ Step-by-Step Build (With Screenshots)
1️⃣ Create the VPC
I created a custom VPC so I could control IP ranges, subnets, and routing.
2️⃣ Create and attach an Internet Gateway
This allows public subnets and the load balancer to reach the internet.
3️⃣ Create subnets (2 public, 4 private)
I used:
2 public subnets → ALB
2 private subnets → EC2
2 private subnets → RDS
This spreads resources across availability zones.
4️⃣ Create route tables
Public route table → 0.0.0.0/0 → Internet Gateway
Private route table → internal only
5️⃣ Create security groups
I created separate security groups:
ALB SG → allows HTTP (80) from anywhere
EC2 SG → allows HTTP only from ALB
RDS SG → allows MySQL only from EC2
This follows least-privilege access.
6️⃣ Launch EC2 in a private subnet
This is my application tier.
7️⃣ Install Apache and test locally
I installed Apache, enabled it, and verified it was running.
8️⃣ Create the Application Load Balancer and target group

I created:
Target group
Application Load Balancer
Listener on port 80
9️⃣ Create RDS (database tier)
The database was created in private subnets and secured so only EC2 could access it.
🔟 Install MariaDB client and connect to RDS
From the EC2 instance, I installed the client and connected to the RDS endpoint.
1️⃣1️⃣ Create database and table
I created a database and table inside RDS.
1️⃣2️⃣ Connect web app to database
The app was configured to talk to RDS and tested successfully
Final Result

The application is reachable through the ALB DNS name, the EC2 is private, and the database is fully isolated.
