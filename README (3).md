<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](https://nextwork.ai/projects/749fab76-0a0b-5822-9b31-c7863050c9bd)

**Author:** Komeezzy  
**Email:** komonservices@gmail.com

---

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_09bcaa8a)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated network inside AWS where you control your own IP range, subnets, route tables, and gateways. It's useful because it gives you full control over what can reach your resources, and from where.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to build an isolated network, then set up a Gateway endpoint so my EC2 instance could reach S3 privately instead of over the public internet.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how alot of the services come together that's crazy!

### This project took me...

This project took me 2 hours

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will create a VPC, launch an EC2 instance, set up an S3 bucket the baseline for everything else.


### Step 2 - Connect to EC2 instance

In this step, I will connect via EC2 Instance Connect to run CLI commands and test S3 access before/after the endpoint.

### Step 3 - Set up access keys

In this step, I will give your EC2 instance access to your AWS environment because that's the next step.

### Step 4 - Interact with S3 bucket

In this step, I will get your EC2 instance to get access to the S3 bucket because that's the next step towards the endpoints.

## Architecture set up

I started my project by launching an EC2 Instance.

I also set up my bucket with files inside it to use the EC2 instances

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4334d777)

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured my Access Key ID, Secret Access key, default region name and the default output format.

Access keys are long-term credentials used to sign programmatic requests to AWS services

Secret access keys are like the password that pairs with your access key ID. You need both to access AWS services.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use an IAM user.

## Connecting to my S3 bucket

The command I ran was aws s3 ls. This command is used to show the list of what is in the bucket.

The terminal responded with my vpc name. This indicated that the access keys I set up worked

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4334d778)

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://nextwork-vpc-project-komon which returned everything inside the bucket.

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4334d779)

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/nextwork.txt. This command creates a blank test file on my EC2 instance.

The second command I ran was aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-project-komon. This command uploads that file from my instance into my S3 bucket.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-komon again, which validated that the new file now appeared in the bucket.

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_3e1e79a2)

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will set up a way for your VPC and S3 to communicate direclty because that's the next step.

### Step 6 - Bucket policies

In your own words, start this step by explaining what you're about to do. We're going to block off your S3 bucket from ALL traffic except traffic coming from the endpoint as this will allow us to check whether or not we have set up our endpoints properly.



### Step 7 - Update route tables

In this step, I will test your VPC endpoint set up because we are troubleshooting a connectivity issue

### Step 8 - Validate endpoint conection

Validate endpoint connection In this step, I'll re-test my VPC endpoint setup, then test an endpoint policy by switching it from Allow to Deny to confirm it actually controls access before switching it back.

## Setting up a Gateway

I set up an S3 Gateway, which lets on-premises applications use standard file protocols to store and access data as objects in Amazon S3.

### What are endpoints?

An endpoint is a URL that serves as an entry point for a web service, allowing your applications, SDKs, or the AWS CLI to connect programmatically to AWS.

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_09bcaa8a)

## Bucket policies

A JSON policy controlling access to the bucket. Mine restricts access to only requests coming through my VPC endpoint.

My bucket policy will...

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_7316a13d)

## Bucket policies

Right after saving it, I got "access denied" — because the route table wasn't yet sending traffic through the endpoint, so nothing could get in, including me

I also had to update my route table because...

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4ec7821f)

## Route table updates

Associated my public route table with the Gateway endpoint, which automatically added a route sending S3-bound traffic to the endpoint instead of the internet. After that, aws s3 ls worked again.

After updating my public subnet's route table, my terminal could return...

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_d116818e)

## Endpoint policies

A policy on the endpoint itself, separate from the bucket's own policy. To test it, I switched the default "Allow" to "Deny" aws s3 ls immediately failed, proving the endpoint policy was actually controlling access.

I updated my endpoint's policy by... I could see the effect of this right away, because...

![Image](https://nextwork.ai/content_turquoise_clever_cumin/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_3e1e79a3)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/749fab76-0a0b-5822-9b31-c7863050c9bd)*
