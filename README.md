# AWS Project: Windows Server in Private Subnet with Bastion Host

## Objective
Deploy a Windows EC2 instance in a private subnet and securely access it from a local machine using a Bastion Host (Jump Server).

---

## Project Demo (YouTube)

Watch the full implementation here:  
https://youtu.be/OuRl7CUXsZs

---

## Architecture
# cbds-project

---

## Step 1: Create VPC

- Go to AWS VPC Console
- Create VPC:
  - CIDR Block: `10.0.0.0/16`

---

## Step 2: Create Subnets

### Public Subnet
- CIDR: `10.0.1.0/24`

### Private Subnet
- CIDR: `10.0.2.0/24`

---

## Step 3: Attach Internet Gateway

- Create Internet Gateway
- Attach it to the VPC

---

## Step 4: Configure Public Route Table

- Create Route Table: `public-rt`
- Add Route:
- - Associate with Public Subnet

---

## Step 5: Configure Private Route Table

- Create Route Table: `private-rt`
- Associate with Private Subnet

### Important:
- Do NOT add:
- 
---

## Step 6: Launch Bastion Host (Public EC2)

- Go to EC2 → Launch Instance
- OS: Amazon Linux / Windows
- Subnet: Public Subnet
- Enable Public IP: YES

### Security Group:
OR

---

## Step 7: Launch Windows EC2 in Private Subnet

- OS: Windows Server
- Subnet: Private Subnet
- Public IP: DISABLED

### Security Group:

---

## Step 8: Connect to Bastion Host

### Linux Bastion:
```bash
ssh -i key.pem ec2-user@<bastion-public-ip>
<private-ip-of-windows-ec2>
ssh -i key.pem -L 3389:<private-ip>:3389 ec2-user@<bastion-public-ip>
localhost:3389
