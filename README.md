<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** Kiprono Yegon  
**Email:** kipronoyegon50@gmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service from Amazon Web Services that allows you to create a private, isolated network within the cloud where you can securely run your applications and resources. It is useful because it gives you full control over your networking environment, including IP address ranges, subnets, routing, and security settings, enabling you to protect your systems, manage traffic flow, and design scalable architectures.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to isolate the resources that I needed for the project and allow interdependence

### One thing I didn't expect in this project was...

The project is very insightful on security of resources in the cloud

### This project took me...

This project took me about one and a half hours

---

## In the first part of my project...

### Step 1 - Architecture set up

I will :
Create a VPC from scratch!
Launch an EC2 instance, which you'll connect to using EC2 Instance Connect later.
Set up an S3 bucket.


### Step 2 - Connect to EC2 instance

In this step, I will connect to the EC2 instance and try access S3 through the public internet!



### Step 3 - Set up access keys

In this step, I will create access keys  because they give the EC2 instance access to the AWS environment.

### Step 4 - Interact with S3 bucket

In this step, I will use the EC2 instance to access the S3 bucket .

---

## Architecture set up

I started my project by launching an EC2 instance and enabled the automatic IP address to be able to use Instance Connect

I also set up an S3 bucket and uploaded two files

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured the Access Key Id, Secret Access Key, Default Region Name and the default output format which is left at the default

Access keys are credentials for  applications and other servers to log into AWS and talk to your AWS services/resources.

Secret access keys are like passwords that pair with access key ID and is needed for AWS services' access

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use IAM role with the necessary permissions and then attaching that role to your EC2 instance.


---

## Connecting to my S3 bucket

The command I ran was "aws s3 ls". This command is used to list all the S3 buckets in the Amazon s3 storage

The terminal responded with alist of the S3 buckets available in the account This indicated that the access keys I set up connected my the instance to Amazon servics

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command a"ws s3 ls s3://nextwork-vpc-project-yegon" which returned a list of the files I had uploaded to the bucket

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command "sudo touch /tmp/test.txt". This command creates a file "test.txt" in the tmp folder

The second command I ran was "aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-yegon"This command will copy  the test.txt file to the s3 bucket

The third command I ran was... which validated that...The third command I ran was "aws s3 ls s3://nextwork-vpc-project-yegon" which validated that the test.txt file that was created earlier has been uploaded to the S3 bucket

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will set up a way for the  VPC and S3 to communicate direclty because the EC2 nstance is connected to the bucket through the public internet.
This isn't the most secure way to communicate - external threats and attacks can easily intercept your commands and get access to your AWS environment or sensitive data.

### Step 6 - Bucket policies

We will validate the endpoint connection by blocking the S3 bucket from ALL traffic except the traffic coming from the endpoint and test if the instance can still access the S3.

### Step 7 - Update route tables

In this step, I will access the S3 via the EC2 instance to check the connectivity via the VPC Endpoint and troubleshoot any arising error

### Step 8 - Validate endpoint conection

In this step, I will test the VPC endpoint set up.
Restrict your VPC's acccess to your AWS environment.



---

## Setting up a Gateway

I set up an S3 Gateway, which is an endpoint used specifically for Amazon S3 and DynamoDB (DynamoDB is an AWS database service).



### What are endpoints?

An endpoint is a service that allows private connections between your VPC and other AWS services without needing the traffic to go over the internet.

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a a type of IAM policy designed for setting access permissions to an S3 bucket. Using bucket policies, you get to decide who can access the bucket and what actions they can perform with it.

My bucket policy will deny all actions on your S3 bucket and its objects to everyone unless the access is from the VPC endpoint 

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because the policy denies all actions unless they come from the VPC endpoint. This means any attempt to access the bucket from other sources, including the AWS Management Console, is blocked!

I also had to update my route table because it gives the route that directs traffic bound for S3 to your VPC endpoint, traffic from your EC2 instance is actually trying to get to your S3 bucket through the public internet instead

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I modified the route table allowing the subnet in the route table

After updating my public subnet's route table, my terminal could return the list of the files in the S3 bucket

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a set of rules that controls what users or services can access through a VPC endpoint.

I updated my endpoint's policy by changing the effect to deny. I could see the effect of this right away, because when I ran the command to list the object in the S3 bucket, there was an error.

![Image](http://learn.nextwork.org/inspired_gray_mysterious_dragon/uploads/aws-networks-endpoints_3e1e79a3)

---

---
