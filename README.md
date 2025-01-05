# 🏗️ Jenkins Server Deployment on AWS EC2

> Automated Jenkins server deployment on AWS EC2 using CloudFormation

## 🌟 Key Features

- ⚡ Automated Jenkins installation
- ☕ Java 11 pre-installed
- 💾 Configurable EBS volume
- 🔒 Available encryption options
- 🛡️ Automatic security group creation
- 🔧 AWS CLI integration

## 📋 Prerequisites

- [x] AWS account with sufficient permissions
- [x] AWS CLI installed and configured
- [x] Existing SSH key pair in AWS
- [x] VPC and Subnet configured in AWS
- [x] Basic knowledge of AWS CloudFormation

## 📝 Información de Sistema Base

- 🐧 AMI Base: Amazon Linux 2023
- 🏷️ AMI ID: ami-0b4624933067d393a (us-east-2)
- 🔄 Versión del Sistema: Amazon Linux 2023 AMI 2023.6.20241212.0 x86_64 HVM kernel-6.1
- 📦 Características pre-instaladas:
  - systemd 252.4
  - yum package manager# 🏗️ Jenkins Server Deployment on AWS EC2

> Automated Jenkins server deployment on AWS EC2 using CloudFormation

## 🌟 Key Features

- ⚡ Automated Jenkins installation
- ☕ Java 11 pre-installed
- 💾 Configurable EBS volume
- 🔒 Available encryption options
- 🛡️ Automatic security group creation
- 🔧 AWS CLI integration

## 📋 Prerequisites

- [x] AWS account with sufficient permissions
- [x] AWS CLI installed and configured
- [x] Existing SSH key pair in AWS
- [x] VPC and Subnet configured in AWS
- [x] Basic knowledge of AWS CloudFormation

## 📝 Base System Information

- 🐧 Base AMI: Amazon Linux 2023
- 🏷️ AMI ID: ami-0b4624933067d393a (us-east-2)
- 🔄 System Version: Amazon Linux 2023 AMI 2023.6.20241212.0 x86_64 HVM
  - aws-cli v2

### 🔍 Compatibility Notes

This implementation is optimized for Amazon Linux 2023. This distribution is recommended due to:

- Native integration with AWS services
- Cloud optimization
- Regular security updates
- LTS support

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
# Desplegar stack
aws cloudformation create-stack \
    --stack-name jenkins-server \
    --template-body file://jenkins-template.yaml \
    --parameters ParameterKey=KeyName,ParameterValue=mi-keypair

# Verificar estado
aws cloudformation describe-stacks \
    --stack-name jenkins-server

# Actualizar stack
aws cloudformation update-stack \
    --stack-name jenkins-server \
    --template-body file://jenkins-template.yaml

# Eliminar stack
aws cloudformation delete-stack \
    --stack-name jenkins-server
```

3. Connect Ec2 Instance

```bash
ssh -i "<name-key>.pem" ec2-user@<public-ip>.<region>.compute.amazonaws.com
```

4. Get Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

5. Accessing Jenkins

Wait approximately 5-10 minutes after deployment
Access Jenkins using:

```
http://<public-ip>:8080
```

#### Note : In the output could find public DNS link

## 🔐 Security

The instance is deployed with a security group that allows:

- Port 22 (SSH)
- Port 8080 (Jenkins UI)
It is recommended to modify JenkinsAllowSSHFrom to restrict SSH access

## 🔧 Maintenance

### Log Access

```bash
sudo tail -f /var/log/deploy.log
```

## 📄 Release Notes v1.0.0

- Automated Jenkins installation
- Support for Amazon Linux 2023
- AWS CLI integration

## 🔄 Updates

To update Jenkins:

```bash
sudo yum update jenkins -y
sudo systemctl restart jenkins
```

## 🤝 Contributions

Contributions are welcome. Please:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## 📝 License

This project is under the MIT License - see the LICENSE file for details

## ✒️ Author

Andres Jose Sanchez - Initial Development - [andresjose84@gmail.com]
