# Static Website Deployment
Static website project with HTML, CSS, and JavaScript, including deployment instructions for AWS EC2 using Nginx and Apache


## Author
- **Name:** Rotimi Abiola
- **Username:** rtmabiola
- **Email:** rtmabiola@gmail.com

## Website

The website includes information about the HNG Internship. Check it out [here](https://hng.tech).

## Deployment

This website is designed to be served using Nginx or Apache on an AWS EC2 instance.

### Steps to Deploy on an instance running ubuntu os and nginx webserver

1. Launch an EC2 instance (Ubuntu Server AMI).
2. Install Nginx:
    ```bash
    sudo apt update -y
    sudo apt install nginx -y
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```

3. Enable Firewall so that unconfigured services will not be exposed.
    ```bash
    sudo apt install ufw 
    sudo ufw allow 22
    sudo ufw allow 80
    sudo ufw logging off
    sudo ufw enable
    sudo ufw status
    ```
3. Copy the website files to the EC2 instance by cloning the repo through the repo URL(https://github.com/rotimiAbiola/static-website-deploy.git):
    ```bash
    git clone https://github.com/rotimiAbiola/static-website-deploy.git
    ```
4. Create a directory for the webfiles in the Nginx web root directory
    ```bash
    sudo mkdir /var/www/html/hng.rtmdemos.name.ng/
    ```

5. Move the files to the Nginx web root:
    ```bash
    sudo mv /home/ubuntu/static-website-deploy/* /var/www/hng.rtmdemos.name.ng/
    ```

6. Replace the content of the default file in the /etc/nginx/sites-available/ directory. You should replace the domain name (hng.rtmdemos.name.ng) in the configuration file to any domain name you have access to as well.Then copy and paste the following config into the file.
    ```bash
    server {
        listen 80;
        listen [::]:80;

        server_name hng.rtmdemos.name.ng;

        root /var/www/html/hng.rtmdemos.name.ng/;
        index index.html;

        location / {
                try_files $uri $uri/ =404;
        }
    }   
    ```

7. Restart Nginx:
    ```bash
    sudo systemctl restart nginx
    ```

Your website should now be accessible via the public IP address of your EC2 instance. To access your website via the domain name, you need to add an A record on your DNS manager that points your domain name to the IP address of the EC2 instance.


### Steps to Deploy on an instance running red hat os and apache webserver
1. Launch an EC2 instance (Red Hat Enterprise Linux 9 AMI).
2. Install Nginx:
    ```bash
    sudo yum update -y
    sudo yum install httpd -y
    sudo systemctl start httpd
    sudo systemctl enable httpd
    ```
3. Copy the website files to the EC2 instance by cloning the repo through the repo URL(https://github.com/rotimiAbiola/static-website-deploy.git):
    ```bash
    git clone https://github.com/rotimiAbiola/static-website-deploy.git
    ```

4. Move the files to the Nginx web root:
    ```bash
    sudo mv /home/ec2-user/static-website-deploy/* /var/www/html/
    ```

5. Restart Apache:
    ```bash
    sudo systemctl restart httpd
    ```




