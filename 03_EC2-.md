# Amazon EC2 (Elastic Compute Cloud)

## Overview
Amazon **Elastic Compute Cloud (EC2)** is a web service that provides **resizable compute capacity** in the AWS cloud. It enables users to run virtual servers (instances) without needing to invest in physical hardware.

## Features
- **Scalable** on-demand computing.
- Supports multiple **instance types** optimized for CPU, memory, storage, and networking.
- **Pay-as-you-go pricing model**.
- Integrates with AWS services like **Auto Scaling, Load Balancers, IAM, and VPC**.
- Provides security via **Security Groups, Key Pairs, and IAM Roles**.
- Supports **multiple OS options** (Linux, Windows, macOS).


## EC2 Lifecycle
An EC2 instance goes through the following states:
1. **Pending** - Instance is launching.
2. **Running** - Instance is active and operational.
3. **Stopping** - Instance is in the process of stopping.
4. **Stopped** - Instance is halted but retains its data.
5. **Shutting Down** - Instance is being terminated.
6. **Terminated** - Instance is permanently deleted.

---

## Steps to Launch an EC2 Instance

### 1. Launch an EC2 Instance
```sh
aws ec2 run-instances --image-id <ami-id> --instance-type t2.micro --key-name <key-pair-name> --security-group-ids <sg-id> --subnet-id <subnet-id>
```

### 2. Connect to the Instance via SSH
```sh
ssh -i <key-pair-name>.pem ec2-user@<public-ip>
```

### 3. Assign an Elastic IP (Optional)
```sh
aws ec2 allocate-address
aws ec2 associate-address --instance-id <instance-id> --public-ip <allocated-ip>
```

### 4. Configure Security Groups
```sh
aws ec2 authorize-security-group-ingress --group-id <sg-id> --protocol tcp --port 22 --cidr 0.0.0.0/0
```

### 5. Stop, Start, and Terminate Instances
```sh
aws ec2 stop-instances --instance-ids <instance-id>
aws ec2 start-instances --instance-ids <instance-id>
aws ec2 terminate-instances --instance-ids <instance-id>
```

---

## Basic Questions & Answers

### What is Amazon EC2?
Amazon EC2 is a cloud-based virtual server hosting service that allows users to run applications in the AWS cloud.

### What are the different types of EC2 instances?
- **General Purpose** (e.g., t2, t3, m5) - Balanced compute, memory, and networking.
- **Compute Optimized** (e.g., c5, c6g) - Ideal for compute-heavy applications.
- **Memory Optimized** (e.g., r5, x1) - Used for applications requiring high memory.
- **Storage Optimized** (e.g., i3, d2) - Suitable for workloads needing high-speed storage.
- **Accelerated Computing** (e.g., p3, inf1) - For machine learning and GPU-based tasks.

### What is the difference between On-Demand, Reserved, and Spot Instances?
- **On-Demand** - Pay per hour; best for short-term workloads.
- **Reserved** - Commit for 1-3 years; cost-effective for long-term usage.
- **Spot** - Low-cost instances with potential interruptions; best for batch jobs.

### What is an AMI (Amazon Machine Image)?
An AMI is a **pre-configured OS image** used to launch EC2 instances with specific software and configurations.

### What is the role of a Security Group in EC2?
A Security Group acts as a **virtual firewall** that controls inbound and outbound traffic for EC2 instances.

### How does EC2 pricing work?
- **Pay-as-you-go** (On-Demand)
- **Savings Plans** (1-3 year commitment for lower costs)
- **Spot Instances** (Up to 90% discount for unused capacity)
- **Dedicated Hosts** (Physical servers for compliance needs)

### What happens when you stop vs. terminate an EC2 instance?
- **Stop**: The instance is shut down but remains available in AWS.
- **Terminate**: The instance is deleted permanently, and attached **EBS volumes are removed** unless marked as "keep."

### What is an Elastic IP in EC2?
An Elastic IP is a **static public IP** that remains associated with your instance even after a restart.

### What Happens When the System is Rebooted?
- **Soft Reboot (OS Level Restart)**: The instance retains its **public IP, storage, and instance state**.
- **Hard Reboot (Instance Restart from AWS Console/CLI)**: The instance stops and starts, but retains data and configuration.
- **Reboot does NOT change the instance ID or storage**.


---

## Advanced Questions & Answers

### How does AWS ensure high availability for EC2 instances?
- **Multiple Availability Zones (AZs)** allow failover.
- **Auto Scaling** replaces failed instances.
- **Load Balancers** distribute traffic across healthy instances.

### What is an EC2 Placement Group, and what are the types?
Placement Groups determine how instances are placed in AWS:
- **Cluster** - Low-latency, high-bandwidth networks.
- **Spread** - Instances distributed across hardware to avoid single points of failure.
- **Partition** - Large-scale distributed systems with fault isolation.

### What is the difference between EBS and Instance Store volumes?
- **EBS** (Elastic Block Store) - Persistent storage that remains after stopping the instance.
- **Instance Store** - Temporary storage that is lost when the instance stops.

### How can you migrate an on-premises server to EC2?
Using **AWS Server Migration Service (SMS)** or **AWS Application Migration Service**.

### How does EC2 Auto Scaling work?
Auto Scaling adds/removes instances based on CPU, memory, or custom metrics.

### What are the security best practices for EC2?
- Use **IAM roles** for permissions.
- Restrict SSH access using **Security Groups**.
- Regularly **update OS and applications**.
- Enable **CloudTrail and VPC Flow Logs** for auditing.
- Encrypt EBS volumes and snapshots.

---

## Scenario-Based Questions & Troubleshooting

### You launched an EC2 instance but cannot connect via SSH. What do you check?
1. Ensure **Security Group** allows inbound SSH (port 22) traffic.
2. Check **Network ACLs** for SSH restrictions.
3. Verify the **instance has a public IP or Elastic IP**.
4. Ensure you are using the correct **private key (.pem)** for authentication.
5. Check **VPC route table** for a proper route to the internet.

### An EC2 instance is running but does not have internet access. What could be wrong?
- The **instance is in a private subnet** (needs a NAT Gateway for internet access).
- No **Internet Gateway (IGW)** is attached to the VPC.
- The **Route Table** is missing a `0.0.0.0/0` entry to the IGW.
- The **Security Group or Network ACLs** are blocking outbound traffic.

### How do you recover a lost SSH key for an EC2 instance?
1. **Create a new key pair**.
2. **Detach the root volume** from the instance.
3. **Attach the volume to another instance**.
4. **Copy the new public key into the `~/.ssh/authorized_keys` file**.
5. **Reattach the volume and restart the instance**.

### How do you ensure that only certain IPs can access your EC2 instance?
Modify **Security Groups and Network ACLs** to allow traffic only from specific CIDR ranges.

### What happens if an EC2 instance in an Auto Scaling Group fails?
Auto Scaling will **replace** the instance automatically with a new one.

### How do you set up a high-availability web application using EC2?
- Use **Multiple AZs** for failover.
- Configure an **Elastic Load Balancer (ELB)**.
- Set up **Auto Scaling** for dynamic scaling.
- Store application data in **RDS or S3** instead of instance storage.

---

## Conclusion
Amazon EC2 provides **scalable, secure, and flexible** compute resources in the cloud. By understanding **networking, storage, security, and troubleshooting**, you can optimize your EC2 workloads for **high availability and cost efficiency**.

**Need more help? Reach out! 🚀**

---

## References
- [AWS EBS Documentation](https://docs.aws.amazon.com/ebs/latest/userguide/)

---

### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)