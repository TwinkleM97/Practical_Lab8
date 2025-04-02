# Practical_Lab8 – PROG8830

## 🧠 Terraform Practical Assignment – Lab 8

This project demonstrates advanced Terraform capabilities including:

- ✅ `count` and `for_each` loops
- ✅ Built-in functions and expressions
- ✅ Modularized infrastructure as code
- ✅ A full web application stack on AWS

---

## 📦 Infrastructure Overview

The Terraform configuration builds the following infrastructure in a **modular and reusable** format:

- **VPC** with public subnets and route tables
- **EC2 Instances** (NGINX) created using `count`
- **Security Groups** created dynamically via `for_each`
- **Application Load Balancer (ALB)** targeting the EC2 instances
- **RDS PostgreSQL Database** with public access
- Use of **Terraform functions** like `cidrsubnet`, `length`, `formatdate`, and more

---

## 🧰 Prerequisites

- Terraform CLI installed
- AWS Academy credentials (use exported environment variables)
- Basic Terraform knowledge (providers, resources, modules)

---

## 🗂 Project Structure

/Lab8/ ├── main.tf # Root config calling modules ├── variables.tf # Top-level input variables ├── outputs.tf # Outputs from modules ├── providers.tf # AWS provider block ├── terraform.tfvars # Environment-specific values ├── modules/ │ ├── vpc/ # VPC, subnets, IGW, route tables │ ├── ec2/ # EC2 + security groups + user_data │ ├── alb/ # Load balancer + target group │ ├── rds/ # PostgreSQL instance config

yaml
Copy
Edit

---

## 🚀 Terraform Commands

```bash
terraform init         # Initialize project
terraform plan         # Review the infrastructure
terraform apply        # Deploy the resources
terraform destroy      # (Optional) Clean up all resources
🔁 Loops in Terraform
✅ count
Used for launching multiple EC2 instances:

resource "aws_instance" "web" {
  count = var.instance_count
  ...
}
✅ for_each
Used to dynamically generate security groups from a map:

hcl
Copy
Edit
resource "aws_security_group" "dynamic_sg" {
  for_each = var.security_groups
  ...
}
🧠 Terraform Functions Used
Category	Functions Used
String	formatdate(), upper(), lower()
Numeric	count.index + 1, min(), max()
Collection	for, concat(), length()
IP/CIDR	cidrsubnet() for subnet allocation
Date/Time	timestamp() for tagging deployments
🛡️ RDS Configuration
The RDS module provisions a PostgreSQL database with the following features:

Publicly accessible

Bound to security groups created via modules

Protected from accidental deletion via skip_final_snapshot

Sample:
resource "aws_db_instance" "postgres" {
  engine         = "postgres"
  instance_class = "db.t3.micro"
  ...
}
🧠 Lessons Learned
Looping: count is great for identical resources; for_each is ideal for maps or unique values.

Modularization: Breaking code into modules improves reusability and clarity.

Function Use: Functions like CIDR subnet, length, and format date make the infrastructure dynamic.

Security: Managing security groups with for_each enhances control and readability.

Real-World Ready: This structure mirrors how real-production Terraform projects are laid out.
