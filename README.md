
# 📖 Terraform Installation & Configuration on AWS EC2

This guide walks you through installing and configuring Terraform on an EC2 instance, and provisioning a simple AWS EC2 instance using Terraform.

---

## 📌 Prerequisites

- AWS account with Admin access
- SSH key pair for EC2 instance access
- Basic knowledge of EC2, SSH, and AWS CLI

---

## ⚙️ Steps to Install and Configure Terraform on EC2

---

### 🔐 0️⃣ Create IAM User with Admin Access

1. Go to **IAM Console → Users → Add Users**
2. Assign user to **Admin group**
3. Generate **Access Key ID** and **Secret Access Key**
4. Save credentials securely

---

### 🖥️ 1️⃣ Launch EC2 Instance

- **Instance Type**: `t2.medium`  
- **AMI**: Amazon Linux 2 (in `ap-south-1`)  
- **Security Group**:
  - Allow SSH: Port `22`

➡️ Create and download key pair: `terraform.pem`

---

### 🔑 2️⃣ SSH into EC2

```bash
cd Downloads
chmod 400 terraform.pem
ssh -i "terraform.pem" ec2-user@<EC2_PUBLIC_IP>
```

---

### ⚙️ 3️⃣ Install Dependencies & Terraform

#### ✅ Update packages

```bash
sudo yum update -y
```

#### 🐍 Install Python

```bash
sudo yum install python -y
python3 --version
```

#### ☁️ Install AWS CLI

```bash
sudo yum install awscli -y
aws --version
```

#### 🔐 Configure AWS CLI

```bash
aws configure
```

➡️ Provide:
- Access Key
- Secret Access Key
- **Region**: `ap-south-1`
- Output format: `json`

#### 🛠️ Install yum-utils and HashiCorp repo

```bash
sudo yum install -y yum-utils shadow-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
```

#### 📦 Install Terraform

```bash
sudo yum -y install terraform
terraform --version
```

---

### 📝 (Optional) Install Terraform on Windows (via PowerShell Admin)

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; `
[System.Net.ServicePointManager]::SecurityProtocol = `
[System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

choco install terraform
terraform -v
```

---

## 📁 4️⃣ Create and Run a Terraform Project

### 📁 Project Setup

```bash
sudo yum install git -y
https://github.com/AvinashTale99/terraform-ec2.git
cd terraform-ec2

terraform init
terraform plan
terraform apply
terraform destroy
```

### OR Create Your Own Project

```bash
mkdir project
cd project
touch main.tf
nano main.tf
```

---

### 📝 Sample `main.tf`

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "6.4.0"
    }
  }
}

# main.tf
resource "aws_instance" "web" {
  ami           = "ami-0a1235697f4afa8a4"
  instance_type = "t3.micro"
  key_name      = "key"
  tags = {
    Name = "webserver"
  }
}
```

---

### 📌 Initialize Terraform

```bash
terraform init
```

### 📊 Plan Deployment

```bash
terraform plan
```

### 🚀 Apply Configuration

```bash
terraform apply
```

> Type `yes` to confirm.

---

### 🗑️ Destroy Infrastructure

```bash
terraform destroy
```

> Type `yes` to confirm.

---

## ✅ Project Complete

You now have a fully functional **Terraform setup on an EC2 instance**, capable of provisioning AWS resources via infrastructure-as-code in the **Mumbai (ap-south-1)** region.

---

## 📎 Notes

- Replace `<EC2_PUBLIC_IP>` with your actual EC2 public IP.
- Update the **AMI ID** if Amazon Linux 2 has a newer version in `ap-south-1`.

---

## 👨‍💻 Author

**Avinash Tale**

### 🔗 Connect with Me

- 💼 [LinkedIn](https://www.linkedin.com/in/avinash-tale-3348b7217/)
- 🐙 [GitHub](https://github.com/AvinashTale99)
- 🐳 [Docker Hub](https://hub.docker.com/u/avinashtale99)
- 📷 [Instagram](https://www.instagram.com/avinash_tale_patil)
- 🌐 [Website](https://avinashtale99.github.io/AvinashRepo/)

---
