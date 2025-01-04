# 🏗️ Jenkins Server Deployment on AWS EC2

> Automated Jenkins server deployment on AWS EC2 using CloudFormation

## 🌟 Key Features

- ⚡ Automated Jenkins installation
- ☕ Java 11 pre-installed
- 💾 Configurable EBS volume
- 🔒 Available encryption options
- 🛡️ Automatic security group creation

## 📋 Prerequisites

- [x] AWS account with sufficient permissions
- [x] AWS CLI installed and configured
- [x] Existing SSH key pair in AWS
- [x] VPC and Subnet configured in AWS
- [x] Basic knowledge of AWS CloudFormation

## ⚙️ Main Parameters

| Parameter | Description | Default Value |
|-----------|-------------|---------------|
| AWSRegion | AWS Region for deployment | us-east-1 |
| JenkinsInstanceType | EC2 instance type | t2.micro |
| JenkinsVolumeSize | EBS volume size (GB) | 16 |
| JenkinsAllowSSHFrom | CIDR for SSH access | 0.0.0.0/0 |

## 🚀 Deployment

1. Clone the repository:
```bash
git clone <repository-URL>
```

2. Deploy the CloudFormation stack:

```bash
aws cloudformation create-stack \
  --stack-name jenkins-server \
  --template-body file://template.yaml \
  --parameters \
    ParameterKey=JenkinsKeyPair,ParameterValue=<your-key-pair> \
    ParameterKey=JenkinsVpc,ParameterValue=<your-vpc-id> \
    ParameterKey=JenkinsSubnet,ParameterValue=<your-subnet-id>
```

🔐 Security
The instance is deployed with a security group that allows:
Port 22 (SSH)
Port 8080 (Jenkins UI)
It is recommended to modify JenkinsAllowSSHFrom to restrict SSH access

🔍 Accessing Jenkins
Wait approximately 5-10 minutes after deployment
Access Jenkins using:
```
http://<public-ip>:8080
```

📝 License
This project is under the MIT License - see the LICENSE file for details

✒️ Author
Andres Jose Sanchez - Initial Development - [andresjose84@gmail.com]
