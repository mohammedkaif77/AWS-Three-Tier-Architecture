
# AWS Three-Tier Web Application

## 📌 Project Overview

Designed and deployed a secure **Three-Tier Web Application Architecture on AWS**, separating the infrastructure into Web, Application, and Database layers.

The project demonstrates practical implementation of AWS networking, EC2, Application Load Balancer, Amazon RDS, Security Groups, Nginx, Python, and private subnet communication.

## 🏗️ Architecture

```text
                         Internet
                            |
                            v
                    Internet Gateway
                            |
                            v
                Application Load Balancer
                            |
             +--------------+--------------+
             |                             |
             v                             v
        Web Server 1                 Web Server 2
        EC2 - Public                EC2 - Public
        us-east-1a                  us-east-1b
             |                             |
             v                             v
        App Server 1                 App Server 2
        EC2 - Private                EC2 - Private
        us-east-1a                  us-east-1b
             \                             /
              \                           /
               +-----------+-------------+
                           |
                           v
                    Amazon RDS MySQL
                       Private DB
````

## 🔹 Web Tier

* 2 Ubuntu EC2 instances
* Deployed across two Availability Zones
* Public subnets
* Nginx configured as a reverse proxy
* Application Load Balancer distributes incoming HTTP traffic

## 🔹 Application Tier

* 2 Ubuntu EC2 instances
* Deployed across two Availability Zones
* Private subnets
* Python-based application
* Application runs on TCP port `5000`
* Managed using Linux `systemd`

## 🔹 Database Tier

* Amazon RDS MySQL
* Single-AZ deployment
* Private database subnet
* MySQL communication on port `3306`
* Shared database accessed by both application servers

## 🔐 Security & Networking

* Custom AWS VPC: `10.0.0.0/16`
* Public and private subnets
* Internet Gateway for public-tier connectivity
* Security Groups controlling communication between tiers
* Application and Database tiers do not have direct Internet access
* S3 Gateway VPC Endpoint for private S3 connectivity
* No NAT Gateway used

### Security Group Flow

```text
Internet
   |
   | HTTP :80
   v
SG-ALB
   |
   | HTTP :80
   v
SG-WEB
   |
   | TCP :5000
   v
SG-APP
   |
   | MySQL :3306
   v
SG-DB
```

## 🛠️ Tech Stack

| Category           | Technologies                                        |
| ------------------ | --------------------------------------------------- |
| Cloud              | AWS                                                 |
| Compute            | Amazon EC2                                          |
| Networking         | Amazon VPC, Subnets, Route Tables, Internet Gateway |
| Load Balancing     | Application Load Balancer                           |
| Database           | Amazon RDS MySQL                                    |
| Web Server         | Nginx                                               |
| Application        | Python                                              |
| Operating System   | Ubuntu Linux                                        |
| Security           | AWS Security Groups                                 |
| VPC Endpoint       | S3 Gateway VPC Endpoint                             |
| Service Management | Linux systemd                                       |

## 🧪 Testing & Validation

The complete application flow was tested through the Application Load Balancer:

```text
Internet
   ↓
ALB
   ↓
Web Server
   ↓
Application Server
   ↓
RDS MySQL
```

End-to-end testing confirmed that requests reached both application servers and successfully retrieved data from the shared RDS MySQL database.

## 📚 Key Learnings

* AWS VPC and subnet design
* Public vs private subnet architecture
* Application Load Balancer configuration
* EC2 networking and security
* Security Group-based access control
* Nginx reverse proxy configuration
* Python application deployment
* RDS MySQL connectivity
* Linux systemd service management
* Troubleshooting private-tier connectivity
* S3 Gateway VPC Endpoint
* Three-tier cloud architecture

## 📂 Project Contents

```text
├── README.md
├── architecture/
│   └── aws-three-tier-architecture.drawio
├── application/
│   └── app.py
├── nginx/
│   └── nginx.conf
├── systemd/
│   └── app.service
└── screenshots/
    ├── vpc-resource-map.png
    ├── alb-target-group.png
    ├── ec2-instances.png
    ├── rds-mysql.png
    └── end-to-end-test.png
```

## 👨‍💻 Author

**Mohammed Kaif**

Cloud & DevOps | AWS | Linux | Docker | Kubernetes | Terraform | Jenkins
