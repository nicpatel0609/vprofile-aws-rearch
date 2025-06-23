# vProfile – Re-Architected on AWS Cloud ☁️

**vProfile** is a demo multi-tier Java web application that was originally deployed on virtual machines using a traditional NGINX + Tomcat stack. This project showcases a complete re-architecture of that system onto AWS cloud infrastructure with production-grade scalability, availability, and observability.

---

## 🏗️ Legacy VM Architecture

Originally deployed on local VMs or a datacenter, vProfile followed a manual configuration model:

- Load Balancer: NGINX
- App Server: Apache Tomcat
- Caching: Memcached (dual-node)
- Database: MySQL Server
- Message Queue: RabbitMQ
- Deployment: Manual WAR deployment + NFS for shared storage

![Old Architecture](architecture/vm-architecture.png)

---

## ☁️ Modern AWS Architecture

The application is now hosted on a scalable AWS-native stack using managed services and Elastic Beanstalk:

- **Route 53** + **CloudFront** for global DNS and content delivery
- **Elastic Beanstalk** with **Auto Scaling** and **ALB**
- **Amazon RDS** (MySQL) for managed database
- **Amazon MQ** (ActiveMQ) for messaging
- **Amazon CloudWatch** for monitoring/logging
- **Amazon S3** for storing build artifacts

![New Architecture](architecture/aws-architecture.png)

---

## 🔄 Architectural Comparison

| Component       | VM-Based Stack                  | AWS Cloud Stack                        |
|----------------|----------------------------------|----------------------------------------|
| Load Balancer  | NGINX manually configured        | Application Load Balancer (ALB)        |
| App Server     | Apache Tomcat on VMs             | Elastic Beanstalk (auto scaling group) |
| Database       | MySQL on a VM                    | Amazon RDS (MySQL, Multi-AZ)           |
| Cache          | Memcached on VMs                 | Memcached (via AWS Elasticache or EC2) |
| Message Queue  | RabbitMQ                         | Amazon MQ (managed ActiveMQ)           |
| DNS/CDN        | Static IP / DNS                  | Route 53 + CloudFront                  |
| Logging        | Local syslog                     | Amazon CloudWatch                      |
| Storage        | NFS                              | Amazon S3 (for artifacts)              |
| Deployment     | Manual SSH & WAR copy            | Elastic Beanstalk auto-deploy          |

---

## ✅ Key Benefits After Migration

- **Scalability**: Elastic Beanstalk automatically scales application instances
- **High Availability**: ALB + Auto Scaling + Multi-AZ RDS
- **Operational Simplicity**: Managed services reduce ops overhead
- **Performance**: CloudFront + S3 improve asset delivery
- **Security**: IAM, VPC isolation, managed RDS/Amazon MQ
- **Cloud-Native**: Fully leverages AWS managed services stack

---

## 🚀 Future Enhancements

- [ ] Convert infrastructure to Terraform for full IaC
- [ ] Add CI/CD using GitHub Actions
- [ ] Use Elasticache for caching (instead of EC2-hosted Memcached)
- [ ] Integrate AWS X-Ray for application tracing

---
