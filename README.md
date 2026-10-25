# AWS VPC Peering Project - EWB Tech Academy

## 👤 Student Details
- **Name:** M Swarna Lakshmi
- **Department:** Computer Science and Engineering
- **Institution:** SJC Institute of Technology
- **Region:** Mumbai (`ap-south-1`)

---

## 🏗️ Project Architecture Overview
This project demonstrates secure cross-VPC communication using **AWS VPC Peering**. 
- **VPC A (`10.10.0.0/16`)**: Contains a public subnet (`ewb-a-public`) with a Bastion Host (`ewb-bastion`) and a private subnet (`ewb-a-private`) hosting `ewb-app-a`.
- **VPC B (`10.20.0.0/16`)**: Contains a private subnet (`ewb-b-private`) hosting `ewb-app-b`.
- **Peering Connection (`ewb-a-b-peer`)**: Connects VPC A and VPC B, allowing private traffic routing via custom route table updates.

---

## 📊 Resource Inventory
| Resource Type | Resource Name | IP Address / CIDR | VPC / Subnet |
| :--- | :--- | :--- | :--- |
| **VPC A** | `ewb-vpc-a` | `10.10.0.0/16` | - |
| **VPC B** | `ewb-vpc-b` | `10.20.0.0/16` | - |
| **Public Subnet** | `ewb-a-public` | `10.10.1.0/24` | `ewb-vpc-a` |
| **Private Subnet A** | `ewb-a-private` | `10.10.2.0/24` | `ewb-vpc-a` |
| **Private Subnet B** | `ewb-b-private` | `10.20.1.0/24` | `ewb-vpc-b` |
| **Bastion Instance** | `ewb-bastion` | Public IP / `10.10.1.10` | `ewb-a-public` |
| **App Instance A** | `ewb-app-a` | `10.10.2.10` (Private) | `ewb-a-private` |
| **App Instance B** | `ewb-app-b` | `10.20.1.10` (Private) | `ewb-b-private` |
| **VPC Peering** | `ewb-a-b-peer` | `pcx-0f0d76bc8799945b3` | VPC A ⟷ VPC B |

---

* Comprehensive project report available under the /report/ directory: Swarna_EWB_VPC_Peering.pdf
