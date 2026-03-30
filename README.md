# AWS Systems Manager Operations Lab

## Project Overview
This lab demonstrates how to manage an Amazon EC2 instance using **AWS Systems Manager** instead of traditional SSH access. The project focuses on operational tasks that are common in cloud support and infrastructure roles, including secure remote access, command execution, and basic patch compliance.

The lab uses:
- **Session Manager** instead of SSH
- **Run Command** for remote administration
- **Patch Manager** basics for scanning and patching
- **IAM role-based access** for Systems Manager management
- **No inbound SSH rule** on the EC2 security group

---

## Why I Built This
I built this lab to show an operations-focused AWS workflow rather than just deploying infrastructure. In real-world cloud environments, secure instance management, remote administration, and patch compliance are important day-2 operational tasks.

This project shows how to:
- securely access an EC2 instance without opening port 22
- run shell commands remotely at scale
- perform patch scanning and basic patching tasks
- use Systems Manager in a way that aligns with cloud operations and support work

---

## AWS Services Used
- **Amazon EC2**
- **AWS Identity and Access Management (IAM)**
- **AWS Systems Manager**
  - Session Manager
  - Run Command
  - Patch Manager
- **Amazon VPC** (default VPC used for simplicity)

---

## What I Built
I launched an EC2 instance running Amazon Linux and attached an IAM role with the `AmazonSSMManagedInstanceCore` policy. After the instance registered as a Systems Manager managed node, I used:

- **Session Manager** to open a shell session in the browser without SSH
- **Run Command** with `AWS-RunShellScript` to gather system information and make a file change
- **Patch Manager / AWS-RunPatchBaseline** to perform a patch scan and review compliance

The EC2 security group was configured with **no inbound SSH access**, proving the instance could still be managed securely through Systems Manager.

---

## Architecture
The environment for this lab was intentionally kept simple and operations-focused:

- **Administrator**
- **AWS Systems Manager**
- **EC2 instance**
- **IAM role attached to EC2**
- **No inbound SSH rule**

### Key Design Point
The main design goal was to manage the EC2 instance **without using SSH keys or opening inbound port 22**.

---

## Validation Steps
I validated the lab by confirming the following:

- The EC2 instance launched successfully
- The IAM role was attached with `AmazonSSMManagedInstanceCore`
- The instance appeared in **Systems Manager Managed Nodes**
- A Session Manager shell opened successfully
- Run Command completed successfully
- Patch scan completed successfully
- The security group had **no inbound SSH rule**

---

## Screenshots
1. IAM role with `AmazonSSMManagedInstanceCore`

<img width="1595" height="572" alt="01-iam-role-ssm-core" src="https://github.com/user-attachments/assets/d1bb2b67-a80d-4bfe-a0ec-97b66f2272c2" />

2. EC2 instance details

<img width="1312" height="734" alt="02-ec2-instance-details" src="https://github.com/user-attachments/assets/868f4c52-3de6-457e-9990-d8569685e746" />

3. Systems Manager managed node

<img width="1779" height="570" alt="03-ssm-managed-node" src="https://github.com/user-attachments/assets/084d2d88-3f1c-41d2-b07d-c305b84d3a97" />

4. Session Manager shell

<img width="599" height="368" alt="04-session-manager-shell" src="https://github.com/user-attachments/assets/241f5fa5-43bf-44a3-9806-c206a1b2be38" />

5. SSM Agent status

<img width="875" height="227" alt="05-ssm-agent-status" src="https://github.com/user-attachments/assets/4acdc185-e2e8-4ebf-aa37-0bbd4acf22e7" />

6. Run Command success

<img width="1586" height="642" alt="06-run-command-success" src="https://github.com/user-attachments/assets/93cd08e2-2a8c-45a1-a33a-62dc55af9e70" />

7. Run Command output

<img width="1569" height="322" alt="07-run-command-output" src="https://github.com/user-attachments/assets/c6f1bd2f-f533-46e9-bcef-b0a12cb61778" />

8. File change through Run Command

<img width="1603" height="525" alt="08-run-command-file-change" src="https://github.com/user-attachments/assets/30759650-7c49-4519-b2d4-74c56d543772" />

9. Patch scan run

<img width="1590" height="304" alt="09-patch-scan-run" src="https://github.com/user-attachments/assets/b32ad71c-abc5-4bbd-a9e3-8036bb9c7057" />

10. Patch compliance or patch command results

<img width="1594" height="631" alt="10-patch-compliance-results" src="https://github.com/user-attachments/assets/cb3a22f4-3514-4679-a853-a7e2a79c781d" />

11. Optional patch install results

<img width="1593" height="747" alt="11-patch-install-results" src="https://github.com/user-attachments/assets/a54eef92-f51d-4270-8557-2cc5da3c75d2" />

12. Security group showing no inbound SSH

<img width="1634" height="433" alt="12-no-inbound-ssh" src="https://github.com/user-attachments/assets/1d28f644-0ca2-40a1-8aac-27c262dfb7e3" />

---

## Example Commands Used

### Session Manager
```bash
whoami
hostname
cat /etc/os-release
pwd
sudo systemctl status amazon-ssm-agent --no-pager
ss -tulpn
