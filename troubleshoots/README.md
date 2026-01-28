failed to connect as my EC2 
was deployed in private subnet so it cannot be reached from tyhe ineternet so instead all traffic will go through the ALB ,this shows up that the application layer is isolated which is the best practice for 3 tier architecture
traffic is directed to EC2 through ALB DNS endpoint
