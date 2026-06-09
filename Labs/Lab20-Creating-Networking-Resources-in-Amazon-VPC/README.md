# Lab 20 — Creating Networking Resources in an Amazon VPC

| | |
|---|---|
| **Programme** | Praesignis AWS re/Start |
| **Date Completed** | 2026-06-08 |
| **Lab Topic** | Building a fully routable VPC with IGW, Route Table, NACL, Security Group, and EC2 |

---

## ✏️ What This Lab Covered

This lab was based on a customer support scenario. A customer named Brock, a startup owner, had previously set up a VPC but could not ping outside of it — meaning his VPC had no internet connectivity. The task was to build all the necessary networking resources from scratch to make the VPC fully routable to the internet and validate connectivity using the `ping` command.

Key activities completed:

- Created a VPC named `Test VPC` with CIDR block `192.168.0.0/18`
- Created a public subnet named `Public subnet` with CIDR `192.168.1.0/26` inside the Test VPC
- Created a Route Table named `Public route table` and associated it with the Test VPC
- Created an Internet Gateway named `IGW Test VPC` and attached it to the Test VPC
- Added a route `0.0.0.0/0 → IGW Test VPC` to the Public route table to enable internet traffic
- Associated the Public subnet with the Public route table
- Created a Network ACL named `Public Subnet NACL` with inbound and outbound rules allowing all traffic (Rule 100)
- Created a Security Group named `Public security group` with inbound rules allowing SSH, HTTP, and HTTPS from anywhere
- Launched an EC2 instance (Amazon Linux 2023, t3.micro) in the Public subnet with the Public security group
- SSH'd into the instance and ran `ping google.com` — confirming successful internet connectivity with 0% packet loss

---

## 📸 Screenshots and Explanations

### 1. VPC Dashboard
![VPC Dashboard](screenshots/Screenshot_2026-06-08_at_13_07_41.png)

The Amazon VPC dashboard showing existing resources in the Oregon (us-west-2) region. This is the starting point for building all networking resources for Brock's VPC.

---

### 2. Create VPC — Test VPC Configuration
![Create VPC form with Test VPC and 192.168.0.0/18](screenshots/Screenshot_2026-06-08_at_13_08_11.png)

The Create VPC form configured with VPC only selected, name tag Test VPC, and IPv4 CIDR block 192.168.0.0/18. No IPv6 block is added and tenancy is set to Default.

---

### 3. Test VPC Created Successfully
![Test VPC created](screenshots/Screenshot_2026-06-08_at_13_09_00.png)

The green banner confirms that Test VPC (vpc-0ec4a84e171a33398) was successfully created with CIDR 192.168.0.0/18 and is showing as Available.

---

### 4. Create Subnet — Public Subnet Configuration
![Create Subnet form](screenshots/Screenshot_2026-06-08_at_13_09_27.png)

The Create Subnet form configured with VPC set to Test VPC, subnet name Public subnet, Availability Zone set to No Preference, and IPv4 CIDR block 192.168.1.0/26.

---

### 5. Public Subnet Created Successfully
![Public subnet created](screenshots/Screenshot_2026-06-08_at_13_09_47.png)

The green banner confirms that Public subnet (subnet-02f8c2d9ce45d3e02) was successfully created and is showing as Available within the Test VPC.

---

### 6. Create Route Table — Public Route Table
![Create Route Table form](screenshots/Screenshot_2026-06-08_at_13_10_39.png)

The Create Route Table form configured with name Public route table and VPC set to Test VPC. This route table will control how traffic is routed within the subnet.

---

### 7. Route Table Created Successfully
![Route table created with local route](screenshots/Screenshot_2026-06-08_at_13_12_05.png)

The Public route table (rtb-01422bb58a373c130) was created successfully. It shows the default local route 192.168.0.0/18 to local which handles internal VPC traffic.

---

### 8. Create Internet Gateway
![Create Internet Gateway form](screenshots/Screenshot_2026-06-08_at_13_13_08.png)

The Create Internet Gateway form configured with name tag IGW Test VPC. An Internet Gateway is required to allow the VPC to communicate with the internet.

---

### 9. Internet Gateway Created Successfully
![IGW created](screenshots/Screenshot_2026-06-08_at_13_13_30.png)

The green banner confirms that IGW Test VPC (igw-075ca556bfcdb2665) was created successfully. The state shows Detached — it still needs to be attached to the VPC.

---

### 10. Attach Internet Gateway to VPC
![Attach IGW to Test VPC](screenshots/Screenshot_2026-06-08_at_13_13_58.png)

The Attach to VPC form with Test VPC selected. Attaching the IGW to the VPC enables the VPC to route traffic to and from the internet.

---

### 11. Internet Gateway Attached Successfully
![IGW attached to Test VPC](screenshots/Screenshot_2026-06-08_at_13_14_10.png)

The green banner confirms that IGW Test VPC has been successfully attached to the Test VPC. The state now shows Attached and the VPC ID is linked.

---

### 12. Edit Routes — Adding IGW Route
![Edit routes with 0.0.0.0/0 to IGW](screenshots/Screenshot_2026-06-08_at_13_18_14.png)

The Edit Routes page showing the new route being added: destination 0.0.0.0/0 targeting IGW Test VPC. This tells the route table that any traffic destined for the internet should be sent through the Internet Gateway.

---

### 13. Routes Updated Successfully
![Routes showing local and IGW routes](screenshots/Screenshot_2026-06-08_at_13_17_00.png)

The Public route table now shows two routes: the local route 192.168.0.0/18 to local for internal VPC traffic, and the internet route 0.0.0.0/0 to igw-075ca556bfcdb2665 for external traffic. Both are Active.

---

### 14. Edit Subnet Associations — Linking Public Subnet
![Edit subnet associations](screenshots/Screenshot_2026-06-08_at_13_16_49.png)

The Edit Subnet Associations page showing the Public subnet (192.168.1.0/26) selected and ready to be associated with the Public route table.

---

### 15. Subnet Association Saved Successfully
![Subnet associated to route table](screenshots/Screenshot_2026-06-08_at_13_15_09.png)

The green banner confirms the subnet association was updated successfully. The Public subnet is now explicitly associated with the Public route table.

---

### 16. Create Network ACL
![Create Network ACL form](screenshots/Screenshot_2026-06-08_at_13_19_12.png)

The Create Network ACL form configured with name Public Subnet NACL and VPC set to Test VPC. A NACL acts as a stateless firewall at the subnet level.

---

### 17. Network ACL Created Successfully
![NACL created](screenshots/Screenshot_2026-06-08_at_13_19_23.png)

The green banner confirms that Public Subnet NACL was successfully created and is listed in the Network ACLs console under the Test VPC.

---

### 18. Edit NACL Inbound Rules
![NACL inbound rule 100 all traffic](screenshots/Screenshot_2026-06-08_at_13_21_18.png)

The Edit Inbound Rules page with Rule 100 configured to allow all traffic from any source (0.0.0.0/0). The asterisk rule below denies everything else by default.

---

### 19. NACL Inbound Rules Saved
![NACL inbound rules saved](screenshots/Screenshot_2026-06-08_at_13_21_56.png)

The inbound rules were saved successfully. Rule 100 allows all traffic inbound, and the default deny rule blocks anything that does not match.

---

### 20. Edit NACL Outbound Rules
![NACL outbound rule 100 all traffic](screenshots/Screenshot_2026-06-08_at_13_22_18.png)

The Edit Outbound Rules page with Rule 100 configured to allow all traffic to any destination (0.0.0.0/0).

---

### 21. NACL Outbound Rules Saved
![NACL outbound rules saved](screenshots/Screenshot_2026-06-08_at_13_26_04.png)

The outbound rules were saved successfully. Both inbound and outbound Rule 100 are now in place allowing all traffic through the subnet-level firewall.

---

### 22. Create Security Group — Public Security Group
![Create Security Group form with SSH HTTP HTTPS rules](screenshots/Screenshot_2026-06-08_at_13_26_29.png)

The Create Security Group form configured with name Public security group, description Allows public access, VPC set to Test VPC, and three inbound rules: SSH (port 22), HTTP (port 80), and HTTPS (port 443) — all from anywhere (0.0.0.0/0).

---

### 23. Security Group Created Successfully
![Security group created](screenshots/Screenshot_2026-06-08_at_13_28_37.png)

The green banner confirms that Public security group was created successfully with 3 inbound permission entries (SSH, HTTP, HTTPS) and 1 outbound entry (all traffic).

---

### 24. EC2 Network Settings — Test VPC and Public Security Group
![EC2 network settings](screenshots/Screenshot_2026-06-08_at_13_28_59.png)

The EC2 Launch Instance network settings showing the instance placed in Test VPC, Public subnet (192.168.1.0/26), auto-assign public IP enabled, and Public security group selected.

---

### 25. EC2 Instance Launched Successfully
![EC2 instance launched](screenshots/Screenshot_2026-06-08_at_13_31_41.png)

The green banner confirms that instance i-02fcd534edc2a7f8d was successfully launched. This is the instance used to test internet connectivity.

---

### 26. SSH Connected to EC2 Instance
![SSH terminal showing Amazon Linux 2023 prompt](screenshots/Screenshot_2026-06-08_at_13_32_24.png)

Successfully connected to the EC2 instance via SSH using the labsuser.pem key at public IP 44.234.66.58. The Amazon Linux 2023 banner and the ec2-user@ip-192-168-1-25 prompt confirm a successful connection.

---

### 27. Ping google.com — Internet Connectivity Confirmed
![Ping results showing replies from google.com](screenshots/Screenshot_2026-06-08_at_13_33_43.png)

Running ping google.com from inside the EC2 instance returns consistent replies from 142.250.69.174 with 0% packet loss and average response time of ~7ms. This confirms that the VPC has full internet connectivity — Brock's problem is solved!

---

### 28. Submission Report
![Submission report](screenshots/Screenshot_2026-06-08_at_14_52_44.png)

The lab submission report confirms the lab was executed and completed successfully on Mon Jun 8 2026.

---

## Key Concepts

| Concept | Description |
|---|---|
| **VPC** | A logically isolated virtual network in AWS where you launch your resources |
| **Subnet** | A range of IP addresses within the VPC — public subnets can route traffic to the internet |
| **Internet Gateway (IGW)** | Attached to the VPC to enable internet communication. Must be added as a route target |
| **Route Table** | Contains rules (routes) that direct network traffic. Must be associated to a subnet |
| **0.0.0.0/0 Route** | The default route — directs all internet-bound traffic to the IGW |
| **Network ACL (NACL)** | A stateless firewall at the subnet level — must explicitly allow both inbound and outbound traffic |
| **Security Group** | A stateful firewall at the instance level — blocks all traffic by default, must allow inbound rules |
| **ping** | A network utility using ICMP to test connectivity — 0% packet loss means full internet access |
| **SSH** | Secure Shell — used to remotely connect to and manage EC2 instances |

---

## AWS Services Used

| Service | Purpose |
|---|---|
| **Amazon VPC** | Created the isolated network (`Test VPC`) with CIDR `192.168.0.0/18` |
| **Subnets** | Created `Public subnet` (192.168.1.0/26) within the VPC |
| **Internet Gateway** | Created and attached `IGW Test VPC` to enable internet access |
| **Route Tables** | Created `Public route table` with IGW route and subnet association |
| **Network ACLs** | Created `Public Subnet NACL` allowing all inbound and outbound traffic |
| **Security Groups** | Created `Public security group` allowing SSH, HTTP, and HTTPS |
| **Amazon EC2** | Launched an instance to test VPC internet connectivity via ping |
