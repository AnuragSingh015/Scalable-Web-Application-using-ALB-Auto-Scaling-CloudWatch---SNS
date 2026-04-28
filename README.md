# Project: Scalable Web Application using ALB, Auto Scaling, CloudWatch & SNS 

## Overview

This project demonstrates a scalable web application architecture on AWS using **EC2, Application Load Balancer (ALB), Auto Scaling Group (ASG), CloudWatch, and SNS**. The system automatically **scales out (adds instances)** when CPU utilization increases and **scales in (removes instances)** when traffic decreases.

**Amazon CloudWatch** monitors CPU utilization of EC2 instances and triggers scaling policies in the Auto Scaling Group. **Amazon SNS (Simple Notification Service)** sends email notifications whenever scaling events occur.

Traffic was generated using **Apache Benchmark (`ab`)** from a **separate EC2 instance** to simulate real user traffic hitting the Application Load Balancer.

---

## Architecture

![Architecture Diagram](images/SWA.png)

### Components

* **Application Load Balancer (ALB)** – Distributes incoming HTTP traffic.
* **Target Group** – Routes requests to registered EC2 instances.
* **Auto Scaling Group (ASG)** – Automatically adjusts the number of EC2 instances.
* **Launch Template** – Defines EC2 instance configuration.
* **CloudWatch** – Monitors CPU utilization and triggers scaling policies.
* **SNS Email Notification** – Sends alerts when scaling events occur.
* **Traffic Generator EC2** – Used to generate load using Apache Benchmark.

---

## Scaling Process

### Scale Out (Increase Instances)

When CPU utilization exceeds the defined threshold, the Auto Scaling Group launches additional EC2 instances.

![Scale Out Email Notification](images/ScaleOut.png)

---

### Scale In (Decrease Instances)

When CPU utilization drops below the threshold, the Auto Scaling Group terminates unnecessary instances.

![Scale In Email Notification](images/ScaleIn.png)

---

## Traffic Generation

Load testing was performed using Apache Benchmark from a separate EC2 instance:

```bash
ab -n 100000 -c 200 http://<ALB-DNS-NAME>/
```

This generated high traffic to increase CPU utilization and trigger Auto Scaling events.

---

## Result

* Automatic **scale-out** when traffic increased.
* Automatic **scale-in** when traffic decreased.
* Email notifications received for both scaling events.

---

## Conclusion

This project demonstrates how AWS services can be integrated to build a **highly available, scalable, and monitored web architecture** that automatically adapts to changing traffic conditions.
