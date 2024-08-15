We're getting AWS credentials soon!

---

**AWS** - Has physical datacenters that not only has a ton of storage, but loads of compute performance you can essentially rent out.

Region vs Availability Zone
 - Region: A geographic area where AWS has established data centers
 - AZ: A location within a region that houses AWS data centers
	 - Multiple can be placed within a region, so we have redundancy in the event of natural disasters, power failures, etc.

https://aws.amazon.com/about-aws/global-infrastructure/
Local Zone - We put them next to high-population density areas to load balance for low-latency purposes, like streaming, gaming, etc.
WaveLength Zone - Puts 5G connections nearby the datacenter to speed up connections to it?
^ These two will not be relevant, just fun to know. Don't need to study.

**Edge Location** - We don't want bob to have to reach across the ocean to use data on this specific S3 bucket.
![](../Images/Pasted%20image%2020240815103338.png)
Instead, we cache that data in the edge location near to him (the one directly above him).

**Serverless** - Abstracts away the server complexity, we just give it code to execute, and we're only billed when the code is executed.

**RESEARCH:**
**What is AWS's base website made in? React, etc? What is happening there?**

**OSM Model** - 7 Layers
*Top Layer*
7. Application Layer
	1. Website, user-facing stuff.
	2. HTTP is a common example protocol
		1. Header, body with content, etc.
6. Presentation Layer
	1. Encryption/Decryption
		1. Allowing/Disallowing someone to view content on a website
		2. SHA256
5. Session Layer
	1. Open a session - communication to endpoints
	2. Facilitates communication to our client and server
4. Transport Layer
	1. We decide what type of protocol to use, through what ports
	2. As for what port, **it depends**
		1. **EPort** - Ephemeral port - 1024-65,000ish?
	3. Common: TCP Handshake, using TCP Handshake
		1. If it fails, it'll try the handshake again
		2. After this, the data is sent, and has to be assembled - it may not be sent in order, but the packets will be numbered
	4. Data Frame:
		1. Preamble
		2. Ports
		3. Protocol
		4. Source/Destination, IP
		5. MAC
		6. Body
		7. CRC - Like a hash to ensure the data matches what we expect
	5. Also common: UDP - Fire and forget, the fastest communication. Just one line.
		1. VOIP, call/audio streaming - wherever speed is king and order might not matter
![](../Images/Pasted%20image%2020240815105919.png)
5. Network Layer
	1. Packets
	2. IP - IPv4/IPv6
6. Data Link Layer
	1. Data Frames
	2. MAC Address - globally unique address that every network card has
7. Physical Layer

With AWS, we have networks separated as VPCs - Virtual Private Cloud
![](../Images/Pasted%20image%2020240815113046.png)
Note that we have different availability zones throughout a region, but each AZ will have it's own subnet within the VPC.

`/24` - We can have up to 18 bits for the address - 2^18
(CHECK THIS)

Public vs Private Subnets
 - Are we allowing people outside our subnet to access addresses the subnet?
 - How can they communicate with one-another?

We use an Internet Gateway to allow our VPC to connect to the internet - using a Route Table (RT)
![](../Images/Pasted%20image%2020240815113925.png)

Note that for updates, each public area has a NAT that will give it a public IP address, which will then be used as one IP address that can access a specified IP - useful for things like APT updates, NPM packages, etc. This REQUIRES traffic to be initiated from the NAT network - you can't access it directly from the outside, only after the handshake.

Nothing really lives in the public subnets except load balancers, our apps will be inside the private subnets, and will access the network via the Internet Gateway.

---

Quick EC2 Demo

EC2 - Elastic Compute Cloud
 - Essentially just a computer in the cloud

You get to choose a name, an AMI (Machine Image)
 - Note the architecture you're on - we're usually developing on x86 instruction set, if you're on a M-series Mac that'll be ARM.

*A note on pricing for burstable class*
![](../Images/Pasted%20image%2020240815115152.png)
(I took a really bad screenshot and then he moved), but we have a set amount of credits that we can pull from. If we don't use a ton of performance, we accumulate credits - if we exceed it, we will pull from the credits.

Important: When we generate keys, choose `.pem`
![](../Images/Pasted%20image%2020240815115323.png)
Windows/Mac can use this via the terminal for SSH.

A security group is an instance-level firewall - you can manage inbound/outbound rules.

With storage, be careful - IOPS is EXPENSIVE, gp2/gp3 is available for the free tier.

IAM instance profiles allow you to manage resource permissions, like accessing an S3 bucket.

For user data, we'll add this:

```
#!/bin/bash

yum update -y

yum httpd -y
```
We're telling it to use bash, to update the OS, and to grab a simple HTTP server.

Go to the directory with our private key, and we can SSH into our EC2 with:
`ssh -i "<key>.pem" <whatever it is>.amazonaws.com`

---
*Back from lunch*

**Amazon S3**
Simple Storage Service
 - Object Storage
	 - Dynamically allocated - you access a pool of data without a set partition size.
 - Block Storage
	 - Can run out of space - you have to provision some amount of size.

We always want ACL to be disabled

When configuring public access, you may want to disable all public access at first, as that's a step we may want to do soon.

Versioning can be helpful, it's the first line of defense against accidental deletions. However, be careful of having too many versions, you may rack up storage space.

We can choose to encrypt data in a bucket by default, which can be done through managing the keys ourself, or by allowing Amazon to do it for us. The dual-layer is there for regulatory compliance, where some financial entities may need to encrypt twice.

**Durability:** Ensuring data is safe (won't be lost)
**Availability:** Ability to access data (can be read/wrote)

For best data durability, Amazon offers the ability to store data across 3 different availability zones - with this option, the data is replicated and synced in these 3 separate regions. If one is destroyed, there are two backups.

When you delete something in an S3 bucket, we still have it stored in a version. If we use the checkmark to delete, or delete the delete marker that stores the version, we *really* have deleted it then.

With S3 events, not only can we get notifications, but we can run a script when something happens.

CloudTrail is a logging service, so we can see what happened, who did it, and more.

With Transfer Acceleration, we're using Amazon's internal network for data transfers as well - not just the open internet. 

For our purposes, we're using the static website hosting feature of S3 - we can just build our React app, and place it into the storage area. We set the home address to index.html, the error to index.html as well, and we should be good to go.

To make sure someone can access something stored in S3, we need to ensure that AWS - which always errs on the side of caution when it comes to data access - has the knowledge that you're explicitly allowing the public internet to view our website. If we deny, or don't specify, it's denied. If we allow it explicitly, *then* the public can see the website.

To create the S3 policy for our website, we can use the policy generator. We want to allow everything in the bucket, and the bucket itself, so we can use the `*` character (and maybe `\*`), and we give it the resource. The policy JSON can then be used to set policy.

```
{
    "Version": "2012-10-17",
    "Id": "Policy1723743681098",
    "Statement": [
        {
            "Sid": "Stmt1723743679000",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": [
                "arn:aws:s3:::bjgomes-bucket-sdet",
                "arn:aws:s3:::bjgomes-bucket-sdet/*"
            ]
        }
    ]
}
```

For the different storage tiers, we are going to be using S3 standard - if we archive it, it's essentially just compressing it.

Tomorrow: Elastic Beanstalk!