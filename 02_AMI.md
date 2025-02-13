# Amazon Machine Image (AMI)

Amazon Machine Image (AMI) is a pre-configured virtual machine template used to create EC2 instances in AWS.

## Features
- **Pre-configured Templates**: Includes OS, applications, and configurations.
- **Custom AMIs**: Create AMIs tailored to your environment.
- **AMI Lifecycle Management**: Automate creation, backup, and deprecation.
- **Multi-Region Support**: Copy AMIs across AWS regions.
- **EBS and Instance Store Support**: Choose storage types for AMI-based instances.

## AMI Components
1. **Root Volume**: Defines the operating system and storage type.
2. **Block Device Mappings**: Specifies additional storage volumes.
3. **Permissions**: Determines AMI access (private, public, or shared).
4. **Launch Permissions**: Control who can launch instances from the AMI.
5. **Architecture**: AMI supports x86, x86_64, or ARM architectures.

## Types of AMIs
1. **Amazon-Provided AMIs**: Pre-built AMIs for common OS distributions.
2. **Marketplace AMIs**: AMIs available for purchase in AWS Marketplace.
3. **Custom AMIs**: Created by users with specific configurations.
4. **Community AMIs**: Publicly shared AMIs by AWS users.

## How to Create an AMI
### From an EC2 Instance:
1. **Prepare the instance**: Install and configure software.
2. **Create an AMI**:
   ```sh
   aws ec2 create-image --instance-id i-1234567890abcdef0 --name "MyCustomAMI" --description "My AMI Backup"
   ```
3. **Monitor AMI creation**:
   ```sh
   aws ec2 describe-images --owners self
   ```
4. **Launch a new instance from AMI**:
   ```sh
   aws ec2 run-instances --image-id ami-12345678 --count 1 --instance-type t2.micro
   ```

### Copy an AMI to Another Region:
```sh
aws ec2 copy-image --source-image-id ami-12345678 --source-region us-east-1 --region us-west-2 --name "CopiedAMI"
```

## Best Practices
- Keep **minimal software** in AMI to reduce size.
- Use **golden AMI strategy** for standardized deployments.
- Automate AMI creation with **AWS Lambda and Lifecycle Manager**.
- Encrypt AMI snapshots for **security**.
- Regularly update and **deprecate old AMIs**.

## Interview Questions and Answers
### Basic Questions
1. **What is an AMI?**
   - AMI is a pre-configured template used to launch EC2 instances in AWS.

2. **What are the types of AMIs in AWS?**
   - Amazon-provided, Marketplace, Custom, and Community AMIs.

3. **How do you create a custom AMI?**
   - By configuring an EC2 instance, creating an image from it, and storing it in AWS.

4. **What is the difference between an EBS-backed AMI and an Instance Store-backed AMI?**
   - EBS-backed AMIs persist data and support snapshots, while Instance Store-backed AMIs use ephemeral storage.

5. **How can you share an AMI with another AWS account?**
   - Modify AMI permissions using AWS CLI or Console.

### Scenario-Based Questions
1. **A team needs to standardize application deployments. How would you achieve this?**
   - Create a golden AMI with pre-installed software and use it for all deployments.

2. **How do you migrate an AMI from one AWS region to another?**
   - Use `aws ec2 copy-image` to copy the AMI to the target region.

3. **Your AMI is not launching properly. What troubleshooting steps would you take?**
   - Check instance logs, verify AMI permissions, and ensure correct kernel version.

4. **How do you automate AMI creation and cleanup?**
   - Use AWS Lambda, Lifecycle Manager, and CloudWatch Events to schedule AMI creation and deletion.

5. **How do you ensure AMIs are secure?**
   - Regularly update AMIs, scan for vulnerabilities, and encrypt snapshots.

## References
- [AWS AMI Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)

---

### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)

