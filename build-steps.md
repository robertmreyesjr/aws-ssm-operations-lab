
---

# build-steps.md

```md
# AWS Systems Manager Operations Lab - Build Steps

## Goal
Build an operations-focused AWS lab that uses **AWS Systems Manager** to manage an EC2 instance without SSH.

This lab demonstrates:
- Session Manager instead of SSH
- Run Command for remote administration
- Patch Manager basics
- IAM role-based management
- No inbound SSH rule on the instance

---

## Part 1 - Create the IAM Role

### Step 1
Sign in to the AWS Management Console.

### Step 2
Go to **IAM**.

### Step 3
In the left navigation menu, click **Roles**.

### Step 4
Click **Create role**.

### Step 5
Choose **AWS service** as the trusted entity.

### Step 6
Choose **EC2**.

### Step 7
Click **Next**.

### Step 8
Search for the policy:
`AmazonSSMManagedInstanceCore`

### Step 9
Select the policy.

### Step 10
Click **Next**.

### Step 11
Name the role:
`EC2-SSM-Managed-Role`

### Step 12
Click **Create role**.

### Screenshot
Take a screenshot showing:
- role name
- attached `AmazonSSMManagedInstanceCore` policy

Suggested filename:
`01-iam-role-ssm-core.png`

---

## Part 2 - Launch the EC2 Instance

### Step 13
Go to **EC2**.

### Step 14
Click **Launch instance**.

### Step 15
Name the instance:
`ssm-ops-lab-instance`

### Step 16
Choose an AMI:
- **Amazon Linux 2023**
- or **Amazon Linux 2**

### Step 17
Choose a small instance type appropriate for Free Tier / low-cost use.

### Step 18
For key pair:
- choose **Proceed without a key pair** if allowed

### Step 19
In Network settings:
- use the default VPC for simplicity
- allow auto-assign public IP if default
- remove any inbound SSH rule
- leave the instance with **no inbound rules**

### Step 20
In the IAM instance profile section, attach:
`EC2-SSM-Managed-Role`

### Step 21
Launch the instance.

### Screenshot
Take a screenshot showing:
- instance name
- running state or instance summary
- IAM role attached
- security group attached

Suggested filename:
`02-ec2-instance-details.png`

---

## Part 3 - Confirm Systems Manager Registration

### Step 22
Wait for the EC2 instance to reach **Running** state and pass status checks.

### Step 23
Go to **AWS Systems Manager**.

### Step 24
Open **Managed Nodes** or **Fleet Manager**.

### Step 25
Confirm the instance appears as a managed node.

### Screenshot
Take a screenshot showing:
- managed node listing
- instance name or ID
- platform / status if visible

Suggested filename:
`03-ssm-managed-node.png`

---

## Part 4 - Connect with Session Manager

### Step 26
In Systems Manager, go to **Session Manager**.

### Step 27
Click **Start session**.

### Step 28
Select your managed instance.

### Step 29
Click **Start session** again.

### Step 30
In the browser terminal, run:

```bash
whoami
hostname
cat /etc/os-release
pwd