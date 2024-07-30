# Deploying a Node Js Application on AWS EC2

### Testing the project locally

1. Clone this project 
```
git clone https://github.com/SUBHAM-NANDI/AWS-Session.git
```
2. Open the project on VSCode.
   
3. Create an environment variable(.env) file.
 ```
 touch .env
 ```
This will create a hidden .env file.

**Environment variable** files are essential for securely managing configuration settings and secrets across different environments (development, testing, production). They separate configuration from code, enhance security by preventing hardcoding of sensitive data, ensure consistency, simplify deployment, and support easy environment-specific configurations. This centralized management approach promotes maintainability and flexibility, making managing and updating settings easier without altering the codebase.
   
4. Setup the following environment variables - `(.env)` file
```
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""
```
Create a Stripe account for free and copy the publishable and secret keys, respectively.
Document link - https://docs.stripe.com/keys

5. Initialise all dependencies and start the project
```
npm install 
npm run start
```

### Set up an AWS EC2 instance

1. Create an IAM user & login to your AWS Console
    - Access Type - Password
    - Permissions - Admin
      
2. Create an EC2 instance
    - Select an OS image - Ubuntu
    - Create a new key pair & download `.pem` file
    - Instance type - t2.micro
      
3. Connecting to the instance using ssh

Open an SSH client.
Locate your private key file. The key used to launch this instance is node.js-app-deploy.pem
Run this command, if necessary, to ensure your key is not publicly viewable. 
Change the permission of the .pem file using the below cmd.
```
chmod 400 "instance.pem"
```
Connect to the ec2 instance using the below cmd

```
ssh -i instance.pem ubunutu@<PUBLIC IP_ADDRESS>
```

### Configuring Ubuntu on remote VM

1. Updating the outdated packages and dependencies
```
sudo apt update
```
3. Install Git - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04) 
4. Configure Node.js and `npm` - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04)

### Deploying the project on AWS

1. Clone this project in the remote VM
```
git clone https://github.com/verma-kunal/AWS-Session.git
```
2. Setup the following environment variables - `(.env)` file
```
DOMAIN= ""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY=""
SECRET_KEY=""
```
> For this project, we'll have to set up an [Elastic IP Address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) for our EC2 & that would be our `DOMAIN`

3. Initialise and start the project
```
npm install
npm run start
```

> NOTE - We will have to edit the **inbound rules** in the security group of our EC2, in order to allow traffic from our particular port

### Project is deployed on AWS 🎉
