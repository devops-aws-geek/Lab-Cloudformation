# Provisioning EC2 Instance using Cloudformation

## Pre-requiste
---
1. Use IDE like VS Code or IntelliJ if you wan to write cloudformation code locally.
---
2. Install git in your terminal
`Linux : sudo yum install git`
`Ubuntu : sudo apt install git`
`Windows install gitbash : https://git-scm.com/downloads`
---
3. git clone the lab repositories to the working folder or workspace, where you want to execute the cloudformation code
`git clone <repo>`
---
4. Create an IAM user in AWS console

i. Go to AWS consle and search for IAM service

![Alt text](image.png)

ii. Click on Users to create a user

![Alt text](image-1.png)

iii. Create a user  by giving some name and Adminstartor access permission to that user(Attach policy directly).

![Alt text](image-2.png)

![Alt text](image-3.png)

iv. Once user is created user will be visible in user page, click on that user and go to Security Credential as shown in images below. Create access key and download the csv file and save the Access key and Security key details in your system.

![Alt text](image-4.png)

![Alt text](image-5.png)

![Alt text](image-6.png)

![Alt text](image-7.png)

![Alt text](image-8.png)

5. Install awscli in your terminal ( I have used ubuntu OS as my terminal)
---
`curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"`
---
`sudo apt install unzip`
---
`sudo apt install unzip`
---
`sudo ./aws/install`
---
`aws --version`
---
Pass the IAM users access ID and Secret ID when asked. Rest all can be left as it is.

`aws configure`
---
Check the aws cli command, if no error then its working else you need to debug

`aws s3 ls`

## LAB Execution Command

**Lets execute the aws cloudformation command to provision the instance.**
`aws  --region us-east-1 cloudformation create-stack --stack-name stack-create-ec2-instance     --template-body file://ec2-create.yaml    --parameters ParameterKey=AvailabilityZone,ParameterValue=us-east-1a ParameterKey=EnvironmentType,ParameterValue=dev ParameterKey=AmiID,ParameterValue='/aws/service/canonical/ubuntu/server/jammy/stable/current/amd64/hvm/ebs-gp2/ami-id' ParameterKey=KeyPairName,ParameterValue=batch755   ParameterKey=LaunchUserData,ParameterValue=$(base64 -w0 install-web-server-ubuntu.sh)`