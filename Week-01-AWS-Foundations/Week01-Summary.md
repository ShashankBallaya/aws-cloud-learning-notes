## What I Built This Week 

This week I set up my AWS account from scratch altough I had been practising well before using the cloud labs provided by AWS. 
I built four core services hands-on, like I created IAM users for myself to avoid using the root-user, created groups for admin and roles for services and configured the AWS CLI on both Windows and Linux.
I launched my first EC2 instance, SSH'd into it, and served a custom webpage using Apache. Then I built an S3 static website with versioning and lifecycle rules. I created a custom VPC with a public subnet, Internet Gateway, and route table, and deliberately broke the routing to understand how it works.
I also completed Project 1 - a live HTTPS website on AWS using CloudFront and a private and a private s3 bucket with OAC.

## What Confused Me 

The biggest confusion was the CloudFront console - the new wizard had renamed Origin Access Control to "Allow private S3 bucket access to CloudFront", and I couldn't find the OAC option.
I learned that AWS regularly updates its console UI, and the official docs don't always match what you see. The fix was to select the S3 bucket from the dropdown. 
I also hit an issue with the AWS CLI on my Linux VM - it was installed but not configured. 
I also made a mistake as I got confused between `--` and `-` in the terminal, and have to build it a habit to write the CLI Commands properly.
AWS CLI commands are new to me, as I always preferred AWS Console. It was a bit difficult to find security groups if you have multiple, and which security group is associated with a public subnet, but I eventually figured it out.

## What I'm Most Proud Of 

Project 1 is live. A private S3 bucket serving a website through CloudFront over HTTPS - with S3 URL returning Access Denied. I built it entirely from scratch, debugged a console UI change in real time, and documented it properly on GitHub. That is a real production pattern, and I understand exactly why every step exists.

