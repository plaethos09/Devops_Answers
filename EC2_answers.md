

**1.	What is Amazon EC2 and how does it work?**

Amazon EC2 (Elastic Compute Cloud) is a web service that provides secure, resizable compute capacity in the cloud. It allows users to launch virtual server instances that can scale up or down based on computing requirements. 

Some key things to know about Amazon EC2:

- It enables users to launch virtual machines called EC2 instances. These act like physical servers with configurable CPU, memory, storage and networking capacity.

- The instances run on Amazon's physical servers located in data centers around the world. Users don't manage the actual servers but have control over the virtual resources.

- Various configuration options allow instances to be optimized for different purposes like web servers, application servers, databases etc. 

- Users pay for the instances on an hourly basis, only while they are running. This allows capacity to scale up or down on demand.

- Storage volumes called EBS (Elastic Block Store) can be attached to provide persistent storage for data.

- It integrates with other AWS services like auto-scaling, load balancing, VPCs, security groups etc. to enable distributed application architectures.

- The AWS management console and APIs allow full control over instance deployment, management, networking and security.
**2.	What are the different instance types available in EC2 and their use cases?**
Amazon EC2 provides a wide variety of instance types optimized for different use cases. The main instance families are:

- General purpose: Balance of compute, memory and networking resources. Use cases include web servers, code repositories, application servers etc. Examples - M5, T3

- Compute optimized: High performance processors ideal for compute-intensive applications like batch processing, media transcoding, scientific modeling, gaming servers etc. Examples - C5, C6g  

- Memory optimized: Fast performance and large memory for high throughput databases, distributed caches, in-memory analytics etc. Examples - R5, X1e

- Storage optimized: High, scalable storage and IOPS performance for large databases, data warehousing, distributed file systems. Examples - I3, D2 

- Accelerated computing: Hardware GPUs/FPGAs for machine learning, graphics rendering, video encoding, finance and scientific applications. Examples - G4, P3 

- Burstable: Low-cost option where workloads can burst to higher performance when needed. Ideal for websites, blogs, development environments etc. Example - T2

Some other capabilities offered:

- Bare metal: Non-virtualized access to underlying server hardware. 

- Arm-based: Cost-optimized instances powered by Arm-based AWS Graviton processors.

- Infrequent access: Low cost option for workloads that do not need continuous computing power.


**3.	How does EC2 security groups work?**

EC2 security groups act as a virtual firewall to control inbound and outbound traffic to EC2 instances. Some key points on how they work:

- Security groups are attached to EC2 instances during launch. An instance can have multiple security groups.

- Each security group contains a set of firewall rules that filter traffic based on protocol, port and source/destination.

- The rules specify which IP addresses or security groups can access the instance on specified ports.

- By default, all outbound traffic from the instance is allowed but inbound traffic is blocked.

- Security groups only allow rules to allow traffic, not deny. Priority is given to the most restrictive rule if there are overlaps.

- Changes to rules are immediately applied to all associated instances.

- Instances associated with the same security group can communicate with each other over all ports and protocols.

- Separate rules need to be added to enable SSH, HTTP, HTTPS access etc. for external entities.

- Security groups are stateful - any allowed inbound traffic is automatically allowed out.

- Instances in a private subnet can only be accessed through Bastion host/VPN connected to the same security group. 

- Security groups can reference other groups and IP ranges for creating rules.

So in summary, security groups provide instance-level firewall to restrict access based on the application's needs. Rules can be modified to open only necessary ports to enable access.

**4.	Explain the difference between an instance store and Amazon EBS volumes.**

The main differences between EC2 instance store and EBS volumes are:

- Instance store provides temporary block-level storage for an EC2 instance. EBS provides durable and persistent block storage volumes.

- Instance store is physically attached to the host server of the EC2 instance. EBS volumes are network attached virtual drives that can be detached and re-attached to instances.

- Data on instance store will be lost if the instance is stopped or terminated. EBS volume data persists independently from the instance lifecycle.

- Instance store sizes are fixed based on the instance type. EBS volumes can be scaled up to 16TB.

- Instance store provides high IOPS based on the physical host. EBS volumes allow you to specify IOPS up to 64,000 based on volume type. 

- Instance store is included with EC2 instance pricing. EBS volumes incur separate charges based on provisioned capacity and I/O.

- Instance store can't be extended or shrunk. EBS volumes are elastic and can be modified.

- Data on instance store can't be accessed if the instance fails. EBS volumes can be detached and attached to new instances. 

- EBS volumes offer redundancy through replication and can be encrypted. Instance store can't be encrypted or replicated across zones.

In summary, instance store provides ephemeral storage for transient data while EBS offers durable, persistent and scalable block storage for applications that need to retain data.

**5.	What is the purpose of an Amazon Machine Image (AMI)?**

An Amazon Machine Image (AMI) serves as a template for launching EC2 instances. The main purposes of an AMI are:

- It contains the operating system, software, libraries, tools and configurations required to launch an instance.

- It allows instances to be quickly launched without having to manually install and configure software.

- It determines the base characteristics like OS, architecture, region etc. for the instances.

- It acts as a baseline image that can be used to launch multiple identical instances.

- It enables customization by allowing adding/removing software as per application needs.

- It aids consistency and standardization for replicated environments like dev, test, prod.

- It allows versioning and rolling back to previous configurations if issues arise.

- It facilitates migration of existing server environment to the cloud.

- It enables creating golden images with organization standards that can be approved and shared.

- It allows bundling resources like apps, binaries, scripts that can be deployed as a package.

So in summary, AMIs allow reusable configuration templates for launching pre-packaged EC2 instances that are faster, consistent and more reliable.

**6.	How can you increase the instance type of a running EC2 instance?**

There are a couple of ways to increase the instance type (size) of a running EC2 instance:

1. Stop the instance, change its instance type, and restart it.

- Stop the instance from the EC2 console.
- Select the stopped instance, go to Actions > Instance Settings > Change Instance Type.
- Specify a new (larger) instance type.
- Start the instance - it will now have the new instance type.

2. Use Elastic Resize to change the instance type on the fly. 

- From the EC2 console, select the running instance and choose Actions > Instance Settings > Change Instance Type.
- Select Elastic Resize option and specify a new instance type.
- The instance will restart with the new size after a few minutes of outage.

3. Create an AMI from the instance, launch a new larger instance from the AMI, and migrate over.

- Stop the instance if needed, then create an AMI.
- Use the AMI to launch a new instance of desired size.
- Migrate data/apps to new instance and terminate old one.

So in summary, the instance type can be changed by stopping, resize Elastic resize or AMI approach. The first two involve some downtime so for zero downtime, creating a new larger instance from AMI is preferred.

**7.	How does EC2 auto-recovery work and when is it triggered?**

EC2 auto-recovery automatically recovers or restarts EC2 instances that have become impaired or unresponsive due to software issues or underlying hardware problems.

Some key points on how it works:

- Auto-recovery is enabled at the instance level and is off by default. It can be enabled when launching or for existing instances.

- It monitors the instance and checks for impaired status - failed system status checks, unresponsive API calls, failed instance ping, etc.

- If the instance is impaired for a specified period of time (default 5 minutes), auto-recovery will first attempt to restart the instance in place.

- If restart is not successful, it will stop the instance and restart it on a new and healthy host hardware. 

- The instance keeps its public DNS name, private IP, EBS volumes etc. so no reconfiguration is required.

- Diagnostic logs and metrics are checked to identify the root cause - kernel errors, hardware issues, depletion of physical resources etc.

- For recurring issues, additional actions like creating a support case or triggering advanced fleet diagnostics can be configured.

- Auto-recovery actions are logged in EventBridge for auditing and correlation.

``aws ec2 recover-instances --instance-ids <instance-id>``
``aws ec2 attach-volume --volume-id <volume-id> --instance-id <instance-id> --device <device-name>``

So in summary, EC2 auto-recovery automatically restarts impaired instances to maintain application health and availability without manual intervention. It helps recover from underlying hardware/software faults.

**8.	What are the different ways to launch an EC2 instance?**

There are several ways to launch an EC2 instance:

1. AWS Management Console:
- Simple graphical interface to configure instance details and launch. Good for testing or one-off tasks.

2. AWS CLI: 
- Launch using 'aws ec2 run-instances' command. Allows scripting and automation.

3. AWS SDK:
- Programmatically launch instances using language-specific SDK like Python boto3.

4. AWS CloudFormation:
- Create templates to deploy EC2 instances in a reproducible way.

5. AWS Elastic Beanstalk:
- Deploy applications on EC2 instances by uploading code. Handles provisioning and config behind the scenes. 

6. AWS OpsWorks: 
- Manages instances using Chef/Puppet and provides app lifecycle management.

7. AWS Batch:
- Schedule batch computing jobs and dynamically launch EC2 instances to run them.

8. Third Party Tools:
- Tools like Terraform allow declaring infrastructure as code and deploy EC2 resources.

So in summary, EC2 offers APIs, CLIs, SDKs and tight integration with other AWS services to enable launching instances in scripts, templates or config files for automation and control.

**9.	How do you monitor EC2 instances using CloudWatch?**

Amazon CloudWatch can be used to monitor various metrics and logs of EC2 instances. Some ways to monitor EC2 instances with CloudWatch are:

-CPU Utilization - Track overall CPU usage and per CPU core usage to detect spikes or under utilization.

-Network Traffic - Monitor bytes/packets in/out of the instance to analyze network performance. 

-Disk Metrics - Track disk reads/writes, IO latency to monitor disk bottlenecks.

-Memory Usage - Monitor memory consumption and pinpoint any memory leaks or saturation.

-Status Checks - Get system/instance status checks to identify any impaired instances.

-Logs - Stream instance logs like application logs, ssh logs, kernel logs to CloudWatch for tracking events.

-Custom Metrics - Push custom app-level metrics like request count, error rates etc. for debugging. 

-Alarms - Set alarms on any metric crossing thresholds to trigger notifications or auto-scaling actions.

-Dashboards - Create dashboards to visualize metrics for instance health, bottlenecks.

-Events - Log state changes like instance launch, shutdown, termination as CloudWatch events.

-Periodic Insights - Schedule periodic EC2 instance assessments to proactively surface issues.

So in summary, CloudWatch provides visibility into key EC2 performance, health, logs and events to help monitor, analyze and set alerts.



**10.	Explain the differences between on-demand, spot, and reserved instances.**

The three main EC2 instance purchasing options have different costs and flexibility characteristics:

On-Demand instances:
- Most flexible option with no long term commitments or upfront payments.
- Pay for compute capacity by the hour with no minimum fees.
- Recommended for short term, spiky, unpredictable workloads.
- Highest per hour cost but no risk of disruption.

Reserved Instances:
- Provide discounted hourly rate for 1 or 3 year terms with upfront payment. 
- Useful for steady state production workloads to save costs.
- Capacity is reserved and always available for the term. 
- Loss of payment if not fully utilized.

Spot Instances: 
- Bid on spare EC2 capacity and run when bid exceeds spot price.
- Upto 90% discount compared to On-demand pricing if utilized.
- Instance can be interrupted with 2 minute warning if spot price exceeds bid.
- Useful for fault tolerant workloads like batch jobs, distributed computing.
- No minimum commitment - use and pay for only the time it runs.

So in summary, the optimal purchase model depends on workload patterns, flexibility needs and willingness to take interruptions vs gain significant cost savings.

**11.	How does EC2 placement groups work and what are their use cases?**

EC2 placement groups allow you to influence the placement of a group of interdependent instances to meet the needs of your workload. There are two types of placement groups:

- Cluster - Packs instances close together in a single Availability Zone. Useful for workloads that benefit from low network latency, high network throughput like Hadoop, distributed computing.

- Spread - Spreads instances across underlying hardware. Useful for applications that need to maximize high availability like critical databases, webapps. Protects against correlated hardware failures.

Some key points on how placement groups work:

- Instances can be launched into a new or existing placement group.

- Placement groups can span multiple instance types but capacities need to be considered.

- Network traffic between instances in the same placement group is optimized. 

- Spread placement groups can span multiple AZs for high availability.

- By default, EC2 distributes instances for best resiliency. Placement groups allow overriding this behavior. 

- There are limitations on moving existing instances into a placement group.

- AWS recommends homogenous instances with consistent utilization forPlacement groups benefit network and hardware sensitive applications like HPC workloads, clustered databases, distributed cache layers etc. that need performance isolation or high availability.

So in summary, placement groups provide instance placement control to optimize performance, lower latency and improve fault tolerance for specific use cases.

**12.	How can you encrypt data on EC2 instances?**

There are a few ways to encrypt data on EC2 instances:

1. Encrypt EBS volumes - EBS volumes can be encrypted at rest using AES-256 encryption. The volumes and snapshots will be encrypted.

2. Use third party disk encryption tools - Software like BitLocker for Windows or LUKS for Linux can be used to encrypt data on the attached EBS volumes.

3. Encrypt data before storing on instance - Encrypt sensitive data before storing it on the EC2 instance using encryption libraries or tools.

4. Use AWS Key Management Service (KMS) - KMS can be used to generate encryption keys, encrypt data before storing on EBS volumes.

5. Encrypt data in transit - Use SSL/TLS certificates to encrypt data in transit to and from the EC2 instance. 

6. Use AWS Certificate Manager (ACM) - Easily provision SSL/TLS certificates through ACM for encrypting connections.

7. Leverage AWS CloudHSM - For managing encryption keys and accelerating cryptographic operations.

8. Restrict access to data - Use IAM roles, security groups to control access to EC2 instances and encrypted data.

So in summary, EBS encryption, SSL connections, KMS integration and tools like CloudHSM provide a secure way to encrypt data at rest and in transit for EC2 instances.

**13.	What is the difference between an EC2 instance and an EC2 container?**

The key differences between EC2 instances and EC2 containers are:

- EC2 instances are virtual machines with dedicated compute resources like CPU, memory, storage and network. EC2 containers provide lightweight packaging of applications using container technology like Docker.

- Instances require selecting an OS, capacity, configuring and maintaining. Containers abstract away the OS and infrastructure so you just run the application stack.

- Instances are isolated from each other and have root access to OS. Containers share the host OS kernel and binaries but isolate the application processes.

- Instances are billed for provisioned capacity while containers are billed per second based on usage. Containers allow higher density.

- Instances are provisioned in minutes while container deployments are faster in seconds. Containers facilitate rapid scaling.

- Instances require installing apps and dependencies. Containers package up code, configs, dependencies for quick deployment.

- Instances are configured individually. Containers use baked images allowing reuse and consistency.

- State is ephemeral in containers. Instances use storage like EBS to persist data.

- Containers are more portable across cloud environments. VMs have more provider specific dependencies.

In summary, containers provide lightweight, portable application deployment while instances are isolated machines with persistent storage more suitable for legacy apps. The choice depends on the application architecture and resource needs.
**14.	How can you resize an EBS volume attached to an EC2 instance?**
There are a couple of ways to resize an EBS (Elastic Block Store) volume attached to an EC2 instance:

1. Stop the instance, detach the volume, modify the volume size, reattach and restart the instance.

- Stop the EC2 instance
- Right click the attached EBS volume in the EC2 console and select "Detach Volume"
- Click on the detached volume and select "Modify Volume"
- Change the volume size to the desired capacity  
- Reattach the resized volume to the EC2 instance
- Start the instance again 

2. Resize the volume online while the instance is running

- From the EC2 console, right click on the attached volume and select "Modify Volume"
- Change the size and select "Expand immediately"
- The API will take a snapshot, create a larger volume from the snapshot and seamlessly resize the filesystem online

Things to note:

- Only EBS volumes backed by SSD and Gp3 can be resized online
- The instance needs to support online resizing if using the online method
- Data is retained, only the allocated capacity increases
- Filesystem needs to be resized after increasing volume size to use the extra space

So in summary, EBS volume size can be easily increased either offline or on the fly based on the instance support and volume type. The data is retained and only usable capacity expands.

Here are the steps to resize an EBS volume using AWS CLI:

1. Check the current size of the EBS volume:

```bash
aws ec2 describe-volumes --volume-ids vol-123456 --query Volumes[].Size
```

2. Detach the volume from the EC2 instance: 

```bash
aws ec2 detach-volume --volume-id vol-123456
```

3. Modify the size of the detached volume:

```bash 
aws ec2 modify-volume --volume-id vol-123456 --size 100
```

4. Attach the resized volume to the original EC2 instance:

```bash
aws ec2 attach-volume --volume-id vol-123456 --instance-id i-123456 --device /dev/sdf
```

5. Login to the EC2 instance and resize the filesystem to use the newly added storage space. 

For Linux using ext filesystems:

```bash
sudo resize2fs /dev/xvdf
```

For Windows, use Disk Management console to extend the volume.

So in summary, AWS CLI allows resizing an EBS volume by detaching, modifying size, reattaching and expanding the filesystem using simple CLI commands.

**15.	What is the purpose of EC2 instance metadata and how can it be accessed?**
EC2 instance metadata is data about an active EC2 instance that can be used to configure or manage the running instance. 

Key things to know about EC2 instance metadata:

- It is exposed by a REST API endpoint to the instance at http://169.254.169.254/

- It provides information like public hostname, AMI ID, security groups, block device mappings, AWS services allowed etc.

- It allows assigning user-defined key-value pairs for custom configuration data

- It can be accessed from within the instance using API calls to the metadata endpoint.

- No authentication is required to access instance metadata.

- Metadata can be used to dynamically configure instances with info they need to run applications

- Tools like CloudInit utilize metadata to initialize instances during bootstrapping

- Session manager plugins can be injected via metadata to allow SSH-like access

- AWS Config, AWS Tags can be accessed via metadata for visibility into environment  

- Care must be taken to not expose sensitive data in metadata that could be abused if the instance is compromised.

So in summary, EC2 instance metadata provides a simple way to dynamically customize and configure instances with the information they need to operate in an AWS environment.


**16.	Explain the difference between public and private IP addresses in EC2.**
The key differences between public and private IP addresses in EC2 are:

Public IP addresses:

- Used for communicating with the instance from the public internet 

- Mapped to the instance's public DNS name to allow internet traffic

- Remains static throughout the instance lifetime by default

- Can be dynamically associated/disassociated with instance

- Public IP can only be assigned if instance is in public subnet

Private IP addresses:  

- Used for communication between instances within the same VPC 

- Allowed to be used with on-premise networks over VPN/DX  

- Assigned to instance from the subnet range upon launch

- Stays with the instance until termination

- Main route table automatically maps private IPs to each other

- Must use NAT Gateway to allow internet access from private IPs

- Can leverage PrivateLink to access AWS services privately 

In summary, public IPs enable external internet access to EC2 instances while private IPs allow secure communication internally between instances and VPC resources based on security groups and routing tables.

**17.	How can you access EC2 instances without using a key pair?**

There are a few ways to access EC2 instances without using a key pair:

- Session Manager - Provides interactive shell access using AWS CLI without SSH. Does not need open inbound ports.

- AWS Systems Manager - Can remotely run commands and scripts on EC2 via SSM agent. Uses IAM permissions instead of keys.

- Amazon EC2 Serial Console - Access EC2 console output over a serial connection. Useful for diagnosing boot and network issues.

- AWS OpsWorks - Manage EC2 instances using Chef/Puppet. Access controlled via IAM.

- Remote Desktop Protocol (Windows) - Enable RDP access in security group and connect using password credentials.

- VM Import (Linux) - Import an instance with password authentication instead of keys.

- SSH Agent Forwarding - Register key pair on a bastion host and use agent forwarding over tunnels.

- AWS Cloud9 - Spin up a Cloud9 IDE and connect to instance through VPC networking.  

- Third-party Tools - Tools like Terraform can run scripts on EC2 by passing temp credentials.

So in summary, while key pairs are the most common and secure way, AWS provides alternative mechanisms like SSM, Serial Console, IAM roles etc. to access EC2 instances without direct key usage.

**How to access instance if key pair is lost**

Here are some options if you lose the key pair for your EC2 instance and can no longer access it:

- Stop the instance and detach the root EBS volume. Attach this volume to another instance as a data volume and modify authorized_keys file with a new keypair.

- Boot the stopped instance in recovery mode to reset SSH credentials. This may not work for all OS types.

- Retrieve administrator password through instance console output. Stop instance, get console output and search for password.

- Rebuild the instance - Take an AMI snapshot, launch a new instance from AMI with a new key pair.

- Use AWS Systems Manager Session Manager to start a session without SSH. Needs SSM agent to be configured.

- Launch another instance in same security group, modify original instance's security group to allow SSH from new instance. Use new instance as a jump host. 

- Create an AMI from the instance, launch new instance from this AMI with a new keypair.

- If EBS root volume is encrypted with default KMS key, you can force stop the instance and it will be unrecoverable.

So in short, stopping the instance and attaching root volume to another instance is usually the simplest way to reset access. SSM Session Manager is also very helpful if already setup.
**18.	What is the significance of user data in EC2 instances?**

User data in EC2 allows running custom scripts or providing configuration data during the boot process of an instance. Some key uses of EC2 user data are:

- Automatically configure instances during launch e.g. installing packages, updating config files 

- Pass configuration data like database connection strings, app settings to applications on startup

- Join instances to a Windows Active Directory domain during launch

- Register instances with a CMDB or monitoring system upon boot

- Run initialization scripts to prepare instances e.g. mounting volumes, updating repos

- Download common dependencies, libraries needed by applications 

- Install and start up prerequisite services like web servers, databases

- Add ssh keys or VPN certificates to instances before connecting

- Configure log collection agents and plugins when launching

- Bake common repetitive initialization tasks into AMIs 

- Perform system hardening and security tasks on first launch

- Pass ephemeral bootstrap data only needed during initialization

So in summary, EC2 user data executes during the first boot to automatically customize, configure and prepare newly launched instances instead of manual steps after launch.
**19.	How can you troubleshoot connectivity issues with EC2 instances?**

Here are some ways to troubleshoot and diagnose connectivity issues with EC2 instances:

- Check instance status in EC2 console - any impaired/degraded checks indicating issues.

- Verify security group rules allow ingress and egress on required ports and protocols.

- Check NACL rules are not blocking traffic unintentionally.

- Check route table has valid entries and does not incorrectly route traffic.

- Try to connect from another instance in same security group to isolate issues.

- Use EC2 Serial Console to check for boot and network errors.

- Check VPC Flow Logs for any rejected or dropped traffic. 

- Usetraceroute and ping to check connectivity and packet loss at each hop.

- Inspect DNS resolution and logs for any failed lookups.

- Verify instance has a public IP address assigned if trying to access externally.

- Check network interface attachment and status for any detachment issues.

- Monitor metrics like packet drops, network traffic in CloudWatch for anomalies.

- Review VPC VPN tunnels/gateways health if connectivity is over VPN.

- Disable firewalls/proxy to isolate if issue is external to the instance.

- Leverage AWS Systems Manager to remotely verify agent logs and processes.

So in summary, methodically verify security group, NACL, routes, interface, DNS, VPNs and use tools like ping, traceroute, VPC Flow Logs, CloudWatch metrics to pinpoint the source of any network connectivity issues.

**20.	What are EC2 instance profiles and how are they used?**

EC2 instance profiles allow EC2 instances to securely access AWS services and resources without exposing or managing access keys on the instance itself. 

Key points about instance profiles:

- Instance profiles contain IAM roles which define the permissions that the EC2 instance will have.

- The temporary security credentials associated with the IAM role are automatically made available on the EC2 instance.

- Applications running on the EC2 instance can use these credentials to access AWS services like S3, DynamoDB etc.

- IAM roles can be dynamically attached or detached from an instance to control access.

- Credentials are automatically rotated ensuring a secure access mechanism.

- Removes need to distribute long-term credentials or access keys on individual EC2 instances.

- Credentials are provided via the metadata endpoint and no further configuration is needed.

- No access keys are stored on the server itself minimizing the blast radius if the server is compromised. 

- Fine grained control over expiration, permissions provided through IAM policies.

So in summary, EC2 instance profiles provide applications on EC2 easy access to other AWS services in a secure and managed way through temporary credentials.
**21.	Explain the concept of EC2 instance states and transitions.**

EC2 instances transition through different states during their lifecycle. The main EC2 instance states are:

- Pending - The instance is being initialized and is not yet ready for use.

- Running - The instance has booted up and is running applications.

- Stopping - The instance is in the process of shutting down but has not fully stopped yet. 

- Stopped - The instance has been shutdown but the data on any EBS volumes remains persisted.

- Terminating - The instance is being prepared for termination and permanent instance retirement. 

- Terminated - The instance has been permanently terminated and can no longer be accessed.


The allowed EC2 instance state transitions are:

- Pending -> Running

- Running -> Stopping -> Stopped 

- Stopped -> Starting -> Running

- Running -> Rebooting -> Running

- Running -> Terminating -> Terminated

- Stopped -> Terminating -> Terminated 

The state transition gives insight into what is currently happening with the instance. Monitoring tools track state changes over time. Certain instance actions like restart or resize cause transitions between restricted states.

**22.	How does EC2 instance placement work in different Availability Zones?**

EC2 instances can be launched in different Availability Zones (AZs) within a region to achieve high availability and fault tolerance. Here is how EC2 placement works with AZs:

- Each AZ represents an isolated location with its own power, networking and physical infrastructure.

- AZs in a region are interconnected through low-latency links for high throughput and redundancy.

- By default, EC2 distributes instances evenly across all AZs to maximize availability.

- When launching multiple instances across AZs, AWS will attempt to place each instance in a separate AZ.

- If too many instances are launched for available capacity in AZs, some may get grouped in the same AZs.

- You can specify a specific AZ at launch to control placement. Useful for instance proximity to other resources. 

- For high availability of applications, deploy instances across two or more AZs so failure of one AZ doesn't affect overall application.

- Data replication tools can be used across AZs for resilient data storage.

- Elastic IP addresses allow remapping instances to new AZs in case of AZ failures.

So in summary, spreading EC2 instances across AZs provides high availability protection from AZ outages. Careful placement considering failure domains is needed for mission critical applications.

**23.	What is the difference between instance store-backed and EBS-backed instances?**
The key differences between EC2 instance store-backed vs EBS-backed instances are:

Instance store-backed:

- Temporary block level storage volumes attached to the physical host computer of the EC2 instance.

- Instance store volumes cannot be detached or attached to another instance. Data is lost on instance termination.

- Performance is very high due to direct SSD/HDD attachment. 

- Well suited for temporary data like buffers, caches, scratch space.

- Instance configuration determines the size and number of instance stores.

EBS-backed:

- EBS volumes are network attached virtual drives that act as persistent block storage. 

- EBS volumes can be detached and re-attached to another instance. Data is persisted beyond instance lifecycle. 

- Allows scaling storage based on demand by modifying volume size and type.

- Can leverage EBS features like encryption, snapshots for backups/versioning.

- Recovery is possible if instance fails by re-attaching EBS volume to new instance.

- Recommended for most persistent storage use cases like databases, file systems etc.

So in summary, instance stores provide high performance ephemeral storage while EBS volumes enable long-term durable and flexible storage. The choice depends on persistence needs.


**24.	How does EC2 Auto Scaling work and how can it be configured?**
EC2 Auto Scaling allows automatically adding or removing EC2 instances based on defined conditions to maintain application availability and optimize costs. Here is an overview:

- An Auto Scaling group is created that launches EC2 instances based on a launch configuration specifying instance properties. 

- Scaling policies define when to scale out (add instances) or scale in (remove instances) based on metrics like CPU usage, request count etc.

- Dynamic scaling uses target tracking to maintain a metric at a target value.  

- Static step scaling adds or removes a fixed number of instances when a threshold is breached.

- Simple/Step scaling policies can be created via the AWS console. More advanced predictive scaling requires AWS Auto Scaling service.

- Auto Scaling monitors the scaling metrics and adds or removes instances to keep resource utilization at optimal levels.

- Auto Scaling integrates with ELB for distributing incoming application traffic across instances.

- Lifecycle hooks allow custom actions like deployments or instance prep before instance goes in service. 

- Auto Scaling is free, you only pay for the underlying EC2 instances launched.

So in summary, Auto Scaling provides automated and self-adjusting horizontal scaling capability to optimally distribute application load across a pool of EC2 instances.

**25.	Explain the concept of EC2 instance metadata and user data.**
EC2 instance metadata and user data allow customizing and configuring instances when they boot.

Instance metadata:

- Data about an instance that apps on the instance can access like MAC address, instance ID etc.

- Exposed via a special endpoint http://169.254.169.254 that is available from within the instance.

- Allows assigning custom key-value pairs for own use cases. 

- Used to provide info like credentials, network details that instance apps may need.

- Can access by querying the endpoint e.g. using curl from within instance.

- Used by libraries and SDKs to discover properties of an instance.

User data:

- Custom bootstrap script that executes only during initial instance launch.

- Allows automating instance configuration and setup on first boot.

- User data is passed to the instance at launch as plain text or as base64 encoded data.

- Max size is 16 KB for plain text or 64 KB when base64 encoded.

- Executed by the instance OS system upon startup e.g cloud-init service in Linux. 

- Can install packages, write files, mount disks etc. using shell scripts or specialized tools like CloudFormation helpers.

So in summary, metadata provides info about the instance while user data executes custom logic during instance first boot. Both are useful for automatically configuring instances.

**26.	What is the maximum number of EC2 instances that can be launched in a VPC?**
There is no fixed limit on the maximum number of EC2 instances that can be launched in a VPC (Virtual Private Cloud). The upper limit depends on these factors:

- Instance type - The total vCPUs and memory across all instances must fit within the VPC CIDR IPv4 address space and memory limits.

- Private IPv4 addresses - VPC CIDR ranges have between 16 million ( /16 block) to 2 million (/20 block) available private IP addresses that can be assigned.

- On-Demand instance limit - Per-region limit on running On-Demand instances per account (by default set to 1152 vCPUs). Can be increased by request.

- VPC limits - Default limits per VPC on routes, network interfaces, security groups etc. Can be increased.

- Service limits - Account limits for specific instance types and families e.g. m4 family.

- Availability Zone capacity - Physical capacity available across AZs for instances.

- Tenancy - Capacity is shared between Dedicated and Default tenancy.

So in essence, the private IPs, subnets, net interfaces impose a practical limit typically in 100s of instances per VPC. The actual number depends on instance sizes and VPC address space. Larger instances further constrain the limit.

**27.	How can you enable enhanced networking for EC2 instances?**
There are a couple ways to enable enhanced networking for EC2 instances to provide lower latency and higher throughput:

1. Elastic Network Adapter (ENA)

- Supports network speeds up to 100 Gbps for supported instance types.

- Uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities.

- Enabled by default for most new general purpose instances. 

- For Linux, install ENA driver at instance launch to leverage enhanced networking.

2. Elastic Fabric Adapter (EFA)

- Provides OS-bypass capabilities for very low latency and high throughput.

- Supports message passing interface (MPI) traffic for HPC applications.

- Supported on compute optimized (ex. C5, M5) and some general purpose instances.

- Needs EFA driver installed on Linux, Windows AMIs to enable enhanced networking.

- Well suited for tightly coupled workloads like machine learning, high frequency trading.

So in summary, ENA and EFA allow greater network performance through accelerated networking drivers optimized for supported EC2 instance types.

**28.	Explain the difference between public, private, and Elastic IP addresses.**

**29.	How can you create a custom AMI from a running EC2 instance?
**Here are the steps to create a custom AMI (Amazon Machine Image) from an existing EC2 instance:

1. Stop the source EC2 instance if it needs to be in a clean state for the AMI.

2. Go to the EC2 Dashboard, right click the instance and select "Create Image".

3. Provide a unique name and description for the AMI. You can also add tags.

4. Choose the root volume to create the AMI from. For EBS-backed instances, this is the main volume.

5. Enable "No Reboot" option if the instance can stay running during AMI creation. Otherwise, instance will reboot.

6. Click "Create Image" and the AMI will start getting created.

7. The AMI creation process will detach any secondary EBS volumes to create snapshots of them.

8. Once completed, the new AMI will appear in the "AMIs" section ready to launch new custom instances.

9. When launching instances from custom AMI, select the appropriate architecture, root device settings and VPC/subnet.

So in summary, stopping the instance if needed, creating an image of the root volume and capturing secondary volume snapshots produces a reusable custom AMI for launching customized EC2 instances.


**30.	What is the purpose of an Elastic Network Interface (ENI) in EC2?**
An Elastic Network Interface (ENI) is a logical networking component in EC2 that represents a virtual network card. Here are some key purposes:

- Provides a private IPv4 address and one or more public IPv4 addresses for an instance.

- Can create ENI independently and attach/detach from instances as needed.

- Allows preserving IP addresses for moving instances across subnets.

- Enable binding multiple interfaces to an instance for segmented subnets/network tiers. 

- Can attach ENI to an instance in one AZ and later move to instance in another AZ.

- Facilitates use of multiple private IPs per instance in a VPC.

- Supports creation of dual-homed instances with connectivity to different subnets.

- Can associate security groups with an ENI independent of the instance it is attached to.

- Useful for creating management network interfaces constrained by security groups.

- Allows moving secondary interfaces between instances for failover scenarios.

- Integrates with load balancers for automatic registration with Elastic IPs.

So in summary, ENIs provide advanced networking capabilities like movable IPs, multiple interfaces, and subnet portability for EC2 instances.

**31.	How does EC2 security groups differ from network ACLs?**
EC2 security groups and network ACLs have some key differences:

- Security groups control inbound and outbound traffic at the instance level. Network ACLs control traffic in and out of subnets.

- Security group rules allow instances to talk to each other within the same group. Network ACLs are stateless and block all traffic by default.

- Security groups are attached to EC2 instances or ENIs. Network ACLs are attached at the subnet level. 

- Security groups support allow rules only. Network ACLs support allow and deny rules.

- Security groups evaluate all rules before deciding to allow traffic. Network ACLs process rules in order based on rule number.

- Security groups are stateful - return traffic is automatically allowed regardless of rules. Network ACLs are stateless and need explicit allow rules for return traffic. 

- Security groups can't block IP addresses on other security groups with allow rules. Network ACLs can block entire security groups.

- Security groups are a CISCO ACL-style firewall applied at instance level. Network ACLs are an AWS NACL-style firewall applied at the subnet level.

So in summary, security groups provide instance level traffic filtering, while network ACLs offer subnet level filtering to add an extra layer of security if needed.

**32.	Explain the difference between horizontal and vertical scaling in EC2.**
Horizontal and vertical scaling are two strategies to scale compute resources in EC2:

Horizontal scaling:

- Involves increasing the number of EC2 instances to handle increased load on an application.

- Achieved by adding smaller/commodity instance types for a scale-out approach.

- Automatically done by Auto Scaling groups based on demand.

- A load balancer distributes traffic across the instances.

- Stateless applications that can run on multiple smaller instances are suitable.

- Cost-effective and provides high availability by redundancy.

- Easy to administer by treating machines as identical units.


Vertical scaling: 

- Involves increasing the compute capacity by using larger/optimized instance types.

- Done by migrating to a larger instance type or family, like t2.micro to m4.large.

- Provides ability to handle increased load on a single instance.

- Ideal for stateful apps like databases which run on a single node.

- Administrative overhead of managing larger machines.

- Limited availability since runs on a single instance.

- More expensive than horizontally scaling out with smaller instances.

So in essence, horizontal scaling scales out by adding instances while vertical scales up with larger instance types. The approach depends on the architecture and needs of the application.


33.	How can you attach and detach EBS volumes from EC2 instances?
Here are the steps to attach and detach EBS volumes from EC2 instances:

To attach a volume:

- Create and provision a new EBS volume in the same AZ as the EC2 instance.

- Stop the EC2 instance before attaching the volume (for Linux and some Windows instances). 

- In the EC2 console, right click on the instance, choose Attach/Detach Volumes and select the EBS volume to attach.

- Specify the device name to expose the volume as (e.g. /dev/sdf).

- Restart the EC2 instance after attaching the volume for it to be recognized.

- Connect to the instance and mount the volume as a filesystem to start using it.


To detach a volume:

- Stop the EC2 instance if necessary before detaching.

- In the EC2 console, right click on the instance and select Detach Volume.

- Select the EBS volume to detach and confirm.

- The volume will detach and you can attach it to another instance if needed.

So in summary, stopping the instance, attaching the volume at the OS device level, and restarting allows safe attachment and detachment of EBS volumes on EC2 instances.

34.	What is the purpose of the EC2 instance metadata service?

The EC2 instance metadata service provides information about a running EC2 instance that can be used to configure or manage the instance.

Key uses of the instance metadata service:

- Allows instances to "learn about themselves" without manual configuration.

- Provides data such as instance ID, host name, SSH keys, security groups, block device mappings etc.

- Can access by querying http://169.254.169.254/ from within the instance.

- Allows setting custom key-value pairs for own application use cases.

- Useful for fetching AWS credentials for accessing other services from the instance.

- Helps bootstrap instances by providing configuration data upon startup.

- Enables workflow tools like CloudFormation to inject initial configuration dynamically.  

- Allows on-the-fly customization of instances without manual updates.

- Provides dynamic data and configuration not available at AMI build time. 

- Can access without authentication within the instance to simplify code.

So in essence, the EC2 instance metadata service offers a simple and automated way to provide information to configure and manage the instance as it runs.

35.	How can you enable detailed monitoring for EC2 instances?
There are two ways to enable detailed monitoring for Amazon EC2 instances:

1. Using the AWS Console:

- Select the EC2 instance in the console and go to the "Monitoring" tab
- Click on "Enable Detailed Monitoring"
- This will enable 1-minute frequency metrics collection via CloudWatch

2. Using the AWS CLI:

- Get the instance ID of the EC2 instance  
- Use the monitor-instances command:

```
aws ec2 monitor-instances --instance-ids i-01234567890abcdef
```

- This will return a response when monitoring state change completes

Things to note:

- By default, EC2 metrics are collected at 5-minute intervals
- Detailed monitoring provides 1-minute metrics needed for autoscaling
- It is recommended for production instances 
- An additional CloudWatch charge applies for detailed monitoring
- Can be enabled/disabled at launch time or for existing instances

So in summary, detailed EC2 monitoring provides granular 1-minute metrics via the console, CLI or at launch time configurations.

36.	Explain the difference between the EC2-Classic platform and EC2-VPC.

The key differences between EC2-Classic and EC2-VPC platforms are:

EC2-Classic: 

- Original release of EC2 that provides access to EC2 instances within a single flat network shared by all customers.

- Uses public IPv4 addresses and optional Elastic IPs. No private IP allocation.

- Predefined IP address ranges assigned to accounts by AWS.

- Provides automatic DNS hostnames.

- Security group controls port access. No subnet or network ACL control.

- Limited network customization options.


EC2-VPC:

- Allows creating a private virtual network within AWS cloud and controlling the network topology.

- Private IPv4 for internal IP scheme with public IPv4 access via IGW. 

- Customizable IP CIDR ranges for subnets, ability to create subnets.

- Route tables control network traffic routing within VPC.

- Network ACLs provide stateless subnet filtering. 

- More isolation, security controls, and management compared to EC2-Classic.

- Required for leveraging many AWS services and features.

- Additional components like VPC endpoints, peering connections make possible complex networks.

So in essence, EC2-Classic provides simple network with less control while EC2-VPC enables creating private, isolated networks with granular topology control.

37.	How can you troubleshoot high CPU utilization on an EC2 instance?

Here are some ways to troubleshoot and diagnose high CPU utilization on an EC2 instance:

- Check processes and services using the most CPU via top/htop command. Identify any anomalies.

- Monitor CPU usage over time using CloudWatch metrics to understand usage patterns.

- Enable detailed CloudWatch monitoring for 1-minute CPU metrics if needed for correlation.

- Analyze application logs for errors, stack traces pointing to potential issues.

- Profile CPU usage for processes using utilities like ps, top, perf. 

- Use tools like gdb, strace for processes using high CPU to understand root cause.

- Compare running processes to a known good baseline to detect new or irregular processes.

- Correlate CPU spikes with other activities like batch jobs, backups, high traffic etc.

- If high usage is from a valid process, consider upgrading to a larger instance type or optimizing application.

- Check for and remove unwanted services not being used by the application.

- Verify instance is sized correctly for workload and increase if it is constrained for CPU.

- Check for configuration issues like incorrect threading model or missing optimizations.

- Disable unneeded visual features of OS like GUI if just being used for backend processing.

So in summary, continuously profile processes and services causing high CPU, correlate with application logs and metrics to pinpoint root cause, optimize software configuration, upgrade instance if necessary.

38.	What are EC2 instance types optimized for?

AWS offers a wide variety of EC2 instance types optimized for different use cases:

- General purpose: Balance of compute, memory and networking for web servers, code repositories etc. (T2, M5)

- Compute optimized: High performance for scientific modeling, batch processing, video encoding etc. (C5, C6g)

- Memory optimized: Fast performance for high memory needs like databases, in-memory caches (R5, X1)

- Storage optimized: High, low-latency IOPS for large databases, distributed file systems (I3, D2) 

- Accelerated computing: Hardware GPUs for graphics, ML, scientific applications (P3, G4) 

- Burstable: Burst to full CPU when needed for low cost websites, dev (T2, T3)

- Bare metal: Non-virtualized access to underlying hardware (m5dn, r5b)

- Arm-based: Cost-optimized Graviton2 processors for scale-out workloads (M6g, C6g)

- Infrequent access: Low cost option for workloads not needing continuous compute (T2, M5)

Some other capabilities:

- Multi-GPU instance types for machine learning training and inference

- FPGA programming for genomics, financial computing 

- AMD EPYC based instances for high core count needs

So in summary, EC2 provides a spectrum of diverse instance families, sizes and features to match a wide variety of workload requirements and use cases.

39.	How does EC2 Spot Instances work and what are their use cases?

EC2 Spot instances allow using spare EC2 capacity at steep discounts compared to On-Demand prices. Here's an overview:

- Spot instances utilize surplus EC2 capacity that would otherwise go unused.

- You bid a maximum price and get the instance as long as spot price remains below bid. 

- If spot price increases above your bid, instance is terminated with 2 minute notification.

- Useful for workloads that are fault-tolerant like batch jobs, Big Data analysis, image processing etc.

- Significant cost savings - often 80-90% lower than On-Demand. Savings increase with flexibility.

- Spot blocks allow locking in a price for a fixed duration (1-6 hours) without interruptions.

- Request Spot via CLI/SDK by specifying bid price, volume sizes, VPC settings etc.

- Spot fleets allow launching a fleet of Spot+On-Demand instances to meet target capacity with cost optimization.

- Integrates with Auto Scaling groups, EMR clusters and other AWS services.

- Well suited for scaling up capacity for periodic workloads in a cost-effective way.

So in summary, Spot instances apply unused EC2 capacity for batch, distributed and interruptible workloads at a fraction of the On-Demand cost.

40.	Explain the concept of Elastic GPUs in EC2 instances.

Elastic GPUs allow attaching GPU accelerators to your EC2 instances to run graphics intensive applications like 3D visualizations, machine learning, video processing etc. Here's an overview:

- Elastic GPUs provide GPU hardware like NVIDIA Tesla GPUs as an attachable resource to EC2 instances.

- Allows right-sizing the GPU capacity independent of the instance specification.

- GPUs can be quickly attached or detached from instances in minutes.

- Available as either Elastic GPUs (shared GPU) or Elastic Inference Accelerators (dedicated GPU).

- Support for both Linux and Windows instances. NVIDIA drivers required.

- Useful for batch processing tasks that can leverage massive parallelization on GPUs.

- Enables running deep learning models and training on frameworks like TensorFlow, PyTorch etc. 

- Reduces the cost of GPU clusters while providing flexibility to scale up and down.

- Pay only for the hours during which the GPU is attached to an active instance. 

- Can run 100% GPU based workloads without paying for idle EC2 capacity. 

So in summary, Elastic GPUs provide cost-efficient GPU acceleration, on-demand, by abstracting the GPU hardware from the EC2 instance life cycle.

41.	How can you limit access to EC2 instances based on IP addresses?

There are a couple of options to limit access to EC2 instances based on IP addresses:

1. Security Groups

- Configure inbound rules to allow traffic only from specific IP addresses.

- Specify individual IPs or CIDR blocks.

- Allows granting access to other security groups.

- Applies at the instance level.


2. Network Access Control Lists (ACLs) 

- Stateless ACL rules can allow/deny IP ranges for subnets.

- Whitelist ingress and egress source IPs. 

- Overrides more permissive security group rules.

- Applies at the subnet level so impacts all instances in subnet.


3. Custom iptables rules (Linux) 

- Set Linux iptables policies to drop or reject by default.

- Add custom ACCEPT rules only for known IPs.

- Provides very granular filtering beyond security groups.


4. External facing load balancer

- Restrict public IP access at the load balancer level.

- Allow only approved public IP ranges to connect to load balancer and instances behind it.

So in summary, Security Groups, NACLs, iptables and load balancers can restrict access to EC2 instances based on IP addresses for additional security.


42.	What is the difference between an on-demand and a reserved instance?

The key differences between On-Demand and Reserved EC2 instances are:

On-Demand instances:

- Pay for compute capacity per hour without any upfront commitments.

- No long term contracts or reservations. 

- Suitable for short term, spiky, unpredictable workloads.

- Highest per hour cost but no unused capacity charges.

- No need for planning. Use and pay only for what you consume.

Reserved Instances:

- Provide a significant discount (up to 75%) compared to On-Demand pricing.

- Reserve capacity for 1 or 3 year terms with upfront payment.

- Ensure reserved capacity is always available during term.

- Ideal for steady-state production workloads to lower costs. 

- Require planning and analysis to size reservations and term.

- Loss of payment if reservations are underutilized.

- Can switch from On-Demand to Reserved at any time.

So in summary, On-Demand provides short term flexibility while Reserved offers long term cost savings at the expense of upfront commitment. The optimal approach depends on workload patterns.


43.	How can you move an EC2 instance from one subnet to another?
There are a couple options to move an existing EC2 instance from one subnet to another in the same VPC:

1. Stop the instance, detach and reattach it to a new subnet:

- Stop the EC2 instance
- Detach the network interface from the instance
- Attach it to the new target subnet
- Restart the instance - it will restart in the new subnet

2. Create an AMI from the instance, launch it in the new subnet:

- Stop the instance if needed
- Create an AMI from the instance 
- Launch a new instance from the AMI in the required subnet
- Migrate elastic IPs, data etc. from old instance
- Terminate the old instance

Things to note:

- Instance will retain same private IP if moved between subnets in same AZ
- A new IP will be assigned if subnets are in different AZs
- Moving between subnets may require updating security groups, NACLs etc.
- Preferred method is to use AMIs to prevent downtime

So in essence, stopping and moving network interfaces or launching from AMIs allows shifting EC2 instances across subnets.

44.	Explain the concept of an instance profile in EC2.

An EC2 instance profile is an entity that allows EC2 instances to access AWS services securely without using access keys. Here's an overview:

- Instance profiles contain IAM roles which define the privileges the EC2 instance will have.

- The IAM role's temporary security credentials are made available to the EC2 instance. 

- Any applications running on the instance can leverage these credentials for accessing AWS resources like S3, DynamoDB, SQS etc.

- IAM roles can be added or removed from an instance profile to enable or revoke access dynamically.

- Credentials are automatically rotated ensuring secure access.

- No need to distribute or embed long term keys within EC2 instances.

- Credentials injected into instances via instance metadata service.

- No additional configuration needed for apps on instance to leverage credentials.

- Fine grained permissions control with IAM policies to restrict access only to approved resources. 

- Allows defining conditions like allowing access only from specific IP, VPC etc.

So in summary, instance profiles simplify securely accessing AWS services from EC2 instances without managing credentials on the instance itself.

45.	How can you migrate an EC2 instance to a different region?
Here are the typical steps to migrate an EC2 instance to a different region:

1. Take a snapshot of the instance's EBS root volume and any attached EBS data volumes. Snapshots are regional resources.

2. Create an AMI (Amazon Machine Image) from the snapshots in the target region.

3. Launch an EC2 instance from the copied AMI in the new target region.

4. Copy any additional data/files from old instance using rsync, scp etc.

5. Update DNS records and traffic rerouting rules to direct traffic to new instance.

6. Test the new instance and applications thoroughly.

7. Once migration is successful, terminate the original instance in old region if no longer needed.

Some tips:

- Use Elastic IPs to quickly remap traffic to new instance in case of issues.

- Perform multiple dry runs to test process before actual cut over.

- Pre-copy large volumes of data using Snowball to minimize downtime.

- Use Systems Manager to copy over configurations, environment settings.

So in summary, migrating across regions involves snapshotting disks, launching from copied AMI and synchronizing data in the new region followed by traffic cutover.


Here are the steps to migrate an EC2 instance to another region using AWS CLI:

1. Stop the EC2 instance in the source region if it needs to be in a clean state:

```bash
aws ec2 stop-instances --instance-ids i-01234567890abcd 
```

2. Create a snapshot of the root EBS volume:

```bash
aws ec2 create-snapshot --volume-id vol-01234567890abcd --description "Root volume snapshot"
```

3. Create AMI from the snapshot in destination region:

```bash 
aws ec2 copy-snapshot --source-region us-east-1 --source-snapshot-id snap-01234567890abcd --region us-west-2
```

4. Launch an EC2 instance from the copied AMI: 

```bash
aws ec2 run-instances --image-id ami-01234567890abcd --count 1 --instance-type t2.micro --key-name mykey --region us-west-2
``` 

5. Optionally copy data from old instance using scp, rsync etc.

6. Update DNS and traffic management to direct to new instance 

7. Terminate the old EC2 instance:

```bash
aws ec2 terminate-instances --instance-ids i-01234567890abcd --region us-east-1
```

So in summary, AWS CLI provides a programmatic way to migrate an EC2 instance across regions using snapshots, AMIs and standard instance provisioning commands.

46.	What is the difference between a public and a private subnet in EC2?

The key differences between public and private subnets in EC2 are:

Public Subnet:

- Resources in public subnets are assigned public IPv4 addresses.

- Allows direct outbound internet access via internet gateway.

- Used for publicly accessible resources like web servers.

- Security groups and NACLs provide security.

- Bastion hosts needed to SSH into instances.


Private Subnet: 

- Resources assigned private IPv4 addresses only. No direct internet access.

- Allows outbound internet access via NAT gateway or proxy only.

- Used for backend servers like databases. 

- End users cannot directly access resources in private subnet over internet.

- VPC peering or VPN can connect to on-premise data centers.

- Supports additional layers of security relative to public subnets.

- Can access internet by adding public subnet with NAT gateway.

So in summary, public subnets front the public traffic while private subnets host sensitive assets with additional network security protections provided by the VPC constructs.

47.	How can you connect to an EC2 instance using SSH?


48.	Explain the difference between the root volume and other EBS volumes.
The main differences between the root EBS volume and other EBS volumes attached to an EC2 instance are:

- Root volume is the boot volume containing the operating system and installed applications. Other volumes provide additional storage capacity.

- Only one root volume can be attached to an instance while multiple extra volumes can be attached.

- Root volume gets deleted automatically when instance is terminated. Extra volumes persist and can be detached. 

- Root volume size determines AMI type - larger volumes can't be used for smaller AMI types. Extra volumes can be different sizes and types.

- By default, root volume can't be detached from a running instance while extra volumes can be detached and reattached. 

- Root volume is labeled as /dev/sda1 in Linux and C: drive in Windows. Extra volumes get labeled as /dev/sd[b-z] and retain labels after detachments.

- Encryption, IOPS allocation, volume type can be specified separately for additional EBS volumes.

- Deleting and creating new root volumes requires creating new AMIs. Extra volumes can directly be deleted and created.

So in summary, the root volume is the boot drive while other EBS volumes provide persistent and independent storage expansion for instances.


49.	How can you transfer files to and from an EC2 instance?

Here are some common ways to transfer files to and from EC2 instances:

- SSH - Use SCP or SFTP to transfer files over SSH. Easy for small files and text configuration files.

- FTP Server - Run an FTP server on the instance to allow file transfers over FTP.

- S3 Sync - Sync files and folders with S3 using AWS CLI. Useful for backups and large file transfers.

- AWS Transfer for SFTP - Managed SFTP service for seamlessly transferring files.

- EBS Volumes - Attach EBS volumes from another instance to copy all files and data.

- AWS DataSync - Replicate large datasets from on-premises to EC2 instances.  

- Database Migration Service - Migrate database files and data to RDS or EC2 databases.

- Snowball/Snowmobile - Transfer terabytes/petabytes of data through portable AWS storage devices. 

- AWS AppSync - Sync and transfer application files and assets.

- Direct Link/VPN - Setup a dedicated private connection to enable high throughput transfers.

So in summary, several approaches like SSH, shared volumes, AWS data transfer services, network connectivity options exist to meet different file transfer size, frequency and performance requirements.

50.	What is the difference between a dedicated and a default tenancy in EC2?
The key differences between Dedicated and Default tenancy in EC2 are:

Dedicated Tenancy:

- Instances run on single-tenant hardware fully dedicated to one customer.

- No sharing of underlying hardware with instances from other accounts.

- Useful for regulatory compliance or if need full control over hardware.

- Significantly more expensive than default tenancy.

- Requires contacting AWS sales team to enable.

Default Tenancy:

- Instances run on shared hardware that may be used by instances from other customers.

- AWS isolates customers from each other through proper logical separation mechanisms.

- Enabled by default for all accounts and requires no special permissions. 

- Costs significantly lower compared to dedicated tenancy.

- Well suited for most general workloads in the cloud.

- Dedicated host can be used for some physical isolation with default tenancy.

So in summary, dedicated tenancy provides full physical isolation while default allows better sharing resulting in lower costs suitable for most workloads.

51.	How can you monitor network traffic on an EC2 instance?

Here are some ways to monitor network traffic on EC2 instances:

- CloudWatch metrics - Monitor bytes/packets in/out, flows, ACL metrics etc. Set alarms on metrics.

- CloudWatch Logs - Stream and analyze VPC Flow Logs to detect anomalies.

- AWS VPC Traffic Mirroring - Mirror instance traffic to a traffic mirror target for inspection.

- Native OS tools - Use netstat, iftop, ntopng on Linux or perfmon on Windows.

- Network analysis tools - Install software like Wireshark for deep packet inspection.

- AWS Direct Connect + Third party tools - Mirror instance traffic to an appliance for analysis. 

- AWS Marketplace network tools - Leverage AMI appliances like Riverbed Cascade for network visibility.

- CloudWatch Embedded Metric Format - Push custom metrics from clients for network usage.  

- Traceroute - Track packet routes and metrics to analyze performance. 

- Security Groups and NACLs - Only allow approved ports and IP ranges based on application needs.

So in summary, a combination of AWS managed services like CloudWatch, VPC Flow Logs combined with native OS, external tools and network security provides comprehensive monitoring and visibility into EC2 network traffic.

52.	Explain the concept of Elastic IP addresses in EC2.

Elastic IP addresses in EC2 provide static, public IPv4 addresses that can dynamically map to instances:  

- An Elastic IP can be allocated to your AWS account.

- It remains allocated until you choose to release it.

- An Elastic IP can be assigned to any EC2 instance in a given region. 

- It can remap between instances to mask failures or migrations.

- You can have multiple Elastic IPs allocated but only one associated per instance.

- Attaching an Elastic IP replaces any existing public IP on the instance.

- Useful for dynamically remapping public endpoints to instances.

- Helps mask changes in underlying infrastructure from the end users.

- Ensures a fixed public IP for accessing instances after stops/starts.

- No charge for Elastic IPs if attached to a running instance or VPC endpoint.

- Small hourly fee if left unattached or attached to a stopped instance.

So in summary, Elastic IP addresses allow static public IP mapping to dynamically changing EC2 instances to simplify management and connectivity.

53.	How can you enable and disable public IP addresses for EC2 instances?
There are a couple ways to enable or disable public IP addresses for EC2 instances:

- During Launch:

When launching a new instance, there is a setting to "Auto-assign Public IP". Set this to Enable to assign a public IP, Disable to not assign a public IP.

- Using Elastic IPs:

Allocate and assign an Elastic IP to an instance to give it a public IP. Disassociate the Elastic IP to remove public IP access.

- Modify Network Interface:  

For an existing instance - navigate to the Network Interfaces section, select the interface, and toggle the setting "Auto-assign Public IP" to enable/disable public IP.

- Create Public/Private Subnets:

Launch instances in a Public Subnet to assign public IPs automatically. Launch in a Private subnet to only get a private IP by default.

- Security Groups: 

Restrict inbound rules to block public internet access to the instance while allowing private VPC access.

So in summary, the public IP assignment can be controlled during launch and post-launch by subnet type, network interface configuration, Elastic IPs and security group rules.

54.	What is the purpose of the EC2 Systems Manager?
AWS Systems Manager (SSM) provides capabilities to manage EC2 and on-premises instances:

- Allows viewing operational data about instances and fleets centrally.

- Provides runtime insights into system status, application performance, resource utilization.

- Enables updating, managing and configuring instances remotely.

- Automates common maintenance and deployment tasks across instances.

- Facilitates compliance patching and configuration management.

- Allows remotely running commands and scripts on instances. 

- Integrates with parameter store for access to secrets and config.

- Provides Session Manager for shell access without SSH or bastion hosts.

- Enables creating logical groups of instances and perform operations on groups.

- Simplifies capturing instance configurations and auditing changes. 

- Tracks resource relationships and visualizes topology.

- Integrates with AWS services like CloudWatch, Lambda, Step Functions for automation.

So in summary, SSM provides tooling and APIs to centrally monitor, manage, configure and update a fleet of EC2 and on-premises instances throughout their lifecycle.


55.	How can you share an AMI with other AWS accounts?

There are a couple of ways to share AMIs (Amazon Machine Images) across AWS accounts:

1. Make the AMI public - In the AMI console, edit the AMI properties and set "Public" to "Yes". This will allow all AWS accounts to launch instances from the AMI.

2. Share AMI via launch permissions - Add the target account IDs under "Launch permissions" and only those accounts will be able to use the AMI.

3. Copy AMI to target account - The owner account can copy the AMI to another account by sharing the AMI ID. The target account can then copy the shared AMI to their region.

4. Make AMI owned by another account - While creating the AMI, select the target account ID under "Owned by" instead of the current account. This transfers ownership of that AMI to the target account. 

5. Use AWS Resource Access Manager (RAM) - Share AMIs between accounts within or across regions using RAM sharing.

The choice depends on the degree of access control required and the number of accounts the AMI needs to be shared with. For selective access, launch permissions or RAM sharing is best. For public AMIs, making AMI fully public is optimal.

56.	Explain the difference between instance metadata and user data.
The key differences between EC2 instance metadata and user data are:

Instance metadata:

- Data about the EC2 instance that applications on the instance can access.

- Includes info like public hostname, instance ID, security groups etc.

- Accessible from within the instance at a special endpoint http://169.254.169.254.

- Allows setting custom key-value pairs for own configuration needs.

- Provides dynamic information not available at launch time.


User data:

- Custom data that is supplied during instance launch.

- Used to perform common automated configuration tasks and bootstrapping operations.

- Has a size limit of 16 KB (plain text) or 64 KB (base64 encoded).

- Executed only during the boot process. Metadata is always available.

- Allows bootstrapping instances with files, configs etc. needed.

- Useful for one-time configuration or installation of software at launch.  

- Retrievable via instance metadata but cannot otherwise modify metadata.

So in summary, metadata provides info about the instance while user data executes custom logic during boot for initialization and configuration.

57.	How can you create an EC2 instance using AWS CLI?

Here is an example to launch an EC2 instance using the AWS CLI:

1. Create a key pair:

```bash
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
```

2. Create a security group: 

```bash
aws ec2 create-security-group --group-name MySecurityGroup --description "Security group for my instances"
```

3. Add ingress rules to allow SSH and HTTP:

```bash
aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --port 22 --protocol tcp

aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --port 80 --protocol tcp  
```

4. Launch an EC2 instance:

```bash
aws ec2 run-instances --image-id ami-0abcdef1234567890 --count 1 --instance-type t2.micro --key-name MyKeyPair --security-groups MySecurityGroup
```

5. Get public IP of instance:

```bash 
aws ec2 describe-instances --instance-ids i-01234567890abcdef --query 'Reservations[*].Instances[*].PublicIpAddress'
```

This will launch an EC2 instance in a few minutes using the AWS CLI without needing the web console.

58.	What are the limitations of EC2 instances?

Some key limitations and constraints to be aware of with EC2 instances are:

- vCPU limits - Default soft limit of 96 vCPUs per region which can be increased via request.

- Instance limits - Default limit of 20 On-demand instances per region which can be increased.

- IP addresses - Limited private IPs per VPC based on CIDR range, public IPs have to be requested.

- Storage - Boot volume limits based on AMI, total volumes and snapshots per region are constrained.

- Instance metadata - Size limit of 16 KB per request, 40 KB total.

- User data - Limited to 16 KB for plain text, 64 KB for base64 encoded data.

- Security groups - Limited to 500 rules per security group, applies per NIC.

- Network interfaces - On-demand limit of 350 interfaces per region.

- EBS optimized instances - Only available for certain instance types and carries a small additional charge. 

- Placement groups - Maximum of 7 running instances for clustered placement group. 

- Pricing - On-demand option is the most expensive compared to Spot, Reserved.

- Boot time - Instance restart/stop/start takes a few minutes unlike bare metal servers.

So in essence, limits exist on almost all aspects of EC2 instances related to IPs, storage, network, metadata size, number of instances etc. These apply on a per-region basis.


59.	How can you attach an IAM role to an EC2 instance?

There are a couple of ways to attach an IAM role to an existing EC2 instance:

1. Using the AWS Management Console:

- Select the EC2 instance and go to the "IAM Role" tab in the details pane.
- Click "Attach/Replace IAM Role" and select the IAM role to attach.
- The EC2 instance will get the permissions defined in the role.

2. Using AWS CLI:

- Retrieve the instance profile of the EC2 instance:

```
aws ec2 describe-instances --instance-ids i-01234567890abcd
```

- Get the IAM role ARN to attach 

- Use the associate-iam-instance-profile command:

```
aws ec2 associate-iam-instance-profile --instance-id i-01234567890abcd --iam-instance-profile Name="RoleName"
```

- The IAM role will be attached to the instance profile.

So in summary, the console provides a simple way to attach IAM roles while the AWS CLI can automate role attachment across instances for permissions management.

60.	Explain the concept of EC2 instance hibernation.
EC2 instance hibernation allows stopping and restarting instances while preserving their in-memory state. Here is an overview:

- Hibernation saves the contents from the instance memory (RAM) to your EBS root volume. 

- The EBS root volume must be encrypted to enable hibernation.

- When an instance is started after hibernation, data is reloaded from the volume and state is restored.

- Much faster boot time compared to a full cold boot of the OS.

- Instance RAM size must be less than 150 GB for hibernation.

- Data is encrypted at rest on the EBS volume and decrypted when starting.

- Ideal for long-running processing that can resume from stored state.

- Use cases like analytics, scientific modeling, ML training etc can leverage hibernation.
  
- Instance is billed only for EBS storage while hibernated, unlike stopped instances.

- Available for Windows, Amazon Linux 2, and Ubuntu AMIs. 

So in summary, hibernation allows cost-effective preservation of in-memory state for certain workloads that need to resume from stored runtime state.

61.	How can you schedule automated start and stop of EC2 instances?

There are a couple options to schedule automatic start and stop of EC2 instances:

1. Use EC2 Scheduled Instances

- Specify a fixed recurring schedule for starting and stopping instances. 

- Schedules like office hours or weekends can be set.

- Instances will automatically start or stop per the defined schedule.

2. Configure Auto Scaling Scheduled Actions

- Auto Scaling allows defining scheduled actions. 

- Scale-out and scale-in policies can be set by time of day/week.

- Instead of scaling instance count, set min=max=0 to stop and min=max=1 to start.

3. Use AWS Lambda functions

- Trigger Lambda on a schedule using CloudWatch Events.

- Lambda can call EC2 control plane APIs to stop, start or terminate instances.

4. Configure AWS Systems Manager Automation

- Define Automation documents with EC2 control actions.

- Use Maintenance Windows to trigger automation runs on schedule.

So in summary, Scheduled Instances, Auto Scaling, Lambda and Systems Manager provide ways to automatically schedule EC2 instance start/stop.


Here is an example to schedule starting and stopping of EC2 instances using AWS CLI:

1. Create a Lambda function that can start/stop EC2 instances:

```
aws lambda create-function --function-name ManageEC2 --runtime python3.8 --zip-file fileb://function.zip --role lambda-role 
```

2. Create a CloudWatch rule to trigger the Lambda daily:

```
aws events put-rule --name DailyLambda --schedule-expression 'cron(0 8 ? * MON-FRI *)'
```  

```
aws events put-targets --rule DailyLambda --targets Id=1,Arn=lambda-arn
```

3. The Lambda code to stop instances at 6 PM and start at 8 AM on weekdays:

```python
import boto3

ec2 = boto3.client('ec2')

def lambda_handler(event, context):

  # Get list of instances
  instances = ec2.describe_instances()['Reservations']

  if event['time'] == 'stop':
    ec2.stop_instances(InstanceIds=get_instance_ids(instances))
  
  if event['time'] == 'start':  
    ec2.start_instances(InstanceIds=get_instance_ids(instances))

def get_instance_ids(reservations):
  return [instance['InstanceId'] for reservation in reservations for instance in reservation['Instances']]
```

So this automates scheduled stop and start of EC2 instances using Lambda and CloudWatch events.

62.	What is the purpose of an EC2 instance profile?

The main purposes of an EC2 instance profile are:

- It contains the IAM role to attach to the EC2 instance.

- The IAM role defines the permissions that the EC2 instance will have.

- The temporary AWS credentials associated with the IAM role get automatically provisioned on the instance.

- Any applications running on the instance can use these credentials to access other AWS services like S3, DynamoDB etc. 

- Removes need to manage permanent access keys on each EC2 instance.

- Credentials are automatically rotated for security.

- Permissions can be controlled by IAM policies to restrict what the instance can access.

- Allows setting conditions like IP range, VPC etc to constrain access.

- No further configuration required on instance to leverage credentials.

- Can attach/replace IAM roles on an instance without reboot.

- Credentials are delivered securely via instance metadata service.

So in essence, instance profiles simplify provisioning temporary credentials on EC2 instances to securely access other AWS services without permanent credentials on each instance.


63.	How can you monitor disk performance on an EC2 instance?

Here are some options to monitor disk performance on EC2 instances:

- CloudWatch disk metrics - Reports disk reads/writes ops, latency, queue depth to detect bottlenecks.

- CloudWatch Logs - Stream and parse disk performance logs from instance.

- Native OS tools - iostat and sar on Linux, Performance Monitor on Windows provide disk IOPS, latency, utilization. 

- 3rd party tools - Install tools like collectd, New Relic agent to collect disk metrics.

- Instance store metrics - Monitor instance store volumes separately from EBS with CLI tools.

- EBS CloudWatch metrics - Granular volume-level statistics for EBS volumes to isolate issues.

- EBS Volume status checks - Identify impaired volumes impacting disk performance.

- Tracing with X-Ray - Trace disk operations to uncover slow code paths.

- Benchmark tools - Run tools like fio, dd to generate disk load and test capability.

- Tune disk - Adjust disk striping, partitioning, OS buffers based on usage patterns.

- Scale instance/disk - Use EBS-optimized or storage optimized instances, provisioned IOPS EBS.

So in summary, a combination of AWS CloudWatch metrics, EBS volume metrics, OS/3rd party tools and load testing can provide deep visibility into EC2 disk performance.

64.	Explain the concept of Elastic Fabric Adapter (EFA) in EC2.
Elastic Fabric Adapter (EFA) is a network interface for EC2 instances to provide high bandwidth, low latency network performance for inter-instance communication. Here is an overview:

- EFA enables OS-bypass capabilities for distributed computing applications.

- Provides very high packet per second (PPS) performance and low inter-instance latencies.

- Implements Scalable Reliable Datagram Protocol (SRDP) for MPI traffic.

- Supports message passing interface (MPI) based applications and frameworks like Apache Spark, Deep Learning.

- Optimized for tightly-coupled workloads that require frequent synchronization and inter-process communication.

- Uses peer-to-peer elastics NICs to provide congestion controlled transport between instances.

- Reduces jitter, CPU overhead, latency compared to TCP-based sockets.

- Only available for certain EC2 instance families like C5, P3, M5.

- Needs EFA-enabled AMI and EFA driver installation to leverage capabilities. 

- Use cases include High Performance Computing (HPC), Machine Learning, High Frequency Trading etc.

So in summary, EFA enables very high performance networking between EC2 instances to run latency-sensitive distributed computing workloads like HPC and ML model training.

65.	How can you perform live migration of EC2 instances?

There are a couple ways to perform live migration of EC2 instances between hosts:

- Using AWS Outposts - Allows live migrating on-premises servers to AWS Outposts via VMware Cloud on AWS. Live migrate to Outposts and back.

- Pilot Light - Keep a pilot light instance spun up in the target AZ. Replicate data to it, switch over DNS to pilot and terminate old.

- AWS Application Discovery Service - Track instance dependencies, map out topology and orchestrate migrations.

- AWS Server Migration Service (SMS) - SMS can live migrate VMs to AWS from on-prem.

- Storage Migration Service (SMS) - Replicate volumes to new AZ in advance then promote replica.

- Custom Script - Script OS/app synchronization between instances before promoting new instance to production.

- DNS Cutover - Update DNS to direct to new instance IP once synchronization is done.

- Elastic Load Balancing - Register new instance with ELB in new AZ, deregister old instance. 

- Database Replication - Use RDS read replicas or database native replication to migrate data in advance.

Some key considerations around live migration are minimum downtime, managing IP change, storage migration, and maintaining synchronization between instances during cutover.

66.	What is the difference between an EC2 instance and an ECS container?
The main differences between EC2 instances and ECS containers are:

- EC2 instances are virtual machines with dedicated compute resources like CPU, memory, network etc. ECS containers are more lightweight and share the host resources.

- Instances require manually configuring and scaling capacity. Containers abstract away capacity management.

- Instances can run different OSes and software as needed. Containers package up just the app and dependencies.

- Instances are isolated and have individual public IPs/hostnames. Containers are networked together and are addressed by private IPs. 

- Instances are billed for full hour even if not utilized. Containers are billed per second based on usage.

- Instances are provisioned in minutes. Containers start in seconds allowing faster scaling.

- Instances require installing dependencies and apps. Containers carry the image with everything baked in.

- Instances are configured individually. Containers use images allowing consistency. 

- State is ephemeral in containers. Instances leverage EBS volumes for persistence.

So in summary, containers enable lightweight, portable deployment of apps while instances provide persistent storage and isolated control suitable for legacy applications.

67.	How can you perform rolling updates on an Auto Scaling group?

Here are the steps to perform rolling updates on EC2 instances in an Auto Scaling group:

1. Create a new launch configuration with the updated AMI/settings.

2. In the Auto Scaling group, update the launch configuration to point to the new version.

3. Set the "Desired Capacity" and "Minimum Capacity" on the group to the same number. 

4. Set the "Maximum Capacity" to the desired total number of instances during the rollout.

5. The Auto Scaling group will launch new instances with new config and terminate old ones sequentially.

6. Monitor the update and rollback if issues arise.

7. Once rollback is no longer needed, set "Minimum" and "Desired" capacities back to original levels.  

Some tips:

- Validate the new AMI and config independently first.

- Gradually change "Desired Capacity" to control the pace of replacements.

- Use Lifecycle Hooks to perform readiness checks before serving traffic.

- Set health checks on the ELB to route traffic only to healthy instances.

So in summary, a controlled rolling update process leverages Auto Scaling lifecycle management capabilities to incrementally deploy a new AMI or configuration.

Here is an example of how to perform a rolling update of an Auto Scaling group across AZs using AWS CLI:

1. Create a new launch configuration with the new AMI:

```
aws autoscaling create-launch-configuration --launch-configuration-name new-lc --image-id ami-new1234abc --instance-type t2.micro
```

2. Update the Auto Scaling group to use the new launch configuration:

```
aws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name new-lc
```

3. Double the maximum size to allow new instances to start: 

```
aws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --max-size 10
``` 

4. Increment desired capacity to start new instances:

```
aws autoscaling set-desired-capacity --auto-scaling-group-name my-asg --desired-capacity 5 
```

5. Wait for new instances to start, then decrement old ones:

```
aws autoscaling set-desired-capacity --auto-scaling-group-name my-asg --desired-capacity 4
```

6. Repeat steps 4-5 gradually to roll out new instances and terminate old.

7. Clean up by setting desired capacity back to original.

This performs a gradual rolling update of the Auto Scaling group across AZs using AWS CLI.


68.	Explain the concept of instance metadata options in EC2.

The EC2 instance metadata options allow controlling access to instance metadata:

- Instance metadata is data about an instance accessible from within at 169.254.169.254.

- It provides information like public IP, hostname, security groups etc.

- By default, metadata service is available without authentication.

- Metadata options allow setting restrictions on metadata access.

- httpTokens - Require sending header X-aws-ec2-metadata-token to retrieve metadata. This token needs to be retrieved separately first.

- httpEndpoint - Enables a non-public IPv6 endpoint for metadata rather than the default public 169.254.169.254 address.

- httpPutResponseHopLimit - Control number of network hops metadata requests can traverse to prevent access from untrusted networks.

- Enforcing token requirement prevents unauthorized reads of metadata.

- Non-public endpoint restricts metadata requests to within VPC. 

- Lower hop limit prevents requests from flavor-of-the-day exploits.

- Can configure metadata options using AWS CLI or user-data at launch.

- Securing metadata access provides defense-in-depth against certain attack vectors.

So in summary, instance metadata options allow controlling and restricting access to instance metadata to prevent potential security issues.


69.	How can you encrypt EBS volumes attached to an EC2 instance?

Here are the main ways to encrypt EBS volumes attached to EC2 instances:

- Enable encryption when creating new EBS volumes and snapshots. The data will be encrypted at rest using AES-256.

- Create encrypted AMIs and launch encrypted instances - The root EBS volume will be encrypted by default.

- Copy an unencrypted snapshot, selecting the encrypt option. Then volumes restored will be encrypted.

- Create an encrypted snapshot of an unencrypted volume. Subsequent volumes will be encrypted. 

- Leverage third party encryption tools like Bitlocker, dm-crypt, LUKS to encrypt at the OS level.

- Use AWS Key Management Service (KMS) for managing encryption keys.

- Enable encryption by default using a default KMS key for EBS encryption for the account.

- Leverage CloudHSM for FIPS 140-2 compliant key storage and use its keys for EBS encryption.

- Set IAM policies to enforce use of encrypted volumes across organization.

- Encrypted volumes have minimal performance impact but can't be encrypted in-place.

So in summary, enabling encryption at volume creation, copying encrypted snapshots and using KMS facilitates encrypting EBS storage for EC2 compliance and security needs.

Here is an example to encrypt an unencrypted EBS volume attached to an EC2 instance using AWS CLI:

1. Create an EBS snapshot of the unencrypted volume:

```bash
aws ec2 create-snapshot --volume-id vol-123abcd --description "Snapshot of unencrypted volume"
```

2. Create an encrypted copy of the snapshot:

```bash
aws ec2 copy-snapshot --source-snapshot-id snap-abc123 --destination-region us-east-1 --encrypted
```

3. Create an EBS volume from the encrypted snapshot:

```bash 
aws ec2 create-volume --snapshot-id snap-xyz123 --availability-zone us-east-1a --volume-type gp2 --encrypted
```

4. Detach the unencrypted volume from the EC2 instance:

```bash
aws ec2 detach-volume --volume-id vol-123abcd 
```

5. Attach the new encrypted volume to the instance:

```bash
aws ec2 attach-volume --volume-id vol-new456 --instance-id i-01234567890 --device /dev/sdf
```

This process migrates the data to an encrypted volume which can then be attached to the instance, encrypting it in the process using AWS CLI.


70.	What is the significance of user data scripts in EC2 instances?
User data scripts allow EC2 instances to execute custom bootstrap operations during launch. Some key uses of user data scripts are:

- Install and configure prerequisites needed by the application like web servers, agents, utilities.

- Download common dependencies and libraries on first launch.

- Pull configuration files, license keys etc. from sources like S3 or GitHub. 

- Join instances to Active Directory or systems management tools.

- Register with DNS, monitoring and log management systems.

- Run update, patch management to harden and secure instances.

- Perform one-time complex configuration tasks needed before launching apps.

- Help conform instances to organizational standards and policies.

- Allow instances to process temporary bootstrap data needed for initialization.

- Handle dynamic data not available at AMI build time.

- Automate menial instance prep and configuration tasks that are error prone.

- Bootstrapping with user data reduces time to launch applications after provisioning instances.

So in summary, user data scripts allow automating and customizing instance configuration on first boot rather than manual steps after launch.

71.	How can you enable and configure CloudWatch Logs on EC2 instances?

Here are the main steps to enable and configure CloudWatch Logs for EC2 instances:

1. Install the CloudWatch Logs agent on the EC2 instance. It comes pre-installed on Amazon Linux AMIs.

2. Configure the agent by specifying log file paths, log groups, and other options in the config file at /etc/awslogs/awslogs.conf.

3. Set up rotation policies, retention periods, and logging queues in CloudWatch Logs console or using CLI. 

4. Start the CloudWatch Logs agent on instance using:

```
sudo service awslogs start
```

5. View and search logs in CloudWatch Logs console once agent starts pushing logs.

6. To track custom application logs, pipe output to /var/log/cwlogs/application.log which is monitored by default.

7. Install and configure AWSCloudWatchAgent on Windows to push event logs, IIS logs etc.

8. Use the CloudWatch Unified Agent for gathering system-level metrics in addition to logs.

9. Analyze log data further using subscription filters into Lambda, analytics tools, etc.

So in summary, installing the CloudWatch agent and configuring monitored log files and destinations enables aggregating, streaming and analyzing EC2 instance logs centrally.


72.	Explain the concept of EC2 instance family and its importance.

EC2 instance families are groups of instance types optimized for specific use cases. Understanding instance families is important for selecting the right instance type: 

- General Purpose - Balanced ratio of compute, memory, networking resources. Ideal for a diverse range of workloads like web servers, code repositories, small databases etc. Families like M5, T3 etc.

- Compute Optimized - High performance processors ideal for high throughput compute like batch processing, media transcoding, scientific modeling, ML inference etc. Families include C5, C6g. 

- Memory Optimized - Fast performance instances designed for memory intensive workloads like high performance databases, distributed caches, in-memory analytics, scientific applications etc. Example families are R5, X1.

- Storage Optimized - High sequential read/write access to very large data sets on local storage. Ideal for data warehousing, distributed file systems. Families include I3, D2.

- Accelerated Computing - Hardware accelerators like GPUs, FPGAs for workloads like machine learning, graphics rendering, genomics, computational finance etc. Examples are P2, G4.

- Each family is further segmented into instance sizes or types within the family based on increasing compute, memory and storage capabilities.

Knowing the capabilities of the instance family guides selection of the most optimal instance type for a given workload's performance, cost and sizing requirements.

73.	How can you change the instance type of a running EC2 instance?

There are a couple of ways to change the instance type (size) of a running EC2 instance:

1. Stop the instance, change its instance type, and restart it. 

- Stop the instance from the EC2 console or using the CLI.
- Select the stopped instance, go to Actions > Instance Settings > Change Instance Type.
- Specify a new (larger or smaller) instance type.
- Start the instance - it will now have the new instance type.

2. Use Elastic Resize to change the instance type on the fly.

- From the EC2 console, select the running instance and choose Actions > Instance Settings > Change Instance Type. 
- Select Elastic Resize option and pick the new instance type.
- The instance will restart with the new size after a few minutes of outage.

3. Create an AMI from the instance, launch a new instance from the AMI with given instance type. 

- Follow AMI creation process.
- Launch new instance from this AMI with desired size.
- Migrate Elastic IP, data etc. from old instance. 

So in summary, stopping or elastic resize changes the size for existing instance while AMI approach launches new one. The first two have downtime so for zero-downtime, AMI is preferred.

Here is an example to change the instance type of a running EC2 instance using AWS CLI:

1. Stop the instance:

```bash
aws ec2 stop-instances --instance-ids i-01234567890abcd
```

2. Change the instance type attribute:

```bash
aws ec2 modify-instance-attribute --instance-id i-01234567890abcd --instance-type {new_type}
```

3. Start the instance again:

```bash  
aws ec2 start-instances --instance-ids i-01234567890abcd
```

The instance will restart with the new instance type.

For resizing without stopping:

```bash
aws ec2 modify-instance-attribute --instance-id i-01234567890abcd --instance-type {new_type} --no-stop
```

This will perform an elastic resize to change instance type on the fly.

So AWS CLI provides easy commands to change instance size either with stop/start or elastic resize approaches.

74.	What are the different ways to stop and start an EC2 instance?
There are a few different ways to stop and start an existing EC2 instance:

- Using the EC2 console - Select the instance, click Actions > Instance State > Stop/Start.

- Using AWS CLI - Use the 'stop-instances' and 'start-instances' commands with the instance-id as parameter.

- Using an API call - Call the StopInstances and StartInstances API actions to stop and start the instance programmatically. 

- Using an AWS SDK - Call the stop_instances() and start_instances() functions in the EC2 client class.

- Creating an AWS Lambda function - Create a Lambda to stop or terminate instances on trigger.

- Configuring a CloudWatch event - Trigger a stop or start based on a schedule using CloudWatch events.

- Using AWS OpsWorks - Use the stop stack and start stack commands to control instance state.

- From EC2 Instance OS - Run shutdown or reboot command within the OS to initiate stop and start.

- Auto Scaling - Use min/max size of 0/1 in Auto Scaling group to stop and start the instance. 

So in summary, the EC2 console, CLI, APIs, SDKs, Lambda, CloudWatch, OpsWorks and Auto Scaling all allow programmatically stopping and starting EC2 instances on-demand or on a schedule.

Here is an example to stop and start an EC2 instance using AWS CLI:

To stop an instance:

```bash
aws ec2 stop-instances --instance-ids i-1234567890abc
```

To check when the instance has stopped completely:

```bash
aws ec2 describe-instances --instance-ids i-1234567890abc
```

To start the stopped instance:

```bash 
aws ec2 start-instances --instance-ids i-1234567890abc
```

To terminate the instance:

```bash
aws ec2 terminate-instances --instance-ids i-1234567890abc
```

The start, stop and terminate commands can be used together to control the lifecycle of EC2 instances using the AWS CLI.

We can also create bash scripts or Ansible playbooks around these commands to stop, start or terminate groups of instances programmatically.

75.	How can you monitor memory usage on an EC2 instance?
Here are some ways to monitor memory usage on EC2 instances:

- CloudWatch memory metrics - Reports memory utilization, available memory, swap usage. Can set alarms on metrics.

- Native tools - top/htop, free, vmstat on Linux; Task Manager on Windows to view memory use, caching, swap.

- CloudWatch Logs - Stream and parse memory logs using CloudWatch Logs agent.

- 3rd party monitoring tools - New Relic, Datadog, AWS Inspector provide memory monitoring.

- Memory pressure notifications - Monitor memory pressure events using tools like Pressure Stall Information (PSI) on Linux.

- Performance benchmarks - Run memory capacity and leak tests using stress-ng, memtester.

- Tracing memory issues - Enable stack traces on OOM kills, analyse heap dumps to pinpoint leaks.

- Tune kernel parameters - Adjust vm.overcommit_memory, swappiness, OOM settings.

- Right size instance - Use memory optimized instances, provisioned IOPS storage for memory intensive apps.

- Horizontal scaling - Distribute memory load across multiple smaller instances.

- Upgrade instance - For persistent high memory, scale up to a larger instance type.

So in summary, a combination of CloudWatch, in-instance tools, benchmarks and parameters tuning ensures optimal memory performance and monitoring.

76.	Explain the difference between an EC2 instance and an ECS service.
The main differences between an EC2 instance and an ECS service are:

- EC2 (Elastic Compute Cloud) is an Infrastructure as a Service (IaaS) that provides virtual machine instances for computing. ECS (Elastic Container Service) is a container orchestration service that supports Docker containers.

- An EC2 instance is a single virtual machine that you launch and manage. An ECS service runs and manages Docker containers across a cluster of EC2 instances. 

- With EC2 you have full control over the OS, software, updates etc. ECS abstracts away the infrastructure so you just manage containers.

- EC2 instances are billed per hour/second of run time. ECS charges for the underlying EC2 resources plus a small fee for the container management.

- Auto-scaling works differently. With EC2 you scale by launching instances based on rules. ECS auto-scales by adjusting the number of tasks/containers running.

- EC2 requires you to configure and optimize the OS and resources. ECS simplifies resource optimization through features like cluster auto-scaling.

- ECS integrates with other AWS services like load balancing, logging, monitoring etc. You have to configure these separately for EC2.

So in summary, EC2 gives you full control of virtual machine instances, while ECS abstracts away infrastructure and lets you focus on deploying and scaling containerized applications.

77.	How can you troubleshoot network connectivity issues with an EC2 instance?
Here are some tips for troubleshooting network connectivity issues with an EC2 instance:

- Check the security group rules associated with the instance - make sure ports/protocols required for connectivity are open.

- Verify the subnet and route table configuration - ensure the instance is in a public subnet with a route to the internet gateway if internet access is required. 

- Check the network ACL rules for the subnet - restrictive rules can block traffic.

- Check if the instance has a public IP address assigned. If not, associate an Elastic IP address.

- Try rebooting the instance in case networking components need resetting.

- Use the EC2 console to check if Status Checks are passing - failing checks indicate an issue.

- Log into the instance and use ping, traceroute to test basic connectivity.

- Inspect the VPC flow logs to see if expected traffic is reaching the instance. 

- Check CloudWatch metrics for the instance's network interfaces to see traffic patterns.

- If attaching to a load balancer, make sure the instance is registered with the target group and passed health checks.

- For Windows instances, remote desktop in to inspect network adapter settings/status.

- For deeper diagnosis, use packet capture tools like Wireshark or tcpdump.

- Check with AWS support if the connectivity issue persists without an obvious cause.

78.	What is the purpose of using placement groups in EC2?

Placement groups in EC2 allow you to influence the placement of instances within an Availability Zone (AZ). Using placement groups can improve performance and reduce latency for inter-connected instances.

Some key benefits and use cases for EC2 placement groups include:

- **Cluster** - Packs instances close together in a single AZ. This provides low network latency and high network throughput between instances, which is great for HPC and big data workloads.

- **Spread** - Spreads instances across underlying hardware. This reduces correlation in failures and is ideal for distributed and replicated workloads (e.g. Hadoop, Cassandra).

- **Partition** - Spreads instances across logical partitions, ensuring that groups don't share the same partitions. Useful for large distributed and replicated workloads with critical high-availability needs. 

- Allows control over instance placement to optimize for the topology of your application.

- Reduce latency between application tiers or network hops.

- Increase bandwidth between instances for high throughput demands.

- Improve performance consistency by eliminating variable network response times.

So in summary, placement groups let you optimize instance placement for the performance and availability needs of your workload.

79.	How can you enable and configure instance metadata service on EC2 instances?
The instance metadata service provides information about your EC2 instance to the software running on the instance. Here are the key steps to enable and configure the metadata service:

- By default, the instance metadata service is enabled for all EC2 instances. No explicit configuration is needed.

- To enhance security, you can require the use of IMDSv2 when requesting instance metadata by setting the "require-imdsv2" flag on the instance or its subnet settings.

- Access instance metadata by querying http://169.254.169.254/latest from the instance. Metadata categories include hostname, public keys, security credentials etc.

- To retrieve a specific metadata value, append the path e.g. http://169.254.169.254/latest/meta-data/public-hostname

- Metadata can also be queried via the command line using the EC2 metadata CLI included on Amazon Linux and the AWS CLI.

- You can add your own custom metadata tags to instances which software can then lookup via the metadata service.

- Configure IAM policies and security groups to control access to metadata service from your instances and applications.

- To improve performance, use caching proxies like nimbus, ssm-cache or EC2 metadata query caches.

- On sensitive instances, you may want to completely disable the metadata service. This can be done using firewall rules, network ACLs or by disabling the service on the instance.

So in summary, the metadata service is enabled by default and provides useful instance info. You can enhance security and performance using IMDSv2, caching, and restricting access.


Here are some tips for configuring and interacting with the EC2 instance metadata service using the AWS CLI:

- The AWS CLI includes a "ec2-instance-metadata" command to interact with the metadata service.

- To require IMDSv2 when requesting metadata, use the modify-instance-metadata-options CLI command:

```bash
aws ec2 modify-instance-metadata-options --instance-id i-1234567890abcdef0 --http-tokens required-imdsv2
```

- To query instance metadata from the command line: 

```
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/
```

- You can retrieve a specific metadata attribute by appending the path:

```bash 
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/public-ipv4
```

- To add a custom metadata tag:

```
aws ec2 create-tags --resources i-1234567890abcdef0 --tags Key=Team,Value=DevOps
```

- Then query it:

```
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/tags/Team
```

- To restrict access, use IAM policies to limit the "ec2:DescribeInstances" permission to authorized roles/users.

- Also restrict access to the metadata endpoint 169.254.169.254 using security groups or NACL rules.

So in summary, the AWS CLI provides convenient access to configure and interact with instance metadata on the command line.

80.	Explain the difference between an instance store and an EBS volume.
The key differences between EC2 instance stores and EBS volumes are:

- **Instance Store**: This is ephemeral storage physically attached to the host server of the EC2 instance. Instance store provides high IOPS but the data does not persist when the instance is stopped/terminated.

- **EBS Volume**: This is network attached persistent block storage. Volumes exist independently from EC2 instances and persist beyond the lifetime of instances. 

- Instance stores offer higher and more consistent I/O performance compared to EBS volumes.

- Data on instance stores cannot be resized or detached. EBS volumes offer flexible sizing and can be detached/reattached to instances.

- Data on instance stores will be lost if the instance fails. EBS volume data persists independently.

- Snapshots and backups are only available for EBS volumes. Data on instance stores can only be backed up manually. 

- By default, the root volume for EC2 instances comes from an instance store. For persistence, this should be changed to an EBS volume.

- Instance types like the M5 support both instance store and EBS volumes. Some instance types support only EBS backed instance storage.

In summary, instance stores offer high ephemeral IOPS while EBS offers network attached persistent storage. The choice depends on your data persistence needs and performance requirements.

81.	How can you migrate an EC2 instance from EC2-Classic to EC2-VPC?

Here are the steps to migrate an EC2 instance from EC2-Classic to EC2-VPC:

1. Create a VPC and subnets for the instance to migrate into. 

2. Create a ClassicLink-enabled VPC security group that will be associated with the instance. This allows communication between EC2-Classic and VPC.

3. Stop the EC2-Classic instance if it is running.

4. Detach any Elastic IP addresses associated with the instance.

5. Right click the instance in the EC2 console and select "Migrate to VPC".

6. Select the VPC, subnets, and security group you created for the migration.

7. The instance will be migrated over with a new private IP address. 

8. Start the instance and test connectivity. Attach Elastic IPs if needed.

9. Once migration is successful, terminate the ClassicLink security group if no longer needed.

10. Finally, release the EC2-Classic IPv4 address associated with the instance.

Key things to note are stopping the instance, detaching EIPs, using a ClassicLink security group, and getting a new private IP after migration. Testing connectivity is important before deleting old configurations. This overall process migrates the instance while minimizing downtime.

Here are the steps to migrate an EC2 instance from EC2-Classic to EC2-VPC using the AWS CLI:

1. Create a VPC and subnets to migrate the instance into:

```
aws ec2 create-vpc --cidr-block 10.0.0.0/16

aws ec2 create-subnet --vpc-id vpc-abcd1234 --cidr-block 10.0.1.0/24 
```

2. Create a ClassicLink-enabled security group: 

```
aws ec2 create-security-group --group-name VPC-Classic-SG --description "ClassicLink SG" --vpc-id vpc-abcd1234
```

3. Stop the EC2-Classic instance:

```
aws ec2 stop-instances --instance-ids i-1234567890abcdef0 
```

4. Detach any Elastic IP address from the instance:

```
aws ec2 disassociate-address --association-id eipassoc-0a1b2c3d4e5f6g7h8
```

5. Migrate the instance to the VPC:

```
aws ec2 modify-instance-placemenet --instance-id i-1234567890abcdef0 --subnet-id subnet-a1b2c3d4  --security-group-ids sg-98h7g6f5
```

6. Start the instance and test connectivity.

7. Delete the ClassicLink security group if no longer needed: 

```
aws ec2 delete-security-group --group-id sg-98h7g6f5
```

8. Release the EC2-Classic IPv4 address:

```  
aws ec2 release-address --allocation-id eipalloc-a1b2c3d4
```

This performs the key steps for migrating an EC2 instance from EC2-Classic to EC2-VPC using the AWS CLI.


82.	What is the purpose of an ENI (Elastic Network Interface) in EC2?

An Elastic Network Interface (ENI) on EC2 serves several purposes:

- Primary network interface - An ENI acts as the primary network interface attached to an EC2 instance via which it connects to a subnet and VPN.

- Additional network interfaces - You can attach additional ENIs to an instance to allow connectivity to multiple subnets/networks. Useful for dual-homed instances.

- IP addresses management - An ENI is assigned a primary private IP address and can have multiple secondary private and public IP addresses.

- Security groups - Security groups are attached to an ENI to control inbound and outbound traffic.

- Network appliance delivery - An ENI can be created independently and attached/detached to instances as needed for use with network appliances.

- Management network - A separate ENI can be created on management instances to isolate the management plane traffic.

- Low interruption detachment - ENIs allow you to detach/reattach network interfaces with minimal instance interruption.

- Elastic IPs - Elastic IP addresses are associated with ENIs for static public IP addressing.

In summary, ENIs provide life-cycle management of network interfaces and IP addresses and allow you to architect network topology flexibility across subnets and security groups.

83.	How can you attach a network interface to an EC2 instance?
Here are the steps to attach a network interface to an existing EC2 instance:

1. Create an Elastic Network Interface (ENI) in the same subnet as your instance:

```
aws ec2 create-network-interface --subnet-id subnet-01234567890abced 
```

2. Retrieve the ENI id from the response.

3. Attach the ENI to your EC2 instance specifying the ENI id:

```
aws ec2 attach-network-interface --network-interface-id eni-01234567890abcdef --instance-id i-09876543210abcdef --device-index 1
```

4. Optionally modify the ENI attributes like description or security groups: 

```
aws ec2 modify-network-interface-attribute --network-interface-id eni-01234567890abcdef --description " secondary ENI"
```

5. Connect to the EC2 instance and configure the new network interface. For Linux, check for the interface name like eth1 in ifconfig output.

6. Assign an IP address to the interface or use DHCP to retrieve an IP. Update routing and firewall rules.

7. Test connectivity over the new ENI. 

So in summary, use the create-network-interface, attach-network-interface, and modify-network-interface-attribute CLI commands to add and configure a new ENI on your EC2 instance.

84.	Explain the concept of EC2 instance metadata and how it can be accessed.

EC2 instance metadata is data about your instance that you can use to configure or manage the running instance. Metadata is available from a REST API endpoint for all EC2 instances. 

Some key points about EC2 instance metadata:

- It is exposed via a REST API available at http://169.254.169.254/latest/meta-data from your instance.

- You don't authenticate to access metadata, but security groups/NACLs can restrict access.

- Metadata categories include hostname, public keys, instance ID, security groups, block device mapping etc.

- You can retrieve the full metadata using GET requests or get specific values by appending a path e.g. /public-keys/

- Metadata can be accessed via the command line using tools like curl, wget or the EC2 metadata CLI.

- AWS CLI also includes commands like "aws ec2-instance-metadata" to access metadata.

- User-defined metadata can also be added as tags and retrieved from the /tags path. 

- Metadata is useful for cloud-init scripts or bootstrap configurations using values specific to an instance.

- Caching proxies like nimbus can be used to reduce metadata traffic overhead.

So in summary, EC2 instance metadata provides a simple REST API to access useful information about your instance that can help configure and manage it at runtime.

Here are some examples of accessing EC2 instance metadata using the AWS CLI:

- Get the full metadata document:

```bash
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data 
```

- Get the instance ID:

```bash
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/instance-id
``` 

- Get the public hostname:

```bash
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/public-hostname  
```

- Get the security groups:

```bash
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/security-groups
```

- Get block device mapping:

```bash
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/block-device-mapping 
```

- Get user-defined metadata tag value: 

```bash
aws ec2-instance-metadata --metadata http://169.254.169.254/latest/meta-data/tags/Name
```

- Query using instance metadata category paths or get the full metadata document.

- Use the CLI for easy access without installing additional tools.

- Metadata can help provide instance-specific values for automation.


85.	How can you troubleshoot high network latency on an EC2 instance?

Here are some tips for troubleshooting high network latency on an EC2 instance:

- Check instance metrics in CloudWatch - look for spikes in network in/out and high CPU utilization as indicators.

- Validate security group rules are not too restrictive - ensure required ports/protocols are open.

- Try rebooting the instance in case the network stack needs resetting.

- Use network tools like ping, traceroute to check latency to different destinations and isolate the issue.

- Change the instance to a different subnet/AZ to see if latency improves - narrows down physical network issues.

- For high internet latency, check the NAT gateway metrics if being utilized. Scale up NAT GW if needed. 

- Attach the instance to a load balancer and compare latency - isolates the issue to NLB or instance.

- Check VPC flow logs for any dropped, rejected packets.

- Use packet capturing tools like Wireshark or tcpdump to inspect traffic.

- Analyze EC2 instance neighbor logs for any correlated latency.

- Open a case with AWS support for further troubleshooting if the cause is still unclear.

- Consider migrating to another instance type or optimization if latency is consistently high.

So in summary, utilize metrics, logs, traces, isolation, and tools to narrow down the root cause and engagement with AWS support can help resolve difficult issues.


86.	What is the difference between instance-based and container-based virtualization?
The main differences between instance-based and container-based virtualization are:

- Instance-based (e.g. EC2): A hypervisor abstracts and allocates hardware resources to create isolated virtual machine instances. Each VM includes a full OS, apps, binaries and libraries.

- Container-based (e.g. ECS): Containers share the host OS kernel and libraries. Each container holds only the application, binaries and dependencies. Containers are more lightweight.

- VMs provide stronger isolation and security boundaries between instances. Container isolation is implemented via namespaces and control groups.

- VM startup time is slower due to booting up full OS. Containers start almost instantly.

- VMs can run different OS & versions than host. Containers require same base OS kernel as host. 

- Scaling containers is faster as they are lighter weight. VMs take more time and resources to provision and boot up.

- Hardware resource utilization is more efficient with containers due to sharing libraries and OS.

- Container portability is better since the environment and dependencies are packaged together.

In summary, VMs provide strong isolation but can be heavyweight. Containers enable faster and more efficient scaling, at the cost of weaker isolation from the shared kernel.

87.	How can you enable and configure EC2 instance termination protection?

Here are the steps to enable and configure EC2 instance termination protection:

1. Open the EC2 console and select the instance you want to protect.

2. Click on the "Instance Settings" button and select "Change Termination Protection".

3. Toggle the "Enable" button to enable termination protection.

4. You can also enable termination protection when launching an instance via the EC2 console or CLI:

```
aws ec2 run-instances --disable-api-termination
```

5. By default, the root user will still be able to terminate protected instances. 

6. To prevent even root from terminating, apply an IAM policy to the instance that denies the ec2:TerminateInstances action.

7. You can also protect instances using Resource Groups and tag restrictions.

8. To disable termination protection later, return to the Instance Settings and toggle it off.

So in summary, enable termination protection on instance launch, or by modifying the instance attributes. Use IAM policies, Resource Groups and tags for more complex protection.

88.	Explain the difference between EC2 instance and ECS task definitions.
The main differences between EC2 instance definitions and ECS task definitions are:

- EC2 instance definition specifies the AMI, instance type, storage, security groups etc. needed to launch an instance. 

- ECS task definition specifies the docker image, CPU/memory requirements, ports, environment variables etc. needed to launch a container.

- Instance definitions control the infrastructure resources. Task definitions focus on the application requirements.

- When scaling EC2, new instances are launched from the definition. With ECS, more copies of the task are placed onto existing infrastructure.

- EC2 instances persist until terminated. ECS tasks are ephemeral and exit when the processing is completed. 

- EC2 instance definitions are immutable. Task definitions can be versioned but the desired count is mutable.

- ECS allows multiple task definitions to run on the same cluster to optimize resource usage.

- EC2 auto-scaling scales out based on fleet metrics like CPU utilization. ECS scaling is driven by your desired task count. 

- Task definitions can be tweaked to run multiple containers per task. Instance defs define one VM.

So in summary, instance definitions control the infrastructure while task definitions focus on running the applications using containers.

89.	How can you create an EC2 instance using AWS CloudFormation?
Here is an example of creating an EC2 instance using AWS CloudFormation:

1. Define the EC2 instance resource in your CloudFormation template YAML:

```yaml
Resources:
  MyEC2Instance: 
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0abcdef1234567890  
      InstanceType: t2.micro
      KeyName: my-key-pair
      SecurityGroups:
        - !Ref InstanceSecurityGroup
```

2. Specify the AMI ID, instance type, key pair, and security group for the instance.

3. Create a security group resource to allow inbound traffic:

```yaml  
  InstanceSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow SSH  
      SecurityGroupIngress:
        - CidrIp: 0.0.0.0/0 
          IpProtocol: tcp
          FromPort: 22
          ToPort: 22
```

4. Deploy the CloudFormation stack to launch the resources. 

5. The EC2 instance will be created with the parameters defined in the template.

6. You can modify properties like InstanceType to update the instance via stack updates.

So CloudFormation provides a consistent and repeatable way to deploy EC2 instances instead of manual creation. Parameters and mappings can be used to customize deployments.


90.	What is the purpose of EC2 instance roles and how are they used?

EC2 instance roles allow you to securely pass AWS credentials to an EC2 instance to access other AWS services and resources. Key points:

- An IAM role can be attached to an EC2 instance defining its permissions policy.

- When attached, temporary security credentials are automatically generated and rotated on the instance.

- These credentials can be used by apps on the instance to make AWS API calls without having to manage long-term keys.

- Credentials are delivered via the EC2 metadata service accessed at 169.254.169.254.

- Instance roles avoid having to embed IAM keys within EC2 instances making it more secure.

- Roles can be attached when launching instances via the AWS console or CLI.

- Roles can be attached, detached or replaced on running instances without having to restart. 

- Common uses are allowing EC2 instances to access S3, DynamoDB, ECR, etc to deploy apps or process data.

- IAM policies applied to the role control which services and resources the instance has access to. 

So in summary, instance roles provide temporary AWS credentials to EC2 instances allowing secure API access without long-term keys. They are very useful for granting access to other services from your instances.

Here is an example of creating and attaching an IAM role to an EC2 instance using AWS CLI:

1. Create an IAM role with necessary permissions:

```bash
aws iam create-role --role-name my-ec2-role --assume-role-policy-document file://ec2-trust-policy.json
```

2. Attach IAM policies to allow required access:

```bash
aws iam attach-role-policy --role-name my-ec2-role --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
```

3. Launch an EC2 instance and specify the IAM role: 

```bash
aws ec2 run-instances --image-id ami-abc1234 --iam-instance-profile Name="my-ec2-role"
``` 

4. Or attach the role to an existing instance:

```bash
aws ec2 associate-iam-instance-profile --iam-instance-profile Name="my-ec2-role" --instance-id i-01234567890
```

5. SSH into the instance and retrieve credentials:

```bash
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/my-ec2-role
```

6. Use the credentials in the AWS CLI or SDK to access other services like S3.

7. Update the role and policy as needed without restarting the instance.

So the AWS CLI provides a convenient way to manage and attach IAM roles to EC2 instances for secure access to AWS resources.


91.	How can you enable and configure enhanced networking for EC2 instances?
Here are the steps to enable and configure enhanced networking for EC2 instances:

1. Choose an instance type that supports enhanced networking. Generally newer generation instance families like C5, M5 etc. 

2. When launching the instance, select an AMI that has enhanced networking drivers pre-installed. Amazon Linux 2 AMIs include the Elastic Network Adapter (ENA) driver.

3. Ensure the instance is launched in a VPC, not EC2-Classic. Enhanced networking requires VPC.

4. In the advanced network configuration, enable "Elastic Network Interface" and/or "Elastic Fabric Adapter" based on the instance type capabilities.

5. Attach the IAM role required by enhanced networking to allow access to create and manage ENIs.

6. After launching, check for the ENA/EFA devices in the instance from the OS using ip or ifconfig commands.

7. Install applications and configure to use the enhanced networking devices instead of the default Ethernet device.

8. Use available ENA/EFA metrics in CloudWatch to monitor performance.

9. Configure Flow Logs on the VPC to capture traffic patterns.

Enhanced networking provides lower latency, lower jitter, higher packet-per-second performance for network intensive applications. Correct IAM roles, interface configuration and metrics monitoring are key.

Here is an example of enabling enhanced networking for an EC2 instance using the AWS CLI:

1. Create a VPC and subnet:

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16

aws ec2 create-subnet --vpc-id vpc-abc123 --cidr-block 10.0.1.0/24
```

2. Create a security group:

```
aws ec2 create-security-group --group-name my-sg --description "Security group for ENA" --vpc-id vpc-abc123
```

3. Create an IAM role for EC2 enhanced networking:

```
aws iam create-role --role-name EC2EnhancedNetworkingRole --assume-role-policy-document file://ena-trust-policy.json
```

4. Launch an EC2 instance with enhanced networking enabled:

```bash
aws ec2 run-instances --image-id ami-abc1234 --instance-type c5.large --ena-support --iam-instance-profile Arn=arn:aws:iam::123456789012:role/EC2EnhancedNetworkingRole  
```

5. Attach the security group to the network interface:

```
aws ec2 modify-network-interface-attribute --network-interface-id eni-1a2b3c4d --groups sg-123abc
``` 

6. Connect to the instance and configure the ENA interface.

7. Enable Flow Logs on the VPC to monitor traffic.

This demonstrates using the AWS CLI to set up the necessary VPC, IAM role, instance config and logging to leverage enhanced networking.


92.	Explain the difference between an EC2 instance and a Lambda function.

The main differences between EC2 instances and Lambda functions are:

- EC2 provides configurable virtual machine instances that run whatever software/apps you need. Lambda runs pre-defined functions in response to triggers.

- EC2 instances are always running when launched. Lambda functions are event-driven and run on-demand. 

- EC2 instances are billed for every second/hour the instance runs. Lambda bills only for compute time used when a function executes.

- EC2 requires you to manage the OS, updates, scaling, high availability. Lambda abstracts away all server management.

- Scaling EC2 involves launching instances based on metrics like CPU. Lambda scales intrinsically based on usage.

- EC2 is customizable but requires more DevOps overhead. Lambda simplifies operations via auto-scaling and built-in HA.

- State is persisted on EC2 using storage like EBS. Lambda function state needs to be stored externally in services like S3. 

- Lambda execution environments are immutable and consistent. EC2 instance state can drift over time.

- Lambda is well-suited for event-driven compute and processing data in object storage. EC2 is flexible for hosting custom apps and databases.

In summary, EC2 provides configurable VMs while Lambda offers serverless, event-driven functions. The choice depends on the architecture, app design and operational needs.


93.	How can you migrate an EC2 instance from one region to another?
Here are the typical steps to migrate an EC2 instance from one region to another:

1. Take an AMI image snapshot of the EC2 instance in the source region.

2. Copy the AMI snapshot to the target region using the EC2 console, CLI or API.

3. Launch an EC2 instance from the copied AMI in the target region. 

4. Update the new instance if needed - assign a new IP, attach volumes, join VPC/subnets etc.

5. Update DNS records and database configurations to point to the new instance.

6. Redirect load balancer traffic to the new instance and remove the old instance.

7. Test the new instance and applications thoroughly.

8. Once stable, terminate the original instance in the source region if no longer needed.

9. Delete any unused dependencies like EIPs or network interfaces in the source region.

Some key points are taking an AMI snapshot to migrate state, directing traffic to the new instance, and cleaning up old resources once migration is complete. Testing validation is crucial to avoid application downtime.


Here is an example of migrating an EC2 instance across regions using the AWS CLI:

1. Stop the instance in the source region: 

```bash
aws ec2 stop-instances --instance-ids i-01234567890abcdef
```

2. Create an AMI from the instance:

```bash 
aws ec2 create-image --instance-id i-01234567890abcdef --name migration-ami --description "AMI for migration"
```

3. Copy the AMI to the target region:

```bash
aws ec2 copy-image --source-region us-east-1 --source-image-id ami-abc123 --region us-west-2
```

4. Launch an instance in the target region from the copied AMI:

```bash
aws ec2 run-instances --image-id ami-123abcd --instance-type t2.micro --key-name mykey --subnet-id subnet-456abcdef
``` 

5. Update DNS records and configurations to use the new instance.

6. Terminate the original instance:

```bash
aws ec2 terminate-instances --instance-ids i-01234567890abcdef
```

7. Delete unused resources in the source region like VPCs, snapshots.

This demonstrates the key steps of stopped instance, creating AMI, copying to new region, launching instance, redirecting traffic, and cleaning up.

94.	What is the purpose of user data in EC2 instances and how can it be used?

User data in EC2 allows you to provide custom scripts or configurations that the instance will execute during the initial boot process. Some common uses cases include:

- Installing software packages needed by your application (yum, apt, pip etc).

- Downloading application code from S3 or GitHub. 

- Running configuration management tools like Ansible/Chef/Puppet.

- Joining the instance to a Windows domain.

- Registering the instance with a load balancer or service discovery.

- Generating authentication keys to allow secure connectivity.

- Setting up log collection by installing agents. 

- Passing in cloud-init directives to customize the instance at launch.

- Defining bootstrap scripts to prepare storage, update packages.

- Setting environmental variables needed by your apps.

User data is limited to 16KB if provided as plain text. For larger data, it can be stored in S3 and downloaded via a script. By automatically executing tasks at launch, user data can prep your instance without manual intervention.

Here is an example of passing user data to an EC2 instance using the AWS CLI:

1. Create a user data script:

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
```

2. Save the script as user-data.sh

3. Launch an EC2 instance, passing the user data script using the --user-data option:

```bash  
aws ec2 run-instances --image-id ami-abc1234 --instance-type t2.micro --key-name mykey --security-groups my-sg --user-data file://user-data.sh
```

4. The user data will execute during initial launch, installing httpd and starting the web server.

5. Check that it worked by connecting to the instance and verifying httpd is running:

```
sudo systemctl status httpd
```

6. For larger scripts, upload to S3 first, then pass the S3 URL as user data:

```
aws ec2 run-instances --user-data https://s3.amazonaws.com/mybucket/userdata.sh
```

This demonstrates how the CLI --user-data parameter can be used to automate EC2 instance configuration and bootstrap application code during launch.

95.	How can you attach and detach an EBS volume from an EC2 instance using CLI?
Here are the steps to attach and detach an EBS volume from an EC2 instance using the AWS CLI:

To attach a volume:

1. Create an EBS volume:

```bash
aws ec2 create-volume --size 100 --region us-east-1 --availability-zone us-east-1a
```

2. Retrieve the volume ID from the output.

3. Attach it to the instance, specifying the volume and instance IDs: 

```bash
aws ec2 attach-volume --volume-id vol-01234567890abcdef --instance-id i-09876543210abcde --device xvdf
```

To detach a volume:

1. List the volumes and note the volume ID:

```bash
aws ec2 describe-volumes
```

2. Detach the volume specifying the volume ID:

```bash
aws ec2 detach-volume --volume-id vol-01234567890abcdef
```

3. The volume will be available for attaching to other instances.

Key options are specify volume ID, instance ID, device name when attaching and specifying volume ID when detaching. This allows managing EBS volumes on EC2 instances via the CLI.


96.	Explain the concept of EC2 instance health checks and how they work.
EC2 instance health checks allow you to monitor the health status of your instances and automate recovery if needed. Here's an overview:

- Two types of health checks - System status checks monitor the AWS instance infrastructure. Instance status checks monitor the software and network configuration of your instance.

- Status checks are automated - performed every minute by the EC2 service.

- Checks monitor metrics like CPU, network connectivity, disk status to determine instance health.

- Statuses can be: Passing, Warning, Impaired, Insufficient data.

- If system status is Impaired, AWS will automatically recover the instance by stopping and restarting it.

- If instance status is Impaired, you need to troubleshoot and manually recover the instance.

- Status check information is available through the CLI, API and in the EC2 console.

- You can also configure CloudWatch alarms based on status check failures.

- By default, both system and instance level checks are enabled. 

- Instance checks can be disabled if you don't want automatic recovery.

So in summary, EC2 health checks provide automated monitoring of system and instance health, enabling self-recovery of system issues and notifications for instance problems.

Here are some examples of using the AWS CLI to check EC2 instance health status:

- View system and instance status of all instances:

```bash
aws ec2 describe-instance-status --include-all-instances
```

- Check system status of a specific instance: 

```bash 
aws ec2 describe-instance-status --instance-ids i-01234567890abcd --include-all-instances --query "InstanceStatuses[*].SystemStatus.Status"
```

- Check instance status:

```bash
aws ec2 describe-instance-status --instance-ids i-01234567890abcd --include-all-instances --query "InstanceStatuses[*].InstanceStatus.Status" 
```

- List instances with impaired system status:

```bash
aws ec2 describe-instance-status --filters Name=instance-status.status,Values=impaired --query "InstanceStatuses[*].InstanceId"
```

- Monitor status in CloudWatch:

```bash
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name StatusCheckFailed_System --statistics Maximum
```

- Create alarm on status check failures:  

```bash 
aws cloudwatch put-metric-alarm --alarm-name status-check-failed --metric-name StatusCheckFailed_System --statistic Maximum --threshold 1 --comparison-operator GreaterThanOrEqualToThreshold --period 60 --evaluation-periods 1 --namespace AWS/EC2 
```

This demonstrates how to retrieve and monitor instance status via the CLI. Automated checks allow detecting and recovering from system and instance health issues.


97.	How can you create and restore a snapshot of an EBS volume?

Here are the steps to create and restore an EBS volume snapshot using the AWS CLI:

To create a snapshot:

1. List volumes and note the volume ID:

```bash 
aws ec2 describe-volumes
```

2. Create a snapshot of the volume:

```bash
aws ec2 create-snapshot --volume-id vol-01234567890abcdef --description "Backup vol-01"
```

3. The snapshot ID will be returned in the output. 

To restore from a snapshot:

1. List snapshots and note the snapshot ID to restore from:

```bash
aws ec2 describe-snapshots
```

2. Create a new EBS volume from the snapshot:

```bash 
aws ec2 create-volume --snapshot-id snap-01234567890abcdef --availability-zone us-east-1a 
```

3. The new volume will be created from the snapshot data.

4. Attach and mount the volume to an EC2 instance if needed.

This allows backing up and restoring EBS volumes using CLI snapshots. Automated snapshots can also be created and Lifecycle policies enabled for managing backups.


98.	What is the difference between instance types and instance families in EC2?
The main differences between EC2 instance types and instance families are:

- Instance types define specific configurations of CPU, memory, storage and networking capacity for an instance. For example, t2.micro, m5.large, r5d.xlarge etc.

- Instance families are a grouping of similar instance types optimized for certain use cases. Families include T, M, C, R, X, Z and more. 

- Families are designated by the first letter of the instance type - e.g. C for Compute Optimized, R for Memory Optimized.

- Instance types offer different ratios of resources within a family - e.g. higher compute for C4 vs C5.

- Instance families are optimized for workloads like:

  - T2/T3 - Burstable small general purpose apps

  - M5 - General purpose, web servers

  - C5 - High CPU based compute like batch processing

  - R5 - High memory intensive apps like databases

  - G4 - GPU based machine learning, video encoding  

- Newer generation instance families like C5 often include advanced features like ENA networking.

- You select an instance type based on the resources needed by your application.

- Then choose a family that provides an optimized configuration profile for your use case.

So in summary, instance families represent a class of instance types tailored for a particular workload. Instance types provide sizing within a family.


99.	How can you perform rolling updates on an ECS service?
Here are the steps to perform rolling updates on an ECS service:

1. Update the task definition with the new application version. 

2. Configure the deployment configuration for the service:

```
aws ecs create-service --deployment-configuration "maximumPercent=100, minimumHealthyPercent=50"
```

3. This will deploy new tasks before stopping old ones.

4. Update the service to use the new task definition:

```
aws ecs update-service --cluster my-cluster --service my-service --task-definition new-task-def:1
``` 

5. ECS will stop old tasks and launch new ones based on the deployment configuration.

6. The load balancer or service discovery should route traffic to the new tasks.

7. Monitor the rollout in the ECS console or CLI and roll back if there are issues:

```
aws ecs update-service --service my-service --task-definition previous-task-def:1 
```

Key points are updating the task definition, configuring deployment options, updating the service, and monitoring the rollout. This allows replacing tasks in a controlled manner for continuous deployments.

100. Explain the difference between EC2 instance store-backed and EBS-backed instances.



![image](https://github.com/plaethos09/Devops_Answers/assets/114465056/88fb986c-23c4-48bd-a896-d01a6154bf97)
