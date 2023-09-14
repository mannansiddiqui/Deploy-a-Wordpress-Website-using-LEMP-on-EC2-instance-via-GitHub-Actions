# Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions

#### Description:

• Provision a Virtual Private Server (VPS) on AWS to host the WordPress website.
• Configure the VPS with a secure Linux distribution i.e. Ubuntu 22.04 and ensure that all necessary firewall rules are applied.
• Install and configure Nginx as the web server, MySQL as the database, and PHP for processing dynamic content.
• Set up a WordPress website on the VPS and secure it following best practices (e.g., strong passwords, limited user privileges, etc.).
• Implement SSL/TLS certificate using Let's Encrypt for secure communication between the server and clients.
• Optimize the Nginx server configuration to enhance website performance (e.g., caching, gzip compression, etc.).
• Set up a GitHub Actions workflow for the automated deployment of the WordPress website to the VPS.


#### Step-1: Provision a Virtual Private Server (VPS) on AWS to host the WordPress website.

Sign to [AWS Management Console](https://console.aws.amazon.com/console/home) and provision an EC2 instance.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/e63d28ff-264f-49bd-a428-8d74a6d8f39d)

Allow ports 80 and 443 in the security group attached to the EC2 instance so we can access the WordPress website from the internet.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/18139609-9c38-4064-a519-a6aa21ba06ca)

#### Step-2: Configure the VPS with a secure Linux distribution i.e. Ubuntu 22.04 and ensure that all necessary firewall rules are applied.

SSH to VM using ```ssh -i <PRIVATE_KEY> ubuntu@<PUBLIC_IP>```

![Screenshot from 2023-09-14 19-08-01](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/ec1cc321-62c3-42d1-8cf0-80025ce75e94)

Update the apt repository, enable ufw firewall, and create a rule for ports 22, 80, and 4443.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/52c88a74-f7aa-4d1c-b473-17f4f57d438a)

