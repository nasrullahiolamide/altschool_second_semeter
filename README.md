# README: AltSchool Africa Karatu 24 Cloud Engineering Second Semester Exam Project 

## Project Title
Welcome to "my" Landing Page

## Description
This project involves setting up a Linux server, configuring a web server (Nginx), and deploying a simple HTML landing page. The purpose of this project is to demonstrate proficiency in server provisioning, configuration, and application deployment.

---

## Steps to Provision the Server and Deploy the Application

### 1. Provisioning the Server
#### Platform Used:
AWS EC2 (Amazon Web Services Elastic Compute Cloud)

#### Steps:
1. **Launch an EC2 Instance**:
   - Logged into the AWS Management Console.
   - Navigated to EC2 and clicked on "Launch Instance."
   - Selected the **Ubuntu Server 22.04 LTS** as the Amazon Machine Image (AMI).
   - Chose an instance type (t2.micro) suitable for this project.
   - Configured the security group to allow HTTP (port 80) and SSH (port 22) traffic.
   - Created and downloaded a key pair for SSH access.
   - Launched the instance and noted the public IP address.

2. **Connect to the Server**:
   - Used the terminal to SSH into the server:
     ```bash
     ssh -i "server-key.pem" ubuntu@[Public_IP_Address]
     ```
   - Updated the package manager and installed essential tools:
     ```bash
     sudo apt update && sudo apt upgrade -y
     sudo apt install curl -y
     ```

---

### 2. Web Server Setup
#### Installing Nginx:
1. Installed Nginx on the server:
   ```bash
   sudo apt install nginx -y
   ```

2. Enabled and started the Nginx service:
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

3. Confirmed that Nginx was running by accessing the server's public IP address in a browser:
   - URL: `http://[Public_IP_Address]`

---

### 3. Deploying the HTML Page
1. **Created the HTML Page:**
   - Developed a simple HTML page containing the following:
     - My name.
     - A project title: "Welcome to [Your Name] Landing Page."
     - A brief description of the project.
     - My full bio.

   - Saved the file as `index.html` on my local machine.

2. **Transferred the HTML File to the Server:**
   - Used SCP (Secure Copy) to transfer the HTML file to the server:
     ```bash
     scp -i "server-key.pem" index.html ubuntu@[Public_IP_Address]:/tmp
     ```

3. **Moved the HTML File to the Web Server Directory:**
   - Logged into the server via SSH and moved the file:
     ```bash
     sudo mv /tmp/index.html /var/www/html/index.html
     ```

4. **Tested the Deployment:**
   - Accessed the HTML page in the browser using the server's public IP:
     - URL: `http://[Public_IP_Address]`

---

### 4. Networking Configuration
1. **Security Group Rules:**
   - Configured the EC2 instance security group to allow:
     - HTTP (port 80): Enables web traffic.
     - SSH (port 22): Enables secure remote access.

2. **Firewall:**
   - Verified that the UFW (Uncomplicated Firewall) was inactive (optional):
     ```bash
     sudo ufw status
     ```
   - If active, allowed HTTP traffic:
     ```bash
     sudo ufw allow 'Nginx HTTP'
     ```

---

## Public IP Address
- **URL to Access the Page:** `http://[Public_IP_Address]`

---

## Challenges and Solutions
1. **Firewall Blocked HTTP Traffic:**
   - Ensured that port 80 was open in the security group and firewall.

2. **HTML File Permissions:**
   - Verified that the `index.html` file had the correct permissions to be served by Nginx:
     ```bash
     sudo chmod 644 /var/www/html/index.html
     ```

---

## Conclusion
This project successfully demonstrates the process of server provisioning, web server configuration, and deploying a live HTML landing page accessible to any browser. It highlights my ability to set up and manage a Linux server environment efficiently.

