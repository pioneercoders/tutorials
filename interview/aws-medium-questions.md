#### 1.What is the difference between Vertical Scaling and Horizontal Scaling in AWS?

* Vertical Scaling:

- Increasing the size of the instance (e.g., t2.micro → m5.large).

- Simple but limited by maximum instance size.

- Requires downtime in many cases.

* Horizontal Scaling:

- Adding more instances to handle increased load.

- Achieved via Auto Scaling Groups + Load Balancers.

- Improves fault tolerance and can scale infinitely (theoretically).


Vertical scaling: Change EC2 instance type in the console.

Horizontal scaling: Use EC2 Auto Scaling with an Application Load Balancer.

#### 2.What are AWS Availability Zones (AZs) and Regions?

- Region: Geographical area (e.g., us-east-1) containing multiple AZs.

- Availability Zone: Physically isolated data center in a region with separate power, cooling, and networking.

- Best practice: Deploy applications across multiple AZs for high availability.

#### 3. Explain the difference between S3 Standard, S3 Standard-IA, and S3 Glacier.

- S3 Standard:

  - High availability, low latency.

  - For frequently accessed data.

  - Cost: Highest of the three.

- S3 Standard-IA (Infrequent Access):

  - Lower cost, higher retrieval fee.

  - For infrequently accessed data.

- S3 Glacier:

  - Archival storage.

  - Retrieval time: minutes to hours.

  - Lowest cost for storage.
























