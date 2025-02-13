# AWS Identity and Access Management (IAM)

Amazon IAM (Identity and Access Management) is a web service that helps securely control access to AWS resources by managing users, groups, roles, and policies.

## Features
- **Fine-Grained Permissions**: Define precise access control using policies.
- **Multi-Factor Authentication (MFA)**: Adds an extra layer of security.
- **Roles and Temporary Credentials**: Allows secure access to AWS services without exposing credentials.
- **IAM Policies**: JSON-based documents defining permissions.
- **Federation and Identity Providers**: Integrate with external identity providers (e.g., Okta, Active Directory).

## IAM Components
1. **Users**: Individual identities that interact with AWS.
2. **Groups**: Collection of users sharing the same permissions.
3. **Roles**: Temporary permissions assigned to AWS services or external users.
4. **Policies**: Define permissions attached to IAM entities.
5. **Identity Providers**: Allow authentication via SAML or OpenID Connect.

## How to Set Up IAM
1. Navigate to **IAM Dashboard** in AWS Console.
2. Create **Users**, **Groups**, or **Roles**.
3. Attach **Policies** to define access levels.
4. Enable **MFA** for additional security.
5. Use **IAM Roles** for cross-account access.

## Best Practices
- Follow the **Principle of Least Privilege**.
- Enable **Multi-Factor Authentication (MFA)**.
- Rotate **Access Keys** regularly.
- Use **IAM Roles** instead of long-term credentials.
- Monitor IAM activities using **AWS CloudTrail**.

## IAM Policy Examples
### S3 Read-Only Access Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": ["arn:aws:s3:::example-bucket", "arn:aws:s3:::example-bucket/*"]
    }
  ]
}
```

### EC2 Full Access Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*"
    }
  ]
}
```

### EBS Volume Management Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["ec2:AttachVolume", "ec2:DetachVolume", "ec2:CreateVolume", "ec2:DeleteVolume"],
      "Resource": "*"
    }
  ]
}
```

### VPC Read-Only Access Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["ec2:DescribeVpcs", "ec2:DescribeSubnets", "ec2:DescribeSecurityGroups"],
      "Resource": "*"
    }
  ]
}
```

## Interview Questions and Answers
### Basic Questions
1. **What is IAM in AWS?**
   - IAM is a service that enables secure access control for AWS resources by managing users, roles, groups, and permissions.

2. **What are IAM policies, and how do they work?**
   - IAM policies are JSON documents that define permissions and are attached to IAM users, groups, or roles to grant or restrict access.

3. **What is the difference between IAM Users and Roles?**
   - IAM Users have permanent credentials, while IAM Roles provide temporary credentials and are used for cross-account or service access.

4. **What is an IAM role, and when should you use it?**
   - An IAM role is an identity with permissions that can be assumed by AWS services, applications, or external entities. It should be used when granting temporary access.

5. **What are the different types of IAM policies?**
   - AWS Managed Policies, Customer Managed Policies, Inline Policies, and Service Control Policies (SCPs).

### Scenario-Based Questions
1. **How would you grant temporary access to an S3 bucket for an external application?**
   - Use an IAM Role with an appropriate S3 policy and enable temporary security credentials via AWS STS (Security Token Service).

2. **An employee is leaving your organization. How do you revoke their AWS access?**
   - Remove their IAM user, revoke permissions, delete access keys, and disable MFA.

3. **How do you enforce MFA for all IAM users?**
   - Create an IAM policy requiring MFA and attach it to all users.

4. **How would you allow an EC2 instance to access an S3 bucket securely?**
   - Assign an IAM Role with an S3 access policy to the EC2 instance.

5. **A developer needs read-only access to AWS services. How would you achieve this?**
   - Assign the AWS managed policy `ReadOnlyAccess` to their IAM user or group.

## References
- [AWS IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/)

---

### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)

