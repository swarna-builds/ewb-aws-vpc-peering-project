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

## 2. Subnet CIDRs and Route Table Associations
* **VPC A Private Route Table (`rtb-vpcA-private`):** Associated with VPC A private subnets. Includes static route `10.20.0.0/16` pointing to peering connection `pcx-0f0d76bc8799945b3`.
* **VPC B Private Route Table (`rtb-vpcB-private`):** Associated with VPC B private subnets. Includes static route `10.10.0.0/16` pointing to peering connection `pcx-0f0d76bc8799945b3`.
* **VPC A Public Route Table (`rtb-vpcA-public`):** Associated with public subnet containing the Bastion host, routing `0.0.0.0/0` via Internet Gateway.

---

## 3. Verification, Testing Evidence & Rubric Requirements
* **Baseline Failure:** Initial ping from App-A (`10.10.2.10`) to App-B (`10.20.1.10`) failed due to missing cross-VPC route entries.
* **Forward & Reverse Ping Success:** Post-routing configuration, continuous ping tests confirmed **0% packet loss** in both directions (App-A $\rightarrow$ App-B and App-B $\rightarrow$ App-A).
* **App-B SSH Proof:** Verified secure administrative access via SSH ProxyJump (`ssh -J ec2-user@10.10.1.10 ec2-user@10.20.1.10`).
* **Controlled ICMP Failure & Recovery:** Temporarily removing the return route in VPC B caused request timeouts; re-adding the route instantly restored connectivity.

---

## 4. Cleanup & Key Learnings
* **Cleanup Note:** Peering connection, route tables, and test instances were properly terminated post-validation following cloud hygiene best practices.
* **Key Learnings:** Gained deep proficiency in AWS networking, VPC peering non-transitive nature, route propagation, and secure tunneling.
