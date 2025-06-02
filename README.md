# AWS Web Server Project

This project sets up a basic Apache web server on an Amazon EC2 instance using Amazon Linux 2. It serves a static HTML page hosted in this GitHub repository.

---

## 🚀 Features

- Apache HTTP Server setup on EC2
- Static website deployment (`index.html`)
- GitHub-based version control
- Automatic deployment via post-receive hook (optional)
- HTTPS support with Certbot (optional)

---

## 📦 Prerequisites

- AWS account with EC2 access
- SSH key pair
- EC2 security group allowing port 80 (HTTP)
- Git installed on the EC2 instance

---

## 🔧 Setup Instructions

### 1. Launch EC2 and Connect

Launch an Amazon Linux 2 EC2 instance and SSH into it:

```bash
ssh -i your-key.pem ec2-user@<EC2_PUBLIC_IP>
### 2. Install Git and Apache
bash
Copy
Edit
sudo yum update -y
sudo yum install git -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
### 3. Set Up Git Repository in Web Directory
bash
Copy
Edit
cd /var/www/html
sudo git init
Configure Git (if not already done):

bash
Copy
Edit
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
### 4. Add and Commit Initial HTML File
bash
Copy
Edit
echo "<h1>Hello, World!</h1>" | sudo tee index.html
sudo git add index.html
sudo git commit -m "Initial commit with index.html"
### 5. Link to Remote GitHub Repository (Optional)
Create a repository on GitHub, then link it:

bash
Copy
Edit
sudo git remote add origin https://github.com/username/repository.git
sudo git branch -M main
sudo git push -u origin main
### 6. Set Up Post-Receive Hook for Auto Deployment (Optional)
bash
Copy
Edit
cd /var/www/html/.git/hooks
sudo nano post-receive
Add this to the post-receive file:

bash
Copy
Edit
#!/bin/bash
GIT_WORK_TREE=/var/www/html git checkout -f
Make it executable:

bash
Copy
Edit
sudo chmod +x post-receive
### 7. Deploy Updates from Local Machine
On your local machine:

bash
Copy
Edit
git clone https://github.com/username/repository.git
cd repository
# make changes to index.html
git add .
git commit -m "Updated website content"
git push origin main
⚙️ If using post-receive hook, changes will auto-deploy to the EC2 web server.

### 8. Access Your Website
Open a browser and visit:

cpp
Copy
Edit
http://<EC2_PUBLIC_IP>
### 9. (Optional) Set Up HTTPS with SSL/TLS
bash
Copy
Edit
sudo yum install certbot python3-certbot-apache -y
sudo certbot --apache
Follow the interactive prompts to secure your site with HTTPS.
