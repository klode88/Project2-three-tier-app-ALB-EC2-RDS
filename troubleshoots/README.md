Troubleshooting & Issues Faced – Three-Tier AWS Architecture

This section documents the real issues I faced while building the three-tier web application using ALB, EC2, and RDS, and how each problem was understood and resolved.

❌ 1. EC2 instance not reachable via SSH

What happened

When attempting to connect to the EC2 instance using EC2 Instance Connect, the connection failed.

Why this happened

The EC2 instance was deployed inside a private subnet, meaning it has no direct access from the internet.

Resolution / Design decision

This was intentional and correct. In a three-tier architecture, application servers must be isolated.
All external traffic is routed through the Application Load Balancer (ALB).

❌ 2. EC2 cannot be accessed from the internet

What happened

Accessing the EC2 public IP in a browser timed out.

Why this happened

The instance is inside a private subnet with no internet gateway route.

How it was solved

The web application became reachable only through the ALB DNS name, not via EC2.

What this confirms

✔ ALB is the only public entry point
✔ EC2 is protected from direct exposure

❌ 3. Failed to install MySQL on Amazon Linux

What happened

Running:

sudo yum install -y mysql


returned “No match for argument: mysql”.

Why this happened

Amazon Linux 2023 does not include MySQL in its default repositories.

How it was fixed

I installed MariaDB client, which is MySQL-compatible and supported:
How it was fixed

I installed MariaDB client, which is MySQL-compatible and supported:

sudo yum install -y mariadb105

❌ 4. Target group showing “Unhealthy”

What happened

The ALB target group showed the EC2 instance as Unhealthy.

Why this happened

Apache was not fully configured and security group rules were incomplete.

How it was fixed

Installed and started Apache

Opened port 80 on EC2

Allowed inbound traffic from ALB security group

Verified health check path

Result

Targets became Healthy and traffic started flowing correctly.
