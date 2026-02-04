***1. What is EC2 and how does it work?***
```text
Amazon EC2 (Elastic Compute Cloud) is a web service that provides resizable compute capacity in the cloud. It allows you to launch virtual servers
called instances with various operating systems, CPU, memory, storage, and networking options.
How it works:
You choose an AMI (Amazon Machine Image) to define the OS and software.
Select an instance type for CPU, memory, and network capacity.
Configure security groups (firewall rules) and storage.
Launch the instance → EC2 provisions virtual hardware on demand.
You can connect via SSH (Linux) or RDP (Windows) to manage it.
```
***2. What are the different types of EC2 instances? When would you use each type?***
```text
General Purpose (t3, t4g, m6)---> Balanced CPU, memory, and networking for web servers, small databases, dev/test
Compute Optimized (c6, c7) ---> CPU-intensive tasks: batch processing, high-performance computing, gaming servers
Memory Optimized (r6, x1e) ---> RAM-heavy workloads: in-memory databases, real-time analytics
Storage Optimized (i3, d2) ---> High-speed storage: NoSQL DBs, data warehousing, big data
Accelerated Computing (p4, g5, inf1) ---> GPU/FPGA tasks: AI/ML training, video rendering
Burstable (t3, t4) --->Low baseline CPU, occasional burst: dev/test, microservices
```
***3. What are the differences between a Launch Template and a Launch Configuration?***
```text
Feature	                                         Launch Template	           Launch Configuration
Supports multiple versions	                            Yes	                      No
Supports EC2 instance tags	                            Yes	                      No
Can specify AMI, instance type, security group	        Yes	                      Yes
Recommended for Auto Scaling	                          Yes	                     (but less flexible)
Parameter update	                              Versioned updates possible	     Must create new config
```
***4. How do you ensure high availability and fault tolerance in EC2?***
```text
Multi-AZ Deployment: Launch instances across multiple Availability Zones (AZs).
Elastic Load Balancer (ELB): Distribute traffic across instances.
Auto Scaling Groups (ASG): Automatically replace unhealthy instances.
Backup: Use snapshots and AMIs for recovery.
Monitoring: CloudWatch alarms and status checks.
```
***5. Explain the steps to resize an EC2 instance.***
```text
Stop the instance.
Change the instance type (e.g., t2.micro → t3.medium) in console or CLI.
Ensure the new instance type is compatible with the current AZ and AMI.
Start the instance.
Verify connectivity and performance.
```
***6. How do you troubleshoot EC2 instance connectivity issues?***
```text
Security Group Rules: Check inbound/outbound ports (SSH: 22, RDP: 3389).
Network ACLs: Ensure traffic is allowed.
Elastic IP / Public IP: Verify instance has a reachable IP.
Route Table / Internet Gateway: Required for public internet access.
EC2 Status Checks: Check for system or instance failure.
Firewall / OS Config: Confirm OS firewall allows connection.
```
***7. How do you secure EC2 instances?***
```text
Use IAM roles instead of hardcoding credentials.
Restrict Security Groups (least privilege).
Enable encryption for EBS volumes (KMS).
Regularly patch OS and software.
Enable CloudTrail & CloudWatch logs.
Use Key Pairs for SSH/RDP; disable password login.
Enable termination protection for critical instances.
```
***8. What are Spot Instances and how do you use them in a production environment?***
```text
Spot Instances are spare EC2 capacity at discounted rates (up to 90% cheaper).
Trade-off: Can be terminated by AWS when capacity is needed.
Use Cases: Batch processing, data analysis, stateless microservices, background jobs.

Best Practices for production:

Use Spot + On-Demand combination in Auto Scaling Groups.
Checkpoint workloads to avoid data loss.
Set Spot interruption notices to gracefully handle termination
```
***9. Explain the process of creating a custom AMI in EC2.***
```text
Launch and configure your EC2 instance.
Stop the instance (optional but safer).
Console: Actions → Create Image (AMI).
Enter Name, Description, and select volumes.
Click Create Image → AMI is ready.
Use this AMI to launch identical instances.
```
***10. How do you handle EC2 instance termination protection and accidental data loss?***
```text
Termination Protection: Prevents accidental instance deletion. Enable in console or CLI:

Data Loss Prevention:
Store critical data on EBS volumes (not instance store).
Enable snapshots and backup/replication.
Use Auto Scaling with lifecycle hooks to preserve data on termination.
```
***11. How would you set up EC2 instance user data to run scripts on boot?***
User Data runs scripts automatically on first boot.
Example Linux script to install Nginx:
```bash
#!/bin/bash
yum update -y
yum install -y nginx
systemctl start nginx
systemctl enable nginx
```
Add the script during instance launch → Advanced Details → User Data.
Verify execution: /var/log/cloud-init-output.log.
