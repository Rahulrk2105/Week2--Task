# 🚀 Week 2 Task – AWS 

## 📖 Project Overview

This project demonstrates the deployment of a complete AWS infrastructure environment using core AWS services.  
The objective of this task was to understand AWS networking fundamentals and deploy interconnected services in a structured and practical manner.

The infrastructure includes:

- Custom VPC
- Public Subnet
- Internet Gateway
- Route Table Configuration
- EC2 Instance (Amazon Linux)
- S3 Bucket (Static Website Hosting)
- VPC Endpoint (Gateway – S3)
- SQS Queue (Visibility Timeout: 90 seconds)

---

# 🏗️ Architecture Workflow

The deployment followed this logical sequence:

Network Setup → Compute Deployment → Storage Setup → Private Connectivity → Messaging Service → Static Website Hosting

---

# 📸 Step-by-Step Implementation

---

## 🥇 1. VPC Created

A custom Virtual Private Cloud (VPC) was created with CIDR block:

`10.0.0.0/16`

DNS resolution and DNS hostnames were enabled to allow internal communication within the VPC.

![VPC Created](screenshots/01-vpc-created.png)

---

## 🥈 2. Public Subnet Created

A public subnet was created inside the VPC with CIDR block:

`10.0.1.0/24`

Auto-assign public IPv4 was enabled to allow instances to receive a public IP automatically.

![Subnet Created](screenshots/02-subnet-created.png)

---

## 🥉 3. Internet Gateway Attached

An Internet Gateway (IGW) was created and attached to the VPC to enable outbound internet connectivity.

Without the IGW, instances inside the VPC cannot access external networks.

![Internet Gateway](screenshots/03-internet-gateway-attached.png)

---

## 4. Route Table Configured

The route table associated with the subnet was updated with:

- `10.0.0.0/16 → local`
- `0.0.0.0/0 → Internet Gateway`

This ensures that internet-bound traffic is routed correctly.

![Route Table](screenshots/04-route-table-configured.png)

---

## 5. EC2 Instance Launched

An EC2 instance (Amazon Linux, t2.micro) was launched inside the public subnet.

Security group rules allowed:
- SSH (Port 22)
- HTTP (Port 80)

A public IPv4 address was assigned for external access.

![EC2 Running](screenshots/05-ec2-instance-running.png)

---

## 6. Internet Connectivity Verified

Internet connectivity was verified by connecting to the EC2 instance and running:

```
ping google.com
```

Successful responses confirmed correct network configuration.

![Internet Test](screenshots/06-ec2-internet-test.png)

---

## 7. S3 Bucket Created

An Amazon S3 bucket was created in the same region to host a static website.

![S3 Bucket](screenshots/07-s3-bucket-created.png)

---

## 8. Files Uploaded to S3

The following files were uploaded:

- `index.html`
- `sample.txt`

Static website hosting was enabled in bucket properties.

![Files Uploaded](screenshots/08-s3-bucket-files-upload.png)

---

## 9. VPC Endpoint Created (Gateway Type – S3)

A Gateway-type VPC Endpoint for Amazon S3 was created and associated with the route table.

This allows private communication between the VPC and S3 without using the public internet.

![VPC Endpoint](screenshots/09-vpc-endpoint.png)

---

## 10. SQS Queue Created

An Amazon SQS Standard Queue was created with:

Visibility Timeout: **90 seconds**

Test messages were successfully sent and received.

![SQS Created](screenshots/10-sqs-created.png)

---

## 11. S3 Bucket Policy Configured

A bucket policy was added to allow public read access to objects in the bucket:

```json
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::bucket-name/*"
}
```

This enabled public access for static website hosting.

![Bucket Policy](screenshots/11-s3-bucket-policy.png)

---

## 12. Static Website Successfully Hosted

The static website was accessed using the S3 website endpoint URL.

This confirms:
- Correct bucket configuration
- Proper policy setup
- Successful file upload

![Static Website Output](screenshots/12-static-website-output.png)

---

# 🧪 Validation & Testing

✔ EC2 successfully connected to the internet  
✔ Static website hosted and accessible  
✔ SQS queue tested successfully  
✔ VPC endpoint created and available  
✔ Networking components properly configured  

---

# 🛠️ AWS Services Used

| Service | Purpose |
|----------|----------|
| Amazon VPC | Custom network creation |
| Subnet | Resource segmentation |
| Internet Gateway | Internet access |
| Route Table | Traffic routing |
| Amazon EC2 | Compute service |
| Amazon S3 | Object storage & website hosting |
| Amazon SQS | Message queuing |
| VPC Endpoint | Private S3 connectivity |

---

# 🎯 Key Learning Outcomes

- Understood AWS networking architecture
- Configured public subnet with internet access
- Launched and secured EC2 instance
- Hosted static website using S3
- Implemented SQS messaging service
- Created and configured VPC endpoint
- Managed bucket policies and security rules

---

# 👨‍💻 Author

Rahul RK  
Aspiring Cloud / System Engineer
