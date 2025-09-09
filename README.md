# AWS Web Server Infrastructure with Terraform

This project creates a complete AWS infrastructure for hosting a web server using Terraform. It provisions a VPC with a public subnet and deploys an EC2 instance configured with Apache web server.

## Architecture

```
Internet Gateway
       |
   Public Subnet (10.0.1.0/24)
       |
   EC2 Instance (Apache Web Server)
       |
   Security Group (HTTP + SSH)
```

## Infrastructure Components

- **VPC**: Custom Virtual Private Cloud (10.0.0.0/16)
- **Public Subnet**: Internet-accessible subnet (10.0.1.0/24)
- **Internet Gateway**: Enables internet connectivity
- **Route Table**: Routes traffic between subnet and internet
- **Security Group**: Firewall rules (HTTP port 80, SSH port 22)
- **EC2 Instance**: Amazon Linux 2023 with Apache web server

## File Structure

```
├── provider.tf      # Terraform and AWS provider configuration
├── variables.tf     # Variable definitions with defaults
├── terraform.tfvars # Actual values for variables
├── network.tf       # VPC, subnet, gateway, routing
├── security.tf      # Security group configuration
├── compute.tf       # EC2 instance with user data
├── outputs.tf       # Infrastructure output values
└── main.tf          # Additional configuration (optional)
```

## Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/downloads) installed
- AWS CLI configured with credentials
- AWS account with appropriate permissions

## Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/sefira/terraform-aws-webserver.git
   cd terraform-aws-webserver
   ```

2. **Customize variables** (optional)
   Edit `terraform.tfvars` to modify:
   ```hcl
   region = "us-west-2"
   instance_type = "t3.micro"
   ```

3. **Deploy infrastructure**
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

4. **Access your web server**
   - Get the public IP from output
   - Visit `http://PUBLIC_IP` in your browser

5. **Clean up**
   ```bash
   terraform destroy
   ```
   
### Outputs

- `vpc_id`: ID of the created VPC
- `public_subnet_id`: ID of the public subnet
- `instance_public_ip`: Public IP address of web server

## Real-World Use Cases

### 1. **Development Environment**
- Quick setup for testing web applications
- Isolated environment for each developer
- Cost-effective with t2.micro (free tier eligible)

### 2. **Proof of Concept (PoC)**
- Demonstrate web application to stakeholders
- Rapid prototyping and iteration
- Easy teardown after presentation

### 3. **Learning Platform**
- Educational projects for cloud computing
- Terraform infrastructure-as-code training
- AWS services hands-on experience

### 4. **Small Business Website**
- Simple company website or blog
- Low-traffic applications
- Cost-effective hosting solution

### 5. **CI/CD Pipeline Foundation**
- Base infrastructure for deployment pipelines
- Staging environment for testing
- Blue-green deployment setup foundation

### 6. **Microservices Testing**
- Individual service deployment
- Load testing environment
- Service mesh experimentation

### 7. **Static Website Hosting**
- Portfolio websites
- Documentation sites
- Landing pages

## Production Considerations

For production use, consider adding:

- **Load Balancer**: Distribute traffic across multiple instances
- **Auto Scaling**: Handle traffic spikes automatically
- **Private Subnets**: Database and backend services
- **NAT Gateway**: Outbound internet for private resources
- **SSL/TLS**: HTTPS encryption with ACM certificates
- **CloudWatch**: Monitoring and logging
- **Backup Strategy**: EBS snapshots and data protection
- **Multi-AZ**: High availability across zones

## Security Best Practices

- Restrict SSH access to specific IP ranges
- Use IAM roles instead of hardcoded credentials
- Enable VPC Flow Logs for network monitoring
- Implement least privilege access policies
- Regular security updates via user data scripts

## Cost Optimization

- Use t2.micro for free tier eligibility
- Implement auto-shutdown for development environments
- Monitor usage with AWS Cost Explorer
- Consider Reserved Instances for long-term use

## Troubleshooting

### Common Issues

1. **Provider download fails**: Network connectivity to Terraform registry
2. **Permission denied**: Check AWS credentials and IAM permissions
3. **Resource conflicts**: Ensure unique resource names
4. **Web server not accessible**: Verify security group rules

### Useful Commands

```bash
# Check Terraform version
terraform version

# Validate configuration
terraform validate

# Format code
terraform fmt

# Show current state
terraform show

# List resources
terraform state list
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request
