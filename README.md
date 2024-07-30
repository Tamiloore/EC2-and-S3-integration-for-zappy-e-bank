# Mini Project: EC2-and-S3-integration-for-zappy-e-bank
## Project Description: 
Zappy E-bank plans to deploy its application on AWS ECS, with S3 buckets serving as the backbone for storage solutions, including customer data, transaction logs, and analytical data. The integration of EC2 and S3, facilitated by a reversed proxy setup, aims to provide a seamless experience for managing and accessing diverse resources under a unified access point.
## Project Task:
**EC2:** Host the core application, enabling scalable computing capacity to meet growing customer demands.

**S3:** Offers secure, scalable objects strong for vast amounts of data, ensuring that Zappy E-bank can serve its customers efficiently and reliably.

## Tips
A reverse Proxy will be configured on the EC2 instance, directing requests to the appropriate destination.

This also explains how to launch an EC2 instance


## Step 1:
- Login into the AWS console as an IAM user

![1_aws](https://github.com/user-attachments/assets/067e4fa3-7e55-4d0b-97cb-dc4da048fcf7)

![2_aws](https://github.com/user-attachments/assets/269fd9f0-89ed-4dd1-a755-13983b1b9008)

## Step 2:
### Launching An Instance
 - Search for EC2 

![3_aws](https://github.com/user-attachments/assets/4b8cc2fd-e290-4d49-a558-f9f1dcaea8f9)


- Click on Launch Instance

![4_aws](https://github.com/user-attachments/assets/d2f5cece-5cbf-476f-85de-6a926d128d91)


- Insert your project Name 

![5_aws](https://github.com/user-attachments/assets/77e37c9c-66a1-4bdf-9065-936e1508c8b7)


- Select an Operating system to run (I'll be using the Ubuntu instance)

![5a_aws](https://github.com/user-attachments/assets/932a392a-dbc6-45c2-88f7-f9e5f658a611)


- Select Instance Type

![6_aws](https://github.com/user-attachments/assets/f9b6884a-d255-4174-bfdd-45daa1eefd02)


- You can decide to generate a key pair if you want to connect to a local server, but I won't be needing it here

![7_aws](https://github.com/user-attachments/assets/7bebd145-9c79-491b-8600-d2b0b85f00e8)


- Select  Network Settings

![9_aws](https://github.com/user-attachments/assets/ce5c32e2-00dd-4665-ab81-b2a86ddeedd8)


- Proceed without key pair

![10_aws](https://github.com/user-attachments/assets/548cad15-2cfa-4f69-98ce-b07540e84ec2)


- Connect to instance 

![12_aws](https://github.com/user-attachments/assets/d862b16d-8291-4cf7-be48-1a561b40f22b)


- You have successfully created an instance 

![13_aws](https://github.com/user-attachments/assets/5402398a-c894-4506-b8e5-ed4b26fb2ad7)


## Step 3:
### Assigning a Static IP (Elastic IP)
Associating an Elastic IP address with your EC2 instance ensures it retains the same public IP address across reboots.

- In the EC2 console navigation, select elastic IP and click on allocate elastic

![14_aws](https://github.com/user-attachments/assets/be738812-eff2-4b17-bd23-66834832d1eb)


![15_aws](https://github.com/user-attachments/assets/9224e5c6-5cb3-4a33-bc00-4f582f28a333)


- Follow the highlighted part

![6b_aws](https://github.com/user-attachments/assets/8c1be237-c347-4671-aee5-7f8cb9c86e6f)

- Click on *Associate*

![16_aws](https://github.com/user-attachments/assets/17b5bab8-fe6e-4a5a-b046-40f7d2f76160)

![17_aws](https://github.com/user-attachments/assets/26327ab8-20b9-49a6-86de-1b5ee0a8a963)


## Step 4:
### Creating S3 Bucket
- Search S3 and click

![20_aws](https://github.com/user-attachments/assets/e76d2a26-0f89-4770-9021-16b3ea910cae)


- Create a new bucket and give it a name of your choice 

![21_aws](https://github.com/user-attachments/assets/9e27a9d2-863c-4037-b295-c6a231ec538c)


- Create a new object inside the bucket. You should upload an index.html file containing 

![22_aws](https://github.com/user-attachments/assets/881c460e-cd69-4420-9ebf-9b94641c81eb)

![23_aws](https://github.com/user-attachments/assets/5a7a0c7e-6254-4666-bef3-31f32cb67724)

![24_aws](https://github.com/user-attachments/assets/b4993e4b-0adc-4f68-bf2d-d6778fc9e7aa)

![25_aws](https://github.com/user-attachments/assets/632b28ad-99e9-4596-b9d4-11aa95c2d657)

![26_aws](https://github.com/user-attachments/assets/c60b649c-8774-4941-ae3b-8f787db22030)


- On your computer, create an index.html file with the content "Welcome to Amazon

![27_aws](https://github.com/user-attachments/assets/ed8f6549-9380-4961-97c7-dae5964268f1)

![28_aws](https://github.com/user-attachments/assets/58a3d742-dc4a-44c5-a75b-416f4564ed63)


- Upload the index.html on S3 bucket as shown in the image below;

![29_aws](https://github.com/user-attachments/assets/31a26385-f9e1-47e5-a477-a15a00847c1e)


## Step 5:
### Configuring S3 Bucket for Web Hosting

- Click on your bucket name

![31_aws](https://github.com/user-attachments/assets/6de02e30-fce2-4024-ae6d-3fa92fec8d31)


- Click on the properties tab and scroll down

![32_aws](https://github.com/user-attachments/assets/f138cd0d-3fcc-4756-92f0-b26758e7940e)


- Click on edit 

![33_aws](https://github.com/user-attachments/assets/a82d5616-20fd-4a3c-a32a-09b182d7c9cf)

![34_aws](https://github.com/user-attachments/assets/010a732d-2025-4e19-986d-8c12daa6cc2d)

- Copy the URL
  
![35_aws](https://github.com/user-attachments/assets/f1aadcb4-69b8-4c69-a89d-c71240015edf)

## Step 6:
### Configuring a web server as Reverse Proxy

- On your EC2 instance, install Nginx web server
 
`sudo apt update -y && sudo apt install nginx -y`

![36_aws](https://github.com/user-attachments/assets/c6c0dd8d-1e0f-4515-b4e9-60362ae65abb)


- Configure the Web Server to Serve your S3 app directly and forward request to your S3 bucket

`sudo vim /etc/nginx/sites-available/mybucket`

![37_aws](https://github.com/user-attachments/assets/279b59bc-bc6f-4331-9a6b-c11feaecc01e)

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

**Note** Make sure to replace the link above with the link you generated after you enabled static web hosting for your bucket

![38_aws](https://github.com/user-attachments/assets/dc8b2566-89de-4420-9248-b8136bd7d7ce)

## Step 7:
### Make your index.html public

- Navigate to the *index.html* file, click on **Action** and then click on **Make Public**

![39_aws](https://github.com/user-attachments/assets/bdad4825-180d-477a-8f80-8cb820d3c11a)

![40_aws](https://github.com/user-attachments/assets/ba19d065-83e7-4383-936a-e78c5aa7ccbb)


## Step 8:
### Launch 
- insert this code to link the files 
`sudo ln -s /etc/nginx/sites-available/mybucket /etc/nginx/sites-enabled`

- Then Restart the nginx
`sudo systemctl restart nginx`

![Snipaste_2024-07-29_20-46-27](https://github.com/user-attachments/assets/f361aa80-99f9-4c12-967e-2109d97068e3)


- Copy your Public URL and paste into your browser







