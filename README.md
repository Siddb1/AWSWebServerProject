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
2. Install Git and Web Server
Update the Instance:

Run the following commands to update the package lists:
sudo yum update -y    # Amazon Linux

Install Git:
Install Git by running:
sudo yum install git -y    # Amazon Linux

Install Apache

sudo yum install httpd -y    # Amazon Linux

Start the Web Server:

Start the web server:
sudo systemctl start httpd    # Apache

Enable Web Server on Boot:

Ensure the web server starts on reboot:
sudo systemctl enable httpd    # Apache

4. Set Up a Git Repository for the Web Server
Navigate to Web Directory:

Apache:
cd /var/www/html

Initialize a Git Repository:

Run:
sudo git init
Configure Git User:

Set up Git user information:
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
5. Add and Commit Web Content
Create a Basic HTML File:

Apache:
echo "<h1>Hello, World!</h1>" | sudo tee index.html

Stage and Commit the File:

Run:
sudo git add index.html
sudo git commit -m "Initial commit with index.html"
6. Set Up a Remote Git Repository (Optional)
Create a Repository on GitHub:

Log in to GitHub and create a new repository.
Link to Remote Repository:

Connect your local repository to GitHub:
sudo git remote add origin https://github.com/username/repository.git
sudo git branch -M main
sudo git push -u origin main
7. Set Up a Post-Receive Hook for Automatic Deployment
Create a Post-Receive Hook:

Navigate to the Git hooks directory:
cd /var/www/html/.git/hooks    # Apache

Create the post-receive Hook:

Create the hook script:
sudo nano post-receive
Add the following content to the script:
#!/bin/bash
GIT_WORK_TREE=/var/www/html git checkout -f   # Apache

Save and exit.
Make the Hook Executable:

Run:
sudo chmod +x post-receive
8. Push Changes from Your Local Machine
Clone the Repository Locally:

Clone the GitHub repository to your local machine:
git clone https://github.com/username/repository.git
cd repository
Make Changes to the Website:

Modify index.html or other files locally.
Commit and Push Changes:

Stage, commit, and push the changes:
git add .
git commit -m "Updated website content"
git push origin main
Deploy Changes Automatically:

The changes will be automatically deployed to your EC2 instance thanks to the post-receive hook.
9. Access Your Website
View Your Website:
Open a web browser and navigate to http://your-ec2-public-ip to view your deployed website.
10. Set Up HTTPS with SSL/TLS (Optional)
Install Certbot:

Install Certbot for Apache:
sudo yum install certbot python3-certbot-apache -y   # Apache

Run Certbot:

Obtain and install the SSL certificate:
sudo certbot --apache    # Apache
Follow the Prompts:

Certbot will guide you through securing your website with HTTPS.
This step-by-step guide should help you set up a web server project on an EC2 instance using Git, complete with automatic deployment and optional HTTPS setup.
