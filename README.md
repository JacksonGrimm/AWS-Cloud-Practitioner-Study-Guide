# Cloud Computing
Cloud computing is the offloading of computing power that in the past has been traditionally done "in-house" to third-party servers. Service options typically include virtual machines, storage services, and networking services.

Some advantages of using AWS cloud computing services include:

- Flexibility
    - It is easy and cost-effective to experiment with services and quickly implement them.
- Redundancy
    - By offloading computing and storage services from one data store to an Access Zone with redundant Data Centers, the fear of a single point of failure is mitigated.
- Initial Cost and Pay-as-You-Go Model
    - Due to the scale of AWS, the initial cost to get started is low. Instead of spending money to build and maintain in-house data stores, that setup is handled by AWS.
    - The pay-as-you-go model means you only pay for the services you use. You don’t need to predict and allocate resources ahead of time to account for more traffic or decrease when user traffic is low. Instead, with AWS services, you only pay for the resources being used.
- Security
    - All physical security and cloud infrastructure is maintained by AWS. See *Shared Responsibility Model.*
    - Services also have IP blocking and DDoS attack protection.
- Scalability
    - AWS allows you to allocate or remove resources depending on usage.
    - If application traffic increases, the cloud will scale up & down accordingly.

## AWS Compute

### EC2

Elastic Cloud Compute (EC2) service provides virtual machines that run in the cloud. These VMs operate on hardware inside an AWS data center. EC2 Instances are part of AWS's pay-as-you-go pricing, where you only pay for the time the instances are live. Different types of EC2 instances and plans include:

- General Purpose - For applications that require a balance of resources, e.g., web servers.
- Compute Optimized - For tasks that require advanced processing, e.g., batch processing, video transcription, high-performance servers.
- Memory Optimized - For fast delivery and performance of workloads that require a large amount of memory, e.g., databases that cache resources in memory.
- Accelerated Computing - For tasks that require large amounts of data processing by using GPUs, e.g., floating-point calculations, graphics processing.
- Storage Optimized - For services that require quick read and write speeds with large data sets, e.g., DynamoDB, MySQL.

#### Plans

- Spot Instances
    - Reserve an extra spot in the host machine, allowing for a more cost-effective solution, up to 90% off other plans. However, the instance could be stopped with a warning when the instance is needed. Perfect for tasks that can be terminated without consequences.
- Reserved On-Demand Instances
    - Pay for the instances in hours or seconds that they're being used. The user is in control of how long the instance lasts. Can be used in many cases but is great for testing, short-term scaling, and allows for reserving a spot without committing to a contract.
- Savings Plans
    - Save costs on EC2 plans by reserving instances for a term of 1 or 3 years. Great for cases when you know you're going to be launching a server that will be used frequently for a long term.

#### Scaling

- Vertical
    - Allocate more resources to a single EC2 instance.
- Horizontal
    - Launch more EC2 Instances and divert traffic evenly between instances.

### ECS

Elastic Container Service (ECS) is a compute option that allows you to quickly launch your Docker container-based application with AWS. By describing the application, ECS implements compute options, autoscaling, and monitoring, allowing management of large container-based applications.

### EKS

Similar to ECS but with Kubernetes support.

### Security Groups

Security groups exist on EC2 instances to control what traffic is allowed in and out. Security groups are stateful. For example, if you send a request from an instance, the response traffic for that request is allowed to reach the instance regardless of the inbound security group rules. Responses to allowed inbound traffic are allowed to leave the instance, regardless of the outbound rules.

### Beanstalk

Elastic Beanstalk is a service for deploying and scaling web applications and services. Upload your code, and Elastic Beanstalk automatically handles the deployment—from capacity provisioning, load balancing, and auto-scaling to application health monitoring.

## AWS Storage

### EBS

Elastic Block Store (EBS) provides persistent block storage for EC2 instances. Block storage is broken into volumes, which are ideal for frequent updates and throughput-intensive apps, e.g., databases, files where sections need frequent updates. EBS comes in SSD or HDD options.

### S3

Simple Storage Service (S3) is an object storage service that is extremely scalable and resilient with 11 9's of durability (99.999999999%). Used for large-scale data storage, content storage, or even static website hosting. S3 data is automatically encrypted in transit and at rest. S3 options include:

- Intelligent-Tiering (cost-effective)
    - For unknown or changing access patterns, S3 Intelligent-Tiering automatically moves objects to more cost-effective access tiers based on access frequency.
- High Performance
    - For frequently accessed data where performance is crucial. Improve access speeds by 10x and reduce request costs by 50% compared to S3 Standard.
- Infrequent Access (IA)
    - For infrequently accessed objects but still offers fast retrieval when resources are accessed.
- One Zone Infrequent Access (OZ-IA)
    - Similar to IA, but unlike other S3 options, which store data in a minimum of three Availability Zones for redundancy, OZ-IA only uses one. This saves 20% more than the other IA plan.
- Glacier Instant Retrieval
    - Glacier is for archival data that is rarely accessed but still requires instant retrieval. This is for data that is accessed even less frequently than IA, saving up to 68% on storage costs.
- Glacier Flexible Retrieval
    - Similar to Glacier Instant Retrieval, Flexible Retrieval doesn’t support instant retrieval but offers flexibility where large data may need to be accessed. A potential use case is database backups.
- Glacier Deep Archive
    - The lowest Glacier storage cost for storing data long term, 7-10 years, with very infrequent retrieval. Designed for people in highly regulated fields that need to store long-term data.
- Outposts
    - On-site S3 storage plan that's compatible with AWS SDK.

### Instance Store

Instance Stores provide temporary storage located on the host computer's disks. Ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content. Also used to store temporary data that you replicate across a fleet of instances, such as a load-balanced pool of web servers.

### EFS

Elastic File System (EFS) is a serverless file system that lets you share file data without provisioning or managing storage capacity. Being serverless, the Linux-based file systems scale automatically as you add or remove files, paying only for the storage used.

### Snowball

AWS Snowball is a suite of physical devices designed to transfer large amounts of data into and out of the AWS cloud. This service reduces networking costs, speeds up data transfer, secures data, and can overcome challenges associated with large-scale data migrations and transport.

#### Snowcone

- Snowcone is a small, portable computing device for edge computing workloads and data transfer. Weighing about 4.5 pounds, it's compact enough to fit into a standard mailbox, be checked onto an airplane, or be shipped in a standard carrier package. It's designed to be rugged and secure for use in a variety of environments.
  - **Features** include an optional battery for locations without direct power, end-to-end tracking, and both wired and wireless networking capabilities.
  - **Storage Options**: Available with 8TB of HDD storage or 14TB of SSD storage.

#### Snowball

- **Snowball Edge Compute Optimized**
  - Designed for local processing and edge-computing tasks, this version of Snowball provides computing power in addition to data transfer capabilities. It's well-suited for situations requiring local processing, machine learning, and full motion video analysis in environments where internet connectivity is limited or nonexistent.
  - **Features**: Includes 104 vCPUs, 416 GiB of memory, and an optional NVIDIA Tesla V100 GPU for processing tasks. Offers 28 TB of usable NVMe SSD storage for Amazon S3 compatible storage or EBS-compatible block volumes.

- **Snowball Edge Storage Optimized**
  - Focused on large-scale data migrations and transport, this version is optimized for situations where high-capacity storage is paramount.
  - **Storage**: Provides 80TB of HDD storage or up to 210TB of NVMe SSD storage, facilitating efficient data transfer to AWS.

#### Snowmobile

- Snowmobile is an exabyte-scale data transfer service used to move extremely large amounts of data to AWS. It's a physical storage container, hauled by a semi-trailer truck, designed for transferring significant volumes of data that would otherwise be impractical over the internet due to large size, security concerns, or bandwidth limitations.
  - **Features**: A secure, temperature-controlled, GPS-tracked container that ensures the physical safety and security of your data during transport.
  - **Storage Capacity**: Capable of transporting up to 100PB of data in a single shipment, making it suitable for massive data lake migrations, large-scale backup and recovery, and major data center shutdowns or moves.

