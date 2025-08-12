#### 1.How would you design a multi-region, highly available architecture for a critical application that must have near-zero downtime?

Regions & Multi-AZ: Deploy workloads in multiple AWS regions (e.g., us-east-1 and ap-south-1) with at least 2 Availability Zones in each.

Global Load Balancing: Use Amazon Route 53 with Latency-Based Routing (LBR) or Geolocation Routing, combined with health checks to failover traffic between regions.

Data Replication:

For RDS/Aurora, use Aurora Global Database or cross-region read replicas.

For DynamoDB, use Global Tables for multi-region, active-active replication.

For S3, enable Cross-Region Replication (CRR).

State Synchronization: Use Amazon ElastiCache Global Datastore for cross-region cache replication.

Failover Strategy: Leverage Route 53 health checks + AWS Global Accelerator for faster DNS failover (sub-second).

Testing: Regularly perform disaster recovery drills (chaos testing).
- Key Considerations: Watch out for data consistency challenges in active-active setups and write conflict

You need to migrate a large on-premises database (50TB) to AWS with minimal downtime. How would you do it?

#### 2. You need to migrate a large on-premises database (50TB) to AWS with minimal downtime. How would you do it?

- Phase 1: Initial Load

Use AWS Snowball Edge for the bulk data transfer to reduce network load.

Ship Snowball to AWS, load data into Amazon S3, then import into RDS or Aurora.

 - Phase 2: Ongoing Sync

Use AWS Database Migration Service (DMS) in Change Data Capture (CDC) mode to replicate incremental changes while the main database stays live.

 - Phase 3: Cutover

Schedule a short downtime window. Stop writes to the old DB, run a final DMS sync, update DNS or connection strings.

- Optional Optimization: Use Aurora Parallel Query or RDS Read Replicas to reduce migration latency.

#### 3.How do you secure an S3 bucket for sensitive financial data while still allowing certain users global read access?

Restrict Public Access: Enable "Block Public Access" at the account and bucket level.

Encryption:

Use SSE-KMS with AWS Key Management Service for encryption at rest.

Use HTTPS (TLS) for encryption in transit.

IAM Policies: Create least privilege IAM policies that allow read-only access to specific IAM roles or users.

Pre-Signed URLs: For temporary global access, generate pre-signed URLs that expire after a set duration.

Logging & Monitoring: Enable S3 Access Logs + CloudTrail Data Events + Macie for sensitive data detection.

Optional: Use S3 Object Lambda to dynamically redact sensitive fields before returning objects.

#### 4.How would you optimize cost for a big data analytics pipeline running on AWS?

Right-Sizing Compute: Use Amazon EMR with spot instances + on-demand mix.

Data Storage Optimization: Store raw data in S3 Glacier Deep Archive and process-ready data in S3 Standard-IA.

Partitioning & Compression: Use Parquet/ORC formats with Athena to reduce scan costs.

Auto Scaling: Enable EMR auto-scaling based on job queue length or CPU utilization.

Lifecycle Policies: Automatically delete old intermediate data using S3 Lifecycle Rules.

Reserved Capacity: For predictable workloads, use Savings Plans or Reserved Instances.

- Pro Tip: In many cases, switching from EMR to AWS Glue + Athena for serverless processing can significantly cut costs.

#### 5.How do you troubleshoot high latency in a VPC-to-VPC connection over VPC Peering?

Check Route Tables: Ensure that routes are correctly pointing to the peering connection.

Security Groups & NACLs: Confirm that both allow inbound and outbound traffic for the required ports.

Bottleneck Identification:

Use VPC Flow Logs to detect packet drops or denied requests.

Check CloudWatch metrics for EC2 CPU/memory pressure.

Test with Multiple AZs: Sometimes cross-AZ traffic increases latency — verify placement.

Consider Alternatives: For higher throughput and lower latency, replace peering with AWS Transit Gateway or AWS PrivateLink.

#### 6.A company wants to implement fine-grained access control for analytics users querying data in S3. How would you implement it?
Use Amazon Lake Formation for central governance.

Define data catalogs in AWS Glue.

Create row-level and column-level permissions in Lake Formation.

Integrate with Athena or Redshift Spectrum so queries automatically respect permissions.

Enable IAM federation for corporate SSO (e.g., with AWS SSO + Okta/AD).

#### 7.How would you implement disaster recovery for an RDS PostgreSQL database with RPO < 5 minutes?
Primary Setup: Multi-AZ deployment for high availability within a region.

Cross-Region:

Use Aurora Global Database for <1-second replication lag, or

For RDS PostgreSQL, use cross-region read replicas with asynchronous replication + logical replication for near real-time sync.

Backup Strategy: Enable automated backups + point-in-time recovery.

Failover: Automate DNS failover with Route 53 health checks.













