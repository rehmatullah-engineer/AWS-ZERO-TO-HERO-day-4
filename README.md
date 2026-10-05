AWS EC2 Instances — Day 4

AWS Hands-On Notes: EC2 from Zero to Hero — Build, Launch, Connect, and Manage

📌 Topics Covered

Amazon EC2 fundamentals

Launching an EC2 instance

AMI (Amazon Machine Image)

Key pairs

Instance types

Network / VPC / Subnet

Public IP

EBS storage

Security Groups

On-Demand vs Spot Instances

Instance Templates / Launch Templates

SSH / RDP connection

Basic EC2 best practices

☁️ 1. What is Amazon EC2?

Amazon EC2 (Elastic Compute Cloud) provides virtual servers (instances) in AWS.

You can use EC2 to:

Run applications and websites

Host APIs and backend services

Deploy development environments

Scale compute resources

Choose different operating systems and hardware sizes

Key Benefits

Flexible and scalable

Pay for what you use

Multiple instance types and operating systems

Integrates with other AWS services

🚀 2. How to Launch an EC2 Instance

Basic launch flow:

Open AWS Console → EC2 → Launch Instance

Select an AMI

Select an Instance Type

Configure Network / VPC / Subnet

Configure Storage (EBS)

Add Tags if required

Configure a Security Group

Review the configuration

Launch the instance

Connect using SSH (Linux) or RDP (Windows)

🖥️ 3. AMI — Amazon Machine Image

An AMI is a pre-configured template used to create an EC2 instance.

It can contain:

Operating system

Software

Configuration

Storage settings

Common AMIs

AMI

Common Use

Amazon Linux

AWS-optimized Linux

Ubuntu

Developer-friendly Linux

Windows Server

Windows applications / GUI

Red Hat

Enterprise workloads

🔑 4. Key Pair

A key pair is used to securely connect to an EC2 instance.

For Linux:

ssh -i my-key.pem ec2-user@<public-ip>

For Ubuntu:

ssh -i my-key.pem ubuntu@<public-ip>

Important: Keep the .pem private key secure. Do not upload it to GitHub.

⚙️ 5. Instance Type

The instance type determines the compute resources available to your server.

It affects:

vCPU

Memory (RAM)

Network performance

Cost

Workload suitability

Examples

Instance

Example Use

t2.micro

Free-tier/testing eligible where available

t3.micro

Small development workloads

t3.small

Small applications

m5.large

General-purpose workloads

c5.large

Compute-intensive workloads

Instance availability, pricing, and free-tier eligibility can vary by AWS Region and account.

🌐 6. Network Configuration

During EC2 launch, common network settings include:

VPC

Your isolated virtual network in AWS.

Subnet

A smaller network range inside a VPC.

Public IP

Allows an instance to communicate with the public internet when the network configuration permits it.

Security Group

Acts as a virtual firewall controlling inbound and outbound traffic.

Example inbound rules:

Protocol

Port

Purpose

SSH

22

Linux administration

HTTP

80

Web traffic

HTTPS

443

Secure web traffic

RDP

3389

Windows Remote Desktop

Best practice: Avoid opening administration ports such as SSH/RDP to 0.0.0.0/0 unless there is a specific reason. Prefer your own IP or a controlled network.

💾 7. EBS Storage

Amazon EBS (Elastic Block Store) provides persistent block storage for EC2.

Common volume types:

Type

Typical Use

gp3

General-purpose workloads

io1/io2

High-IOPS workloads such as demanding databases

st1

Throughput-oriented workloads

sc1

Infrequent-access / cold workloads

A common beginner configuration is an 8 GiB gp3 root volume, depending on the OS and workload.

🏷️ 8. Tags

Tags are key-value labels used to organize and identify AWS resources.

Example:

Key: Name
Value: My-Web-Server

Useful tags:

Environment = Development
Project     = AWS-Learning
Owner       = Rehmat

Tags help with organization, cost tracking, searching, and automation.

🔐 9. Security Group

A Security Group controls network traffic to and from an EC2 instance.

Example development web server:

SSH    → TCP 22  → My IP
HTTP   → TCP 80  → 0.0.0.0/0
HTTPS  → TCP 443 → 0.0.0.0/0

Only open the ports your application actually needs.

💰 10. On-Demand vs Spot Instances

Feature

On-Demand

Spot

Cost

Higher

Often much cheaper

Availability

No spare-capacity dependency

Depends on spare AWS capacity

Termination

You control termination

AWS can interrupt the instance

Best For

Stable workloads

Fault-tolerant / flexible workloads

On-Demand

Good for:

Development

Production applications

Predictable workloads

Workloads that cannot tolerate interruption

Spot

Good for:

Batch processing

Testing

Big-data jobs

Flexible workloads

Fault-tolerant applications

Key idea: Spot instances can be interrupted, so applications should be designed to handle interruptions.

📋 11. Instance / Launch Template

A Launch Template stores reusable EC2 configuration such as:

AMI

Instance type

Key pair

Security groups

Network settings

Storage

Tags

Why use it?

Consistent instance configuration

Faster launches

Useful with Auto Scaling

Reduces configuration mistakes

Helps maintain standardized infrastructure

🔌 12. Connect to an EC2 Instance

Linux — SSH

ssh -i my-key.pem ubuntu@<public-ip>

or:

ssh -i my-key.pem ec2-user@<public-ip>

Windows

Use RDP (Remote Desktop Protocol) with the appropriate Windows administrator credentials.

🧪 13. Beginner Hands-On Practice

Task 1 — Launch On-Demand EC2

Create a small EC2 instance using:

AMI:          Amazon Linux or Ubuntu
Instance:     Small/general-purpose type
Network:      Default VPC or your practice VPC
Public IP:    Enabled when required
Storage:      gp3
Security:     SSH from your IP

Then connect through SSH.

Task 2 — Explore the Instance

Check:

whoami

hostname

df -h

free -h

uptime

Task 3 — Explore Spot

Launch a Spot instance for a non-critical test workload and understand that it may be interrupted.

Task 4 — Create a Launch Template

Save your common:

AMI + Instance Type + Key Pair + Security Group + Storage

configuration as a reusable Launch Template.

🧠 Quick Revision

EC2       → Virtual server
AMI       → Server/OS template
Key Pair  → Secure login credentials
Instance  → Running virtual server
VPC       → Isolated AWS network
Subnet    → Network segment inside VPC
SG        → Virtual firewall
EBS       → Persistent block storage
On-Demand → Flexible, non-interruptible pricing model
Spot      → Cheaper, interruptible compute
Launch Template → Reusable EC2 configuration

✅ Day 4 Takeaways

EC2 provides virtual servers in AWS.

AMI defines the starting OS/software image.

Instance type defines compute capacity.

VPC and Subnet define network placement.

Security Groups control network access.

EBS provides persistent storage.

Key pairs enable secure instance access.

On-Demand is suitable for predictable workloads.

Spot is cost-effective for interruptible workloads.

Launch Templates make EC2 deployments consistent and repeatable.

📚 Day 4 Learning Goal

By the end of this practice, you should be able to:

Explain EC2 in simple terms

Launch an EC2 instance from an AMI

Select an appropriate instance type

Configure basic networking

Attach and understand EBS storage

Configure a Security Group

Connect to Linux EC2 using SSH

Understand On-Demand vs Spot

Create and understand a Launch Template

AWS Learning Series — Day 4 🚀
