# AWS Web Server Project

This project sets up a basic Apache web server on an Amazon EC2 instance using Amazon Linux 2. It serves a static HTML page hosted in this GitHub repository.

## 🚀 Features

- Apache HTTP Server setup on EC2
- Static website deployment (`index.html`)
- GitHub version control

---

## 📦 Prerequisites

- AWS account with EC2 access
- Key pair for SSH
- Security group allowing port 80 (HTTP)
- Git installed on EC2 instance

---

## 🔧 Setup Instructions

### 1. Launch EC2 and Connect

Create an Amazon Linux 2 EC2 instance and SSH into it:

```bash
ssh -i your-key.pem ec2-user@<EC2_PUBLIC_IP>
2. Install Apache
bash
Copy
Edit
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
3. Clone the Repository
bash
Copy
Edit
cd /var/www/html
sudo rm -rf *
sudo git clone https://github.com/Siddb1/AWSWebServerProject.git .
Now visit http://<EC2_PUBLIC_IP> in your browser to view the website.

🔄 Update Content
To update the live site:

bash
Copy
Edit
cd /var/www/html
sudo git pull origin main
