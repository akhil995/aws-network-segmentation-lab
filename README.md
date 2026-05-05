# AWS Network Segmentation Lab

## 📌 Overview
This project demonstrates how to implement **network segmentation in AWS** using:
- Security Groups (stateful)
- Network ACLs (stateless)

The goal was to restrict traffic flow between layers of a **multi-tier architecture**:
- Bastion Host
- Application Load Balancer (ALB)
- Application Servers
- RDS Database

---

## 🏗️ Architecture
3-tier architecture:

- **DMZ Layer**
  - Bastion Host (SSH access)
  - ALB (HTTP/HTTPS)

- **Application Layer**
  - EC2 App Servers (only accessible via ALB)

- **Database Layer**
  - RDS (only accessible from App Servers)

---

## 🔐 Security Groups Configuration

### Bastion SG
- SSH (22) → Anywhere

### ALB SG
- HTTP (80) → Anywhere
- HTTPS (443) → Anywhere

### App Server SG
- HTTP (80) → ALB SG
- SSH (22) → Bastion SG

### RDS SG
- MySQL (3306) → App Server SG

---

## 🌐 Network ACL Configuration

### DMZ Layer
Inbound:
- 22, 80, 443 → Allow
- Ephemeral ports → Allow

Outbound:
- 22, 80, 443 → Allow
- Ephemeral ports → Allow

---

### App Layer
Inbound:
- 80 → Allow
- Ephemeral → Allow

Outbound:
- 80 → Allow
- Ephemeral → Allow

---

### DB Layer
Inbound:
- 3306 → Allow
- Ephemeral → Allow

Outbound:
- 3306 → Allow
- Ephemeral → Allow

---

## 🔍 Key Learnings
- Difference between **stateful vs stateless security**
- How to design **least-privilege network access**
- Importance of **layer isolation in cloud architectures**
- Practical implementation of **defense-in-depth**

---

## ⚠️ Improvements (Real-world perspective)
- Restrict SSH to specific IP instead of 0.0.0.0/0
- Tighten NACL rules (avoid open access)
- Use Private Subnets for DB layer
- Add NAT Gateway for controlled outbound traffic

---

## 📷 Screenshots
attached in the repository

---

## 🚀 Outcome
Successfully implemented secure communication between layers while minimizing unnecessary exposure.

