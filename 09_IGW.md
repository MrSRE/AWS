# Internet Gateway in AWS

An **Internet Gateway (IGW)** is a horizontally scaled, redundant, and highly available AWS service that allows communication between instances in a VPC and the internet.

## Features of Internet Gateway
- **Enables internet access** for instances in a public subnet.
- **Redundant and scalable** within an AWS region.
- **No bandwidth constraints** and operates at high availability.
- **Routes traffic via route tables** associated with the VPC.
- **No additional cost** for usage (only data transfer costs apply).

## How an Internet Gateway Works
- An Internet Gateway allows outbound and inbound traffic from the internet.
- It must be attached to a VPC to function.
- The associated route table must have a route allowing `0.0.0.0/0` through the IGW.
- Instances must have a **public IPv4 address** or **Elastic IP (EIP)** to access the internet.
- Security Groups and Network ACLs control access.

## Steps to Configure an Internet Gateway
### 1. Create an Internet Gateway
```sh
aws ec2 create-internet-gateway
```
### 2. Attach the Internet Gateway to a VPC
```sh
aws ec2 attach-internet-gateway --internet-gateway-id igw-12345678 --vpc-id vpc-12345678
```
### 3. Update the Route Table for Public Access
```sh
aws ec2 create-route --route-table-id rtb-12345678 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-12345678
```
### 4. Associate the Route Table with a Public Subnet
```sh
aws ec2 associate-route-table --route-table-id rtb-12345678 --subnet-id subnet-12345678
```

## Internet Gateway vs. NAT Gateway
| Feature             | Internet Gateway (IGW) | NAT Gateway |
|--------------------|----------------------|------------|
| Purpose           | Enables public internet access | Enables outbound internet access for private subnets |
| Works with       | Public subnets | Private subnets |
| Requires Elastic IP | No | Yes |
| Supports inbound connections | Yes | No |
| Supports outbound connections | Yes | Yes |
| Cost | Free | Charged per hour & data transfer |

## Interview Questions and Answers
### Basic Questions
1. **What is an Internet Gateway?**
   - An IGW is a component that allows instances in a VPC to communicate with the internet.

2. **How does an IGW provide internet access?**
   - It allows bidirectional traffic between instances in a VPC and the internet via a route table entry.

3. **Does an IGW provide a static IP?**
   - No, instances need a public IP or an Elastic IP to communicate externally.

4. **Can an Internet Gateway be attached to multiple VPCs?**
   - No, an IGW can only be attached to a single VPC at a time.

5. **What happens if an IGW is detached from a VPC?**
   - The instances in that VPC will lose direct internet access.

### Scenario-Based Questions
1. **Your instances in a public subnet can't access the internet. What could be wrong?**
   - Check if the IGW is attached, the route table has a `0.0.0.0/0` route, and instances have public IPs.

2. **How do you ensure only specific instances can access the internet in a public subnet?**
   - Use Security Groups and Network ACLs to restrict access.

3. **How do you provide internet access to instances in a private subnet?**
   - Use a NAT Gateway or configure a bastion host in a public subnet.

4. **Can an Internet Gateway be used for private communication between VPCs?**
   - No, for private communication, use VPC Peering or AWS Transit Gateway.

5. **How do you restrict access to certain websites from an Internet Gateway?**
   - Use a proxy server, AWS Network Firewall, or a third-party firewall appliance.

## Best Practices
- Attach the IGW to your VPC before configuring public subnets.
- Restrict inbound access with **Security Groups and NACLs**.
- Use **AWS WAF** to filter malicious traffic.
- Monitor traffic using **VPC Flow Logs**.
- Use **Elastic IPs** for static external communication.

## References
- [AWS Internet Gateway Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)

---
### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)

