# Cloud Security (D7078E) LAB 1: AWS Fundamentals 
**Authors:** Ivana Pristavnik, Sebastian Ringström, Nenad Sekulic  
**Date:** 21 November 2025 

## 1. Introduction
This lab documents the exploration of the AWS Console with a focus on EC2 and IAM documentation[cite: 19, 20]. The primary goal was to create security groups, deploy EC2 instances, configure EBS volumes, and utilize AMIs to showcase various cloud functionalities.

**IAM:** A framework providing authentication, authorization, and access management.
**EC2:** AWS service providing scalable computing capability designed for cost efficiency.

---

## 2. Step-by-Step Lab Execution

### 2.1 Security Group Configuration
Security groups act as a virtual firewall for resources. We created a group following the naming pattern `SEC_D7078E_ivpri`.
**Inbound Rules:** SSH and HTTP rules were set for all locations.
**Outbound Rules:** Open by default to allow all egress traffic.

![Figure 1: Security group creation](images/fig1_security_group.png)
*Figure 1: Security group creation*

### 2.2 EC2 and EBS Setup
We provisioned an EC2 instance with the following specifications:
**AMI:** Ubuntu 24.04 (Free-tier eligible).
**Instance Type:** `t3.small` (General purpose).
**Storage:** EBS volume created with "delete on termination" disabled.
**Access:** Assigned a custom key pair and associated with our previously created security group.

![Figure 2: Instance summary](images/fig2_instance_summary.png)
*Figure 2: Summary for the created EC2 instance *

### 2.3 Installing Apache Web Server
After connecting to the instance, we installed and customized the Apache2 server:

1. Elevate to root: `sudo -i` 
2. Update packages: `apt-get update` 
3. Install Apache: `apt-get install apache2` 

![Figure 4: Default Apache Page](images/fig4_apache_default.png)
*Figure 4: Default HTML page via Public DNS *

We modified the `index.html` file located in `/var/www/html` using `vim` to verify live updates.

![Figure 5: Edited HTML Page](images/fig5_apache_edited.png)
*Figure 5: Edited HTML page showing custom lab text*

### 2.4 Testing "Launch More Like This"
We created a new instance using the 'launch more like this' option. 
**Result:** No server response when navigating to the Public DNS.
**Observation:** This occurs because the new instance uses a separate EBS volume and lacks the Apache installation present on the original instance.

### 2.5 AMI Creation and Persistence
To standardize the environment, we created an **AMI (Amazon Machine Image)** from our original instance.

![Figure 7: Created AMI](images/fig7_ami_creation.png)
*Figure 7: Custom AMI includes root volume templates and software*

When launching a new instance from this custom AMI, the software and edited `index.html` were immediately available.

---

## 3. Conclusion
Custom AMIs are powerful tools for organizations to enforce security baselines and standardize developer environments. By pre-configuring security agents, patches, and access controls within an image, an organization significantly reduces risk in dynamic environments.


---

## 4. Appendix & Resources
**Command Reference:** For a quick-reference list of all terminal commands used in this lab, see [commands.txt](./scripts/commands.txt). 
**EC2 Details:** Detailed instance summaries, including attached EBS volumes and security group rules, are documented in the appendix of the full lab report. 