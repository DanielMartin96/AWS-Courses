# EC2 Fundamentals

## EC2 Basics

### Amazon EC2
- EC2 is one of the most popular AWS offerings
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- Renting virtual machines (EC2)
- Storing data on virtual drives (EBS)
- Distributing load accross machines (ELB)
- Scaling the services using an auto-scaling group (ASG)
- Knowing EC2 is fundamental to understand how the Cloud works

### EC2 sizing & configuration options
- Operating System (**OS**): Linux, Windows or Mac OS
- How much compute power & cores (CPU)
- How much random-access memory (RAM)
- How much storage space: Network-attached (EBS & EFS) or Hardware (EC2 Instance Store)
- Network card: speed of the card, Public IP address
- Firewall rules: **security group**
- Bootstrap script (configure at first launch): EC2 User Data

### US2 User Data
- It is possible to bootstrap our instances using an EC2 User Data Script
- Bootstrapping means launching commands when a machine starts
- That script is only run once at the instance first start
- Used to install updates
- Used to install software
- Used to download common files from the internet
- The EC2 User Data Script runs with the root user

## EC2 Instance Types Basics

### EC2 Instance Types - General Purpose 
- Great for diversity of workloads such as web servers or code repositories
- Balance between Compute, Memory and Networking

### EC2 Instance Types - Compute Optimised
- Great for compute-intensive tasks that require high performance processors
- Batch processing workloads
- Media transcoding
- High performance web servers
- High performance computing (HPC)
- Scientific modeling & machine learning
- Dedicated gaming servers


### EC2 Instance Types - Memory Optimised
- Fast performance for workloads that process large data sets in memory
- High performance, relational/non-relational databases
- Distributed web scale cashe stores
- In-memory databases optimised for BI (business intelligence)
- Applications performing real-time processing of big unstructured data

### EC2 Instance Types - Storage Optimised
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- High frequency online transaction processing (OLTP) systems
- Relational & NoSQL databases
- Cache for in-memory databases (for example, Redis)
- Data warehousing applications 
- Distributed file systems

## Security Groups & Classic Ports Overview
- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 instances
- Security groups only contain **allow** rules
- Security groups rules can reference by IP or security group
- Security groups are acting as a "firewall" on EC2 instances
- They regulate Access to Ports
- They regulate Authorised IP ranges - IPv4 and IPv6
- They regulate Control of inbound network (from other to the instance)
- They regulate Control of outbound network (from instance to other)

### Security Groups Good to Know
- Can be attached to multiple instances
- Locked down to a region/VPC combination
- Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it 
- It's good to maintain one separate security group for SSG access
- If your application is not accessible (time out), then it's a security group issue
- If your application gives a "connection refused" error, then its an application error or it's not launched
- All inboud traffic is **blocked** by default
- All outbound traffic is **authorised** by default 

### Classic Ports to know
- 22 = SSH (Secure Shell) - log into a Linux instance
- 21 = FTP (File Transfer Protocol) - upload files into a file share
- 22 - SFTP (Secure File Transfer Protocol) - upload files using SSH
- 80 - HTTP - access unsecured websites
- 443 = HTTPS = access secured websites
- 3389 - RDP (Remote Desktop Protocol) - log into a Windows instance

## SSH Overview
| SSH    | Putty    | EC2 Instance Connect    |
|---------------- | --------------- | --------------- |
| X    |     | X    |
| X    |     | X    |
|    | X   | X   |
| X   | X   | X   |

## EC2 Instance Purchasing Options 
- **On-Demand Instances** - short workload, predictable pricing, pay by second
- **Reserved** (1 & 3 years): Reserved Instances - long workloads. Convertible Reserved Instances - long workloads with flexible instances
- **Saving Plans** (1 & 3 years) - commitment to an amount of usage, long workload
- **Spot Instances** - short workloads, cheap, can lose instances (less reliable)
- **Dedicated Hosts** - book an entire physical server, control instance placement
- **Dedicated Instances** - no other customers will share your hardware
- **Capacity Reservations** - reserve capacity in a specific AZ for any duration

### EC2 On Demand
- Pay for what you use: Linux or Windows - billing per second, after the first minute. All other operating systems - billing per hour
- Has the highest cost but no upfront payment
- No long-term commitment 

- Recommended for **short-term** and **un-interrupted workloads,** where you can't predict how the application will behave  

### EC2 Reserved Instances
- You reserve a specific instance attributes **(Instance Type, Region, Tenancy, OS)** 
- **Reservation Period** - **1 year** (+discount) or **3 years** (+++ discount)  
- **Payment Options** - **No Upfront (+), Partial Upfront (++), All Upfront (+++)** 
- **Reserved Instance's Scope** - **Regional** or **Zonal** (reserve capacity in an AZ)  
- Recommended for steady-state usage applications (think database)
- You can buy and sell in the Reserved Instance Marketplace

- Convertible Reserved Instance: Can change the EC2 instance type, instance family, OS, scope and tenancy

### EC2 Saving Plans
- Get a discount based on long-term usage
- Commit to a certain type of usage
- Usage beyond EC2 Savings Plans is billed at the On-Demand price 

- Locked to a specific instance family & AWS region (eg. M5 in eu-east-1)
- Flexible accross: Instance Size, OS, Tenancy

### EC2 Spot Instances
- Instances that you can "lose" at any point of time if your max price is less than the current spot price
- The **MOST cost-efficient** instances in AWS

- Useful for workloads that are resilient to failure: Batch jobs, data analysis, image processing, any **distributed** workloads, workloads with a flexible start and end 17:39

- **Not suitable for critical jobs or databases** 

### EC2 Dedicated Hosts
- A physical server with EC2 instance capacity fully dedicated to your use
- Allows you address **compliance requirements** and **use your existing server-bound software licenses** (per-socket, per-core, pe--VM software licenses)
- Purchasing Options: **On-demand** - pay per second for active Dedicated Hosts. **Reserved** - 1 or 3 years (No Upfront, Partial Upfront and All Upfront)  
- The most expensive option

- Useful for software that have complicated licensing model (BYOL - Bring Your Own License)
- Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
- Instances run on hardware that is dedicated to you
- May share hardware with other instances in same account
- No control over instance placement (can move hardware Stop/Start)

### EC2 Capacity Reservations
- Reserve **On-Demand** instances capacity in a specific AZ for any duration
- You always have access to EC2 capacity when you need to
- **No time commitment** (create/cancel anytime), **no billing discounts**
- Combine with Regional Reserved Instances and Saving Plans to benefit from billing discounts
- You're charged at On-Demand rates whether you run instances or not

- Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ

### Which purchasing option is right for me?
- **On demand:** coming and staying in resort whenever we like, we pay the full price
- **Reserved:** like planning ahead and if we plan to stay for a long time, we may get a good discount 
- **Savings Plans:** pay a certain amount per hour for certain period and stay in any room type
- **Spot instances:** the hotel allows people to bid for the empty rooms and the highest bidder keeps the rooms. You can get kicked out at any time 
- **Dedicated Hosts:** We book an entire building of the resort
- **Capacity Reservations:** you book a room for a period with full price even if you don't stay in it 
