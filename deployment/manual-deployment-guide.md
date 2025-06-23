# Manual Deployment Guide: vProfile on AWS

This guide outlines the manual steps taken to deploy the vProfile application to AWS without Infrastructure as Code (IaC).

---

## 1. 🌐 Domain + CDN Setup

### Route 53
- Registered or imported a domain
- Created a hosted zone and defined DNS records (A, CNAME)

### CloudFront
- Created a CloudFront distribution pointing to the Application Load Balancer (ALB)
- Enabled caching and SSL termination

---

## 2. 🚀 Application Hosting (Elastic Beanstalk)

### Environment Creation
- Created a new environment (Web Server) using the Elastic Beanstalk Console
- Selected Tomcat platform (Java)
- Configured instance type, key pair, instance profile, and VPC settings

### Artifact Deployment
- Uploaded `.war` file manually to Amazon S3
- Specified the S3 path in Elastic Beanstalk to deploy the application

### Auto Scaling
- Enabled auto scaling with min/max instance count
- Linked with ALB for load distribution

### Logs & Monitoring
- Enabled enhanced logging with Amazon CloudWatch
- Configured health checks and environment alerts

---

## 3. 💾 Database Setup (Amazon RDS)

- Launched a MySQL RDS instance
- Selected Multi-AZ for high availability
- Set up initial DB schema manually via SQL client
- Configured security groups to allow access from Beanstalk EC2 instances

---

## 4. 🏠 Messaging (Amazon MQ)

- Created an Amazon MQ (ActiveMQ) broker
- Configured security groups and user credentials
- Updated application properties to point to the broker endpoint

---

## 5. 📂 Storage (S3)

- Created a dedicated S3 bucket named `vprofile-artifacts`
- Uploaded WAR artifacts, logs, and backup files

---

## 6. 📊 Observability (CloudWatch)

- Configured log streaming from EC2 instances
- Set alarms for CPU, memory, and disk thresholds
- Created basic dashboards for application metrics

---

## 7. 🔒 Security Configuration

- Configured IAM roles for EC2 and Beanstalk environments
- Created security groups with strict ingress/egress rules
- Used SSL certificates on CloudFront for HTTPS traffic

---

## 📍 Notes

- All services were set up manually through AWS Management Console
- No automation or scripting (e.g., Terraform, CloudFormation) was used
- This is intended as a resume showcase project with room for future IaC automation

---

## 🚚 Next Steps

- Export current environment configuration as a `.json` for backup
- Plan migration to Terraform or CloudFormation for future automation
- Integrate with GitHub Actions or Jenkins for CI/CD
