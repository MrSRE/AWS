# Amazon Virtual Private Cloud (VPC)

Amazon Virtual Private Cloud (VPC) enables you to launch AWS resources in a logically isolated virtual network.

## Features
- **Logical Isolation**: Provides a private network space within AWS.
- **Subnetting**: Supports both public and private subnets.
- **Customizable IP Ranges**: Define your own CIDR block.
- **Security Groups & NACLs**: Control inbound and outbound traffic.
- **Internet & NAT Gateways**: Enable internet access selectively.
- **VPC Peering & Transit Gateway**: Connect multiple VPCs securely.
- **AWS PrivateLink**: Secure access to AWS services without exposing traffic to the internet.

## VPC Components
1. **VPC**: The main virtual network container.
2. **Subnets**: Logical partitions of the VPC.
3. **Internet Gateway (IGW)**: Allows public internet access.
4. **NAT Gateway**: Enables private instances to access the internet securely.
5. **Route Tables**: Direct traffic between subnets and networks.
6. **Security Groups (SGs)**: Instance-level firewalls.
7. **Network Access Control Lists (NACLs)**: Subnet-level firewalls.
8. **VPC Peering**: Connects VPCs within or across regions.
9. **Transit Gateway**: Centralized networking for multiple VPCs.
10. **Endpoints**: Secure AWS service access without the internet.

## How to Create a VPC
### Using AWS CLI:
```sh
aws ec2 create-vpc --cidr-block 10.0.0.0/16
```
### Creating a Subnet:
```sh
aws ec2 create-subnet --vpc-id vpc-12345678 --cidr-block 10.0.1.0/24
```
### Attaching an Internet Gateway:
```sh
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --vpc-id vpc-12345678 --internet-gateway-id igw-12345678
```
### Configuring Route Table for Public Access:
```sh
aws ec2 create-route --route-table-id rtb-12345678 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-12345678
```

## Best Practices
- Use **multiple availability zones** for high availability.
- Implement **private subnets** for sensitive workloads.
- Use **VPC Flow Logs** to monitor traffic and security events.
- Restrict access with **Security Groups** and **NACLs**.
- Use **AWS PrivateLink** for secure service access without public exposure.
- Encrypt sensitive data in transit and at rest.

## Interview Questions and Answers
### Basic Questions
1. **What is a VPC?**
   - A VPC is a logically isolated network in AWS that allows control over IP addressing, subnets, routing, and security.

2. **What is the difference between Security Groups and NACLs?**
   - Security Groups operate at the instance level and are stateful, while NACLs operate at the subnet level and are stateless.

3. **How does a NAT Gateway work?**
   - A NAT Gateway allows private instances to initiate outbound internet traffic while preventing inbound traffic.

4. **What is VPC Peering?**
   - VPC Peering allows two VPCs to communicate privately without using the internet.

5. **What is the purpose of an Internet Gateway?**
   - An Internet Gateway enables resources in a VPC to communicate with the internet.

### Scenario-Based Questions
1. **Your private instances need to connect to an external API. How do you enable internet access securely?**
   - Use a NAT Gateway or a proxy in a public subnet.

2. **How do you secure communication between two VPCs?**
   - Use VPC Peering or AWS Transit Gateway.

3. **A web application requires high availability across regions. How do you design the VPC?**
   - Use multi-region VPCs with VPC Peering and Route 53 for DNS routing.

4. **How do you monitor VPC network traffic?**
   - Enable VPC Flow Logs and analyze logs in CloudWatch or S3.

5. **How do you restrict SSH access to EC2 instances in a VPC?**
   - Configure Security Groups to allow SSH access only from specific IP addresses.

## References
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)

---

### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)

