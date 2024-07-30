# Mini Project: EC2-and-S3-integration-for-zappy-e-bank
## Project Description: 
Zappy E-bank plans to deploy its application on AWS ECS, with S3 buckets serving as the backbone for storage solutions, including customer data, transaction logs, and analytical data. The integration of EC2 and S3, facilitated by a reversed proxy setup, aims to provide a seamleass exprience for managing and accessing diverse resources under a unified access point.
## Project Task:
**EC2:** Host the core application, enabling scalable computing capacity to meet growing customers demands.

**S3:** Offers secure, scalable object stronge for vast amounts of data, ensuring that Zappy E-bank can serve its customers efficiently and reliably.

## Tips
A reverse Proxy will be configured on the EC2 instance, directing requests to the appropriate destination.

This also explians how to launch an EC2 instance


## Step 1:
- Login into the AWS console as an IAM user

![alt text](img/1_aws.png)

![alt text](img/2_aws.png)

## Step 2:
### Launching An Instance
 - Search for EC2 

![alt text](img/3_aws.png)

- Click on Launch Instance

![alt text](img/4_aws.png)

- Insert your project Name 

![alt text](img/5_aws.png)

- Select an Operating system to run (I'll be using the ubuntu Instance)

![alt text](img/5a_aws.png)

- Select Instance Type

![alt text](img/6_aws.png)

- You can decide to generate a key pair if you want to connect to local server, but i won't be needing it here

![alt text](img/7_aws.png)

- Select  Network Settings

![alt text](img/9_aws.png)

- Proceed without key pair

![alt text](img/10_aws.png)

- Connect to instance 

![alt text](img/12_aws.png)

- You have succesfully created an instance 

![alt text](img/13_aws.png)

## Step 3:
### Assigning a Static IP (Elastic IP)
Associating an Elastic IP address with your EC2 instance ensure it retains the same public IP address across reboots.

- In the EC2 console navigation, select elastic Ip and click on allocate elastic

![alt text](img/14_aws.png)

![alt text](img/15_aws.png)

- Follow the highlighted part

![alt text](img/16a_aws.png)

- Click on *Associate* 

![alt text](img/17_aws.png)

## Step 4:
### Creating S3 Bucket
- Search S3 and click

![alt text](img/20_aws.png)

- Create a new bucket and give it a name of your choice 

![alt text](img/21_aws.png)

- Create a new object inside the bucket. You should upload an index.html file containng 

![alt text](img/22_aws.png)

![alt text](img/23_aws.png)

![alt text](img/24_aws.png)

![alt text](img/25_aws.png)

![alt text](img/26_aws.png)

- On your computer, create an index.html file with the content "Welcome to Amazaon

![alt text](img/27_aws.png)

![alt text](img/28_aws.png)

- Upload the index.html on S3 bucket as shown in the image below;

![alt text](img/29_aws.png)

## Step 5:
### Confiquring S3 Bucket for Web Hosting

- Click on your bucket name

![alt text](img/31_aws.png)

- Click on the properties tab and scroll down

-![alt text](img/32_aws.png)

- Click on edit 

![alt text](img/33_aws.png)


![alt text](img/34_aws.png)

- Copy the Url
![alt text](img/35_aws.png)


## Step 6:
### Confiquring a web server as Reverse Proxy

- On your EC2 instance, install Nginx web server
 
`sudo apt update -y && sudo apt install nginx -y`

![alt text](img/36_aws.png)

- Configure the Web Server to Serve your S3 app directly and forward rewuest to your S3 bucket

`sudo vim /etc/nginx/sites-available/mybucket`

![alt text](img/37_aws.png)

- Paste the configuration code snippet below and replace the highlighted part with your S3 link 

 ```                
 server {
    listen 80;
    server_name 100.26.55.173;  # Replace with your domain name or server IP address

    location / {
        proxy_pass https://your-bucket-name.s3.amazonaws.com; # Replace with the link you generated after you enabled  static web hosting for your bucket
        proxy_set_header Host your-bucket-name.s3.amazonaws.com;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

**Note** Make sure to replace the link above with the likn you generated after you enabled static web hosting for your bucket

![alt text](img/38_aws.png)

## Step 7:
### Make your index.html public

- Navigate to the *index.html* file, click on **Action** and then click on **Make Public**

![alt text](img/39_aws.png)

![alt text](img/40_aws.png)

## Step 8:
### Launch 
- insert this code to link the files 
`sudo ln -s /etc/nginx/sites-available/mybucket /etc/nginx/sites-enabled`

- Then Restart the nginx
`sudo systemctl restart nginx`

![alt text](img/Snipaste_2024-07-29_20-46-27.png)

- Copy your Public Url and paste on your browser







