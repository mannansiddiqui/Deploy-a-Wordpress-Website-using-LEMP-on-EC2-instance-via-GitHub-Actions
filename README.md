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

Update the apt repository, enable ufw firewall, and create a rule for ports 22, 80, and 443.

To update apt repository run ```sudo apt update``` and to check the ufw status run ```sudo ufw status```

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/52c88a74-f7aa-4d1c-b473-17f4f57d438a)

#### Step-3: Install and configure Nginx as the web server, MySQL as the database, and PHP for processing dynamic content.

Installing Nginx on Ubuntu 22.04 using ```sudo apt install nginx -y```

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/80e539b5-10ca-4d09-85a4-a21bb8b2089d)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/9c3870f0-6105-4038-a3ae-cfbfc42a15b5)

First, list all the available application profiles using ```sudo ufw app list``` then create a firewall rule to allow application profiles i.e. Nginx Full and OpenSSH using ```sudo ufw allow "Nginx Full"``` and ```sudo ufw allow OpenSSH```

![Screenshot from 2023-09-15 07-26-01](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/1d0ce7ac-c0de-4883-b5c0-91ef45b39dbc)

Install Mysql server using ```sudo apt install mysql-server -y```

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/a7207a1e-a44e-45f4-abb4-65994e3bd8fb)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/cf90271e-a99e-49d3-878f-467e0cceed83)

Install php extensions
