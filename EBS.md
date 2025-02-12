# Elastic Block Store (EBS)

Amazon Elastic Block Store (EBS) is a scalable, high-performance block storage service provided by AWS. It is designed to work with EC2 instances to store persistent data.

## Features
- **Durable and Reliable**: Data is replicated within an Availability Zone (AZ) to prevent data loss.
- **Scalable**: Easily increase volume size without downtime.
- **Secure**: Supports encryption at rest and in transit.
- **Performance Options**: Multiple volume types to suit different workloads.
- **Backup and Restore**: Supports snapshots for backups and disaster recovery.

## EBS Volume Types
1. **SSD-backed Volumes (For performance-intensive workloads)**
   - **gp3 (General Purpose SSD)**: Cost-efficient, customizable IOPS, and throughput.
   - **gp2 (General Purpose SSD)**: Balances cost and performance with burst capabilities.
   - **io2/io1 (Provisioned IOPS SSD)**: High-performance storage for databases and latency-sensitive applications.

2. **HDD-backed Volumes (For throughput-intensive workloads)**
   - **st1 (Throughput Optimized HDD)**: Ideal for big data and log processing.
   - **sc1 (Cold HDD)**: Lowest cost for infrequent access workloads.

## How to Create an EBS Volume
1. Go to the AWS EC2 Dashboard.
2. Click on **Volumes** under the **Elastic Block Store** section.
3. Click **Create Volume**.
4. Select volume type, size, and other parameters.
5. Attach the volume to an EC2 instance.
6. Format and mount the volume inside the instance.

## EBS Snapshots
- **Point-in-time backup**: Capture the current state of a volume.
- **Incremental**: Only changes since the last snapshot are stored.
- **Cross-Region Copy**: Snapshots can be copied to other AWS Regions.

## Best Practices
- Use **gp3** for cost efficiency with customizable performance.
- Enable **encryption** for sensitive data.
- Take regular **snapshots** for backup and disaster recovery.
- Monitor usage with **CloudWatch** to optimize costs and performance.
- Use **Multi-AZ replication** for high availability.

## Interview Questions and Answers
### Basic Questions
1. **What is Amazon EBS, and how does it differ from instance store volumes?**
   - Amazon EBS provides persistent block storage for EC2 instances, while instance store volumes are temporary and data is lost when the instance is stopped or terminated.

2. **What are the different types of EBS volumes, and when should each be used?**
   - **gp3/gp2 (General Purpose SSD)**: Used for general workloads like boot volumes and small databases.
   - **io2/io1 (Provisioned IOPS SSD)**: Best for high-performance databases and latency-sensitive applications.
   - **st1 (Throughput Optimized HDD)**: Used for big data and log processing.
   - **sc1 (Cold HDD)**: Ideal for long-term, infrequently accessed data.

3. **How does EBS encryption work, and what are its benefits?**
   - EBS encryption uses AWS KMS to encrypt data at rest, during transit, and in snapshots. Benefits include enhanced security, compliance, and ease of management.

4. **How can you increase the size of an EBS volume without downtime?**
   - Modify the volume size in the AWS Console or CLI, then resize the filesystem using `resize2fs` (Linux) or `diskpart` (Windows).

5. **What is an EBS snapshot, and how does it work?**
   - An EBS snapshot is an incremental backup that captures changes since the last snapshot. It is stored in S3 and can be used to restore or copy volumes.

### Scenario-Based Questions
1. **Your EC2 instance is running out of disk space. How would you increase the storage capacity?**
   - Modify the volume size in AWS, extend the filesystem in the instance, and validate the changes.

2. **You need to migrate an EBS volume from one region to another. How would you achieve this?**
   - Take a snapshot of the volume, copy the snapshot to the target region, and create a new volume from it.

3. **An EBS volume attached to an EC2 instance has high latency. What troubleshooting steps would you take?**
   - Check CloudWatch metrics, ensure the volume type matches workload needs, upgrade to a higher-performance volume if necessary, and verify instance I/O limits.

4. **A production database is running on an EBS-backed EC2 instance. How would you ensure high availability and data durability?**
   - Use Multi-AZ replication, enable automated snapshots, and consider RAID configurations for redundancy.

5. **How would you restore data from a corrupted EBS volume using snapshots?**
   - Create a new volume from the most recent snapshot and attach it to the instance as a replacement.

## References
- [AWS EBS Documentation](https://docs.aws.amazon.com/ebs/latest/userguide/)

---

### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)

