# Elastic File System (EFS)

Amazon Elastic File System (EFS) is a scalable, fully managed cloud-based file storage service designed to be shared across multiple Amazon EC2 instances.

## Features
- **Scalability**: Automatically scales as storage needs grow or shrink.
- **Shared Access**: Supports multiple EC2 instances simultaneously.
- **Performance Modes**: General Purpose and Max I/O for different workloads.
- **Lifecycle Management**: Reduces storage costs by moving infrequently accessed files to a lower-cost tier.
- **Encryption**: Supports encryption at rest and in transit.

## EFS Performance Modes
1. **General Purpose**: Best for latency-sensitive applications.
2. **Max I/O**: Suitable for highly parallel applications requiring high throughput.

## Storage Classes
1. **Standard Storage**: Frequently accessed data.
2. **Infrequent Access (IA)**: Cost-optimized storage for less frequently accessed files.

## How to Create an EFS File System
1. Navigate to the **AWS EFS Dashboard**.
2. Click **Create file system**.
3. Configure **performance mode**, **throughput mode**, and **encryption settings**.
4. Assign a **security group** and **mount targets** for EC2 instances.
5. Mount the EFS file system using the **mount command** or Amazon EFS mount helper.

## EFS vs. EBS
| Feature  | EFS  | EBS  |
|----------|------|------|
| Storage Type | File Storage | Block Storage |
| Accessibility | Multiple instances | Single instance |
| Scalability | Automatically scales | Must resize manually |
| Use Case | Shared storage, containerized applications | Databases, application storage |

## Best Practices
- Use **EFS Infrequent Access** for cost savings on infrequent data.
- Enable **encryption** to protect sensitive data.
- Use **AWS Backup** to manage file system backups.
- Optimize performance by selecting the appropriate **throughput mode**.
- Monitor usage with **AWS CloudWatch** to ensure efficiency.

## Interview Questions and Answers
### Basic Questions
1. **What is Amazon EFS, and how does it differ from Amazon EBS?**
   - Amazon EFS is a scalable, shared file storage service for multiple EC2 instances, whereas Amazon EBS is block storage attached to a single EC2 instance.

2. **What are the key features of EFS?**
   - Scalability, shared access, lifecycle management, performance modes, and encryption support.

3. **How does EFS automatically scale?**
   - EFS scales elastically as files are added or removed without requiring manual resizing.

4. **What are the different EFS performance modes?**
   - General Purpose (low-latency) and Max I/O (high-throughput, parallel applications).

5. **How is data encrypted in EFS?**
   - EFS supports encryption both at rest using AWS KMS and in transit using TLS.

### Scenario-Based Questions
1. **Your application requires shared storage across multiple EC2 instances. Would you use EFS or EBS? Why?**
   - EFS is the preferred choice since it allows multiple instances to share the same file system, whereas EBS is restricted to a single instance.

2. **How would you optimize cost when using EFS?**
   - Use Lifecycle Management to transition infrequently accessed files to the EFS Infrequent Access (IA) storage class.

3. **An application requires very high throughput and parallel access. Which performance mode should be used?**
   - Max I/O mode should be used for highly parallel workloads requiring high throughput.

4. **How would you mount an EFS file system on an EC2 instance?**
   - Use the `mount` command or the Amazon EFS mount helper with the file system ID.

5. **How do you back up an EFS file system?**
   - Use AWS Backup to schedule and manage backups for EFS file systems.

## References
- [AWS EFS Documentation](https://docs.aws.amazon.com/efs/latest/userguide/)

---

### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)

