# clinic-appointment-system
Flask-based clinic app for online booking, AWS-hosted with RDS, VPC, IAM, S3, ALB, Auto Scaling &amp; CloudWatch
# Clinic Appointment Web Application

A fully functional, scalable, and secure clinic appointment system built with Flask, hosted on AWS infrastructure.

## Project Overview

This project is a web-based clinic appointment booking system that allows users to book appointments, view staff schedules, and manage their data efficiently. The system features an intuitive interface, secure database management with AWS RDS, and deployment with AWS EC2, ALB, and Auto Scaling.

---

## Features

- User registration and appointment booking
- Staff management and schedule viewing
- Secure database connection with AWS RDS
- Static frontend hosted on AWS S3
- Load balancing with ALB for high availability
- Auto Scaling for managing load
- Backup and recovery systems using S3
- Monitoring and logging with CloudWatch

---

## Challenges and How I Overcame Them

### 1. Connecting Flask to AWS RDS
Initially, I faced issues with database connectivity, as errors like "unknown database" and connection failures appeared. The challenges stemmed from:

- Incorrect database endpoint or credentials
- Database not being correctly created or accessible
- Database permissions

**Solution:**  
I verified the RDS database exists via MySQL CLI, recreated the database when needed, and ensured the connection parameters (`host`, `user`, `password`, `dbname`) matched exactly. I also set security group rules to allow EC2 access.

---

### 2. Deployment Troubles 
Deploying Flask with Gunicorn on EC2 took multiple attempts, primarily due to misconfigurations in the environment variables and service setup.

**Solution:**  
 I configured environment variables carefully, tested locally with Flask debug mode, inspected logs (`journalctl`), and refined the service setup.

---

### 3. Ensuring System Resilience
Next, I set up Elastic IPs, Load Balancer (ALB), and Auto Scaling to ensure high availability in case of instance failure.

**Challenge:**  
Handling scaling and balancing loads, particularly with respect to SSL/TLS setup.

**Solution:**  
I integrated ALB with ACM for SSL certificates, created launch templates, and Auto Scaling groups, and monitored through CloudWatch.

---

### 4. Backup Strategy
To prevent data loss, I configured regular database dumps and backups of static assets on S3.  
**Challenge:**  
AWS CLI failed initially due to missing credentials.

**Solution:**  
I generated AWS IAM user access keys, configured CLI with `aws configure`, and set permissions for S3 buckets.

---

## Technologies Used

- **Backend:** Python, Flask
- **Database:** AWS RDS MySQL
- **Hosting:** EC2, Load Balancer, Auto Scaling Group
- **Static Hosting:** AWS S3
- **Monitoring:** AWS CloudWatch
- **Version Control:** Git & GitHub

## Deployment Steps (Overview)

1. Create and configure AWS Resources (EC2, RDS, S3, ALB, Auto Scaling)
2. Develop your Flask app locally
3. Configure environment variables and secrets securely
4. Upload static assets to S3
5. Deploy backend on EC2 or Lambda (optional)
6. Regularly backup database and assets to S3
7. Monitor with CloudWatch

---

## Getting Started

### Prerequisites

- AWS account with free tier enabled
- Git installed
- AWS CLI configured with credentials
- Python 3 environment

### Cloning & Running the Project

