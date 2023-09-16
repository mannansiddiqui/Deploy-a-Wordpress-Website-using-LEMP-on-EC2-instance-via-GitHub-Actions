# Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions

#### Description:

- Provision a Virtual Private Server (VPS) on AWS to host the WordPress website.
- Configure the VPS with a secure Linux distribution i.e. Ubuntu 22.04 and ensure that all necessary firewall rules are applied.
- Install and configure Nginx as the web server, MySQL as the database, and PHP for processing dynamic content.
- Set up a WordPress website on the VPS and secure it following best practices (e.g., strong passwords, limited user privileges, etc.).
- Implement SSL/TLS certificate using Let's Encrypt for secure communication between the server and clients.
- Optimize the Nginx server configuration to enhance website performance (e.g., caching, gzip compression, etc.).
- Set up a GitHub Actions workflow for the automated deployment of the WordPress website to the VPS.


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

First, list all the available application profiles using ```sudo ufw app list``` then create a firewall rule to allow application profiles i.e. Nginx Full and OpenSSH using ```sudo ufw allow "Nginx Full"``` and ```sudo ufw allow OpenSSH```. Then, enable ufw using ```sudo ufw enable```

![Screenshot from 2023-09-15 07-26-01](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/1d0ce7ac-c0de-4883-b5c0-91ef45b39dbc)

Install Mysql server using ```sudo apt install mysql-server -y```

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/a7207a1e-a44e-45f4-abb4-65994e3bd8fb)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/cf90271e-a99e-49d3-878f-467e0cceed83)

Let's configure MySQL

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/afdc3187-5a6d-4a83-a4b7-8be1b0a1a52e)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/1c9c2ae5-e1e2-45fa-8eba-2258b2368047)

Install PHP

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/19fd7337-3069-4bf1-a84d-2c62fb1ccffc)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/bfd1d2b6-fc36-483e-aa4d-a80df030e9bc)

Now, Configure nginx to use PHP

First, create a root directory i.e. ***/var/www/wordpress***, and create an Nginx configuration file with this as the document root and brainstormforce.ddns.net as a domain.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/0151bdeb-16b8-4114-a93b-c75166ef15cb)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/8283f0d8-ef80-4766-a46a-68a373018108)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/bc1e68d4-828c-4450-917c-be755ec5745e)

Let's test php with nginx. For this create a test PHP file in the document root.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/b46d83e1-f1ec-425b-af9c-73f20a2a6aaf)

Try accessing url i.e. ```http://brainstormforce.ddns.net/info.php```

It's working now we can remove the info.php file from the document root.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/b4b96dc7-8e30-4b43-b8b7-79e202752858)

Install php extensions and restart php-fpm

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/1333c9f9-3b4b-4670-9d95-8ad6bd252f68)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/1c6908e8-322c-4cf9-a850-48103c8c0273)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/257b044f-3eac-44d6-9ebb-db5df12b1db0)

#### Step-4: Set up a WordPress website on the VPS and secure it following best practices (e.g., strong passwords, limited user privileges, etc.).

Download WordPress in a root directory.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/70da695c-7a7b-4884-acd7-a441ce491f0a)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/cd5687a3-539f-44a0-bf61-1ad0726ce6ed)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/59985f24-a83f-478b-88fb-93080a2b69d7)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/a19d5df0-547d-4f97-85b0-e068a6e274a4)

Now, set up the WordPress config file.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/eb46d998-0409-4ff8-9281-2044b541b563)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/18794fcb-f7e7-467c-9e00-b9eff985d435)

Now, complete the WordPress installation through a web interface.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/66d9b130-c9c0-4994-ae37-23967133563e)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/5d27831d-a5fe-4395-8c23-fd82abc9ed4e)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/51f607c4-2093-4cd0-b9a2-59e67af1846e)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/ea9bc9f3-c8f0-49f9-bfd0-9a245364ad47)

#### Step-5: Implement SSL/TLS certificate using Let's Encrypt for secure communication between the server and clients.

To implement SSL/TLS install Certbot.

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/c0849f60-32be-47d8-90d5-41a196ff0ddf)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/db9b46fb-059e-42dd-986b-a9b776510825)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/a501fe88-4cb1-4c42-9e1d-89a919f728ea)

#### Step-6: Optimize the Nginx server configuration to enhance website performance (e.g., caching, gzip compression, etc.).

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/90af5d95-33c8-4f8d-b7ef-6a90ee8434a8)

After this reload the nginx using ```sudo systemctl reload nginx.service```

#### Step-7: Set up a GitHub Actions workflow for the automated deployment of the WordPress website to the VPS.

Now, let's create a GitHub actions workflow

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/19e9018c-ecb2-4e8f-963a-2e5669542682)

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/06d35c10-8f5b-4384-adaa-5ce00e852de0)

Let's hit the URL again to test

![image](https://github.com/mannansiddiqui/Deploy-a-Wordpress-Website-using-LEMP-on-EC2-instance-via-GitHub-Actions/assets/74168188/b6138623-a042-41ec-a67b-6653969000fa)

We are able to access it

THANK YOU...
