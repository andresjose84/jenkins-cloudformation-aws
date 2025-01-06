# 🏰 Jenkins Server Deployment on AWS EC2

> Automated Jenkins server deployment on AWS EC2 using CloudFormation

## 🌟 Key Features

- ⚡ Automated Jenkins installation
- ☕ Java 17 pre-installed
- 📀 Configurable EBS volume
- 🔒 Available encryption options
- 🛡️ Automatic security group creation
- 🔧 AWS CLI integration
- 🏢 Subdomain registration with Route 53
- ⚠️ SSL certificate configuration using Certbot
- ⤵️ Nginx reverse proxy setup
- 🔃 Automatic SSL certificate renewal

## 👌 Prerequisites

- [x] AWS account with sufficient permissions
- [x] AWS CLI installed and configured
- [x] Existing SSH key pair in AWS
- [x] VPC and Subnet configured in AWS
- [x] Basic knowledge of AWS CloudFormation

## 📜 Base System Information

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

| Parameter              | Description                                     | Default Value         |
|------------------------|-------------------------------------------------|-----------------------|
| AWSRegion             | AWS Region for deployment                      | us-east-1            |
| JenkinsInstanceType   | EC2 instance type                               | t2.micro             |
| JenkinsVolumeSize     | EBS volume size (GB)                            | 16                   |
| JenkinsAllowSSHFrom   | CIDR for SSH access                             | 0.0.0.0/0            |
| DomainName            | Subdomain for Jenkins                          | jenkins.example.com  |
| SSLCertificateEmail   | Email for SSL certificate notifications         | admin@example.com    |

## 🚀 Deployment

1. Clone the repository:

```bash
git clone <repository-URL>
```

2. Deploy the CloudFormation stack:

```bash
# Deploy stack
aws cloudformation create-stack \
    --stack-name jenkins-server \
    --template-body file://template.yaml \
    --parameters ParameterKey=KeyName,ParameterValue=mi-keypair

# Check status
aws cloudformation describe-stacks \
    --stack-name jenkins-server

# Update stack
aws cloudformation update-stack \
    --stack-name jenkins-server \
    --template-body file://template.yaml

# Delete stack
aws cloudformation delete-stack \
    --stack-name jenkins-server
```

3. Connect to the EC2 Instance:

```bash
ssh -i "<name-key>.pem" ec2-user@<public-ip>.<region>.compute.amazonaws.com
```

4. Get the Jenkins Admin Password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

5. Access Jenkins:

- Wait approximately 5-10 minutes after deployment.
- Access Jenkins using:

```
https://jenkins.example.com
```

## 🔐 Security

The instance is deployed with a security group that allows:

- Port 22 (SSH)
- Port 80 (HTTP)
- Port 443 (HTTPS)
- Port 8080 (Jenkins UI)

It is recommended to modify JenkinsAllowSSHFrom to restrict SSH access.

## 🔧 Maintenance

### Log Access

```bash
sudo tail -f /var/log/deploy.log
```

### SSL Certificate Renewal

- Automatic renewal is configured with Certbot.
- To manually renew the SSL certificate, run:

```bash
sudo certbot renew
```

- Test the renewal process:

```bash
sudo certbot renew --dry-run
```

## 📄 Release Notes v1.1.0

- Added subdomain registration with Route 53
- Configured SSL certificate with Certbot
- Implemented Nginx as a reverse proxy
- Automated SSL certificate renewal with Certbot

## 🤝 Contributions

Contributions are welcome. Please:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## 📝 License

This project is under the MIT License - see the LICENSE file for details.

## ✍️ Author

Andres Jose Sanchez - Initial Development - [andresjose84@gmail.com]

