# Packer AMI Builder with Apache Web Server

This project automates the creation of custom Amazon Machine Images (AMIs) using HashiCorp Packer. The resulting AMI includes a pre-configured Apache HTTP server that displays custom content.

## 📋 Prerequisites

Before you begin, ensure you have the following:

- **AWS Account** with appropriate IAM permissions
- **AWS CLI** installed and configured
- **Packer** installed (version 1.2.8 or higher)
- **Terraform** (optional, for infrastructure deployment)
- Valid AWS credentials configured locally

### Required IAM Permissions

Your AWS user/role needs the following permissions:
- EC2: CreateImage, DescribeImages, RunInstances, TerminateInstances
- EC2: CreateSecurityGroup, AuthorizeSecurityGroupIngress
- EC2: CreateKeyPair, DeleteKeyPair


## 🚀 Quick Start

### 1. Clone or Create Project Directory

```bash
mkdir packer-ami-project
cd packer-ami-project
```
## 📁 Project Structure

```
packer-ami-project/
├── webserver.pkr.hcl      # Packer configuration template
├── install_httpd.sh       # Apache installation script
├── main.tf                # Terraform infrastructure (optional)
├── ami_manifest.json      # Generated AMI details (after build)
└── README.md              # This file
```

### 2. Create Required Files

Create the following files in your project directory:

- `webserver.pkr.hcl` - Packer configuration template
- `install_httpd.sh` - Apache installation script
- `main.tf` - Terraform configuration (optional)

### 3. Configure AWS Credentials

```bash
aws configure
```

Enter your AWS Access Key ID, Secret Access Key, and default region.

### 4. Initialize Packer

```bash
packer init .
```

### 5. Validate Configuration

```bash
packer fmt .
packer validate webserver.pkr.hcl
```

### 6. Build the AMI

```bash
packer build webserver.pkr.hcl
```

The build process takes approximately 4-5 minutes.

```
$ packer build webserver.pkr.hcl
ami-packer.amazon-ebs.al2023: output will be in this color.

==> ami-packer.amazon-ebs.al2023: Prevalidating any provided VPC information
==> ami-packer.amazon-ebs.al2023: Prevalidating AMI Name: packer-linux-aws-20260
113055908
==> ami-packer.amazon-ebs.al2023: Found Image ID: ami-0a864d7e31fe76819
==> ami-packer.amazon-ebs.al2023: Creating temporary keypair: packer_6965df2c-46
0d-b29c-a33f-23a46e503725
==> ami-packer.amazon-ebs.al2023: Creating temporary security group for this ins
tance: packer_6965df2d-c320-4922-bba3-288087a27a96
==> ami-packer.amazon-ebs.al2023: Authorizing access to port 22 from [0.0.0.0/0]
 in the temporary security groups...
==> ami-packer.amazon-ebs.al2023: Launching a source AWS instance...
==> ami-packer.amazon-ebs.al2023: Instance ID: i-0795e504e4df305e3
==> ami-packer.amazon-ebs.al2023: Waiting for instance (i-0795e504e4df305e3) to
become ready...
==> ami-packer.amazon-ebs.al2023: Using SSH communicator to connect: 34.222.65.1
27
==> ami-packer.amazon-ebs.al2023: Waiting for SSH to become available...
==> ami-packer.amazon-ebs.al2023: Connected to SSH!
==> ami-packer.amazon-ebs.al2023: Provisioning with shell script: install_httpd.
sh
==> ami-packer.amazon-ebs.al2023: Waiting for process with pid 1987 to finish.
==> ami-packer.amazon-ebs.al2023: Amazon Linux 2023 Kernel Livepatch repository
   99 kB/s |  30 kB     00:00
==> ami-packer.amazon-ebs.al2023: Last metadata expiration check: 0:00:01 ago on
 Tue Jan 13 06:00:57 2026.
==> ami-packer.amazon-ebs.al2023: Dependencies resolved.
==> ami-packer.amazon-ebs.al2023: Nothing to do.
==> ami-packer.amazon-ebs.al2023: Complete!
==> ami-packer.amazon-ebs.al2023: Last metadata expiration check: 0:00:11 ago on
 Tue Jan 13 06:00:57 2026.
==> ami-packer.amazon-ebs.al2023: Dependencies resolved.
==> ami-packer.amazon-ebs.al2023: ==============================================
==================================
==> ami-packer.amazon-ebs.al2023:  Package               Arch     Version
              Repository     Size
==> ami-packer.amazon-ebs.al2023: ==============================================
==================================
==> ami-packer.amazon-ebs.al2023: Installing:
==> ami-packer.amazon-ebs.al2023:  httpd                 x86_64   2.4.66-1.amzn2
023.0.1       amazonlinux    47 k
==> ami-packer.amazon-ebs.al2023: Installing dependencies:
==> ami-packer.amazon-ebs.al2023:  apr                   x86_64   1.7.5-1.amzn20
23.0.4        amazonlinux   129 k
==> ami-packer.amazon-ebs.al2023:  apr-util              x86_64   1.6.3-1.amzn20
23.0.2        amazonlinux    97 k
==> ami-packer.amazon-ebs.al2023:  apr-util-lmdb         x86_64   1.6.3-1.amzn20
23.0.2        amazonlinux    13 k
==> ami-packer.amazon-ebs.al2023:  generic-logos-httpd   noarch   18.0.0-12.amzn
2023.0.3      amazonlinux    19 k
==> ami-packer.amazon-ebs.al2023:  httpd-core            x86_64   2.4.66-1.amzn2
023.0.1       amazonlinux   1.4 M
==> ami-packer.amazon-ebs.al2023:  httpd-filesystem      noarch   2.4.66-1.amzn2
023.0.1       amazonlinux    13 k
==> ami-packer.amazon-ebs.al2023:  httpd-tools           x86_64   2.4.66-1.amzn2
023.0.1       amazonlinux    81 k
==> ami-packer.amazon-ebs.al2023:  libbrotli             x86_64   1.0.9-4.amzn20
23.0.2        amazonlinux   315 k
==> ami-packer.amazon-ebs.al2023:  mailcap               noarch   2.1.49-3.amzn2
023.0.3       amazonlinux    33 k
==> ami-packer.amazon-ebs.al2023: Installing weak dependencies:
==> ami-packer.amazon-ebs.al2023:  apr-util-openssl      x86_64   1.6.3-1.amzn20
23.0.2        amazonlinux    15 k
==> ami-packer.amazon-ebs.al2023:  mod_http2             x86_64   2.0.27-1.amzn2
023.0.3       amazonlinux   166 k
==> ami-packer.amazon-ebs.al2023:  mod_lua               x86_64   2.4.66-1.amzn2
023.0.1       amazonlinux    60 k
==> ami-packer.amazon-ebs.al2023:
==> ami-packer.amazon-ebs.al2023: Transaction Summary
==> ami-packer.amazon-ebs.al2023: ==============================================
==================================
==> ami-packer.amazon-ebs.al2023: Install  13 Packages
==> ami-packer.amazon-ebs.al2023:
==> ami-packer.amazon-ebs.al2023: Total download size: 2.4 M
==> ami-packer.amazon-ebs.al2023: Installed size: 6.9 M
==> ami-packer.amazon-ebs.al2023: Downloading Packages:
==> ami-packer.amazon-ebs.al2023: (1/13): apr-util-lmdb-1.6.3-1.amzn2023.0.2.x86
_ 162 kB/s |  13 kB     00:00
==> ami-packer.amazon-ebs.al2023: (2/13): apr-util-1.6.3-1.amzn2023.0.2.x86_64.r
p 1.1 MB/s |  97 kB     00:00
==> ami-packer.amazon-ebs.al2023: (3/13): apr-1.7.5-1.amzn2023.0.4.x86_64.rpm
  1.4 MB/s | 129 kB     00:00
==> ami-packer.amazon-ebs.al2023: (4/13): apr-util-openssl-1.6.3-1.amzn2023.0.2.
x 646 kB/s |  15 kB     00:00
==> ami-packer.amazon-ebs.al2023: (5/13): generic-logos-httpd-18.0.0-12.amzn2023
. 621 kB/s |  19 kB     00:00
==> ami-packer.amazon-ebs.al2023: (6/13): httpd-2.4.66-1.amzn2023.0.1.x86_64.rpm
  1.4 MB/s |  47 kB     00:00
==> ami-packer.amazon-ebs.al2023: (7/13): httpd-core-2.4.66-1.amzn2023.0.1.x86_6
4  22 MB/s | 1.4 MB     00:00
==> ami-packer.amazon-ebs.al2023: (8/13): httpd-filesystem-2.4.66-1.amzn2023.0.1
. 238 kB/s |  13 kB     00:00
==> ami-packer.amazon-ebs.al2023: (9/13): httpd-tools-2.4.66-1.amzn2023.0.1.x86_
6 1.5 MB/s |  81 kB     00:00
==> ami-packer.amazon-ebs.al2023: (10/13): libbrotli-1.0.9-4.amzn2023.0.2.x86_64
.  13 MB/s | 315 kB     00:00
==> ami-packer.amazon-ebs.al2023: (11/13): mailcap-2.1.49-3.amzn2023.0.3.noarch.
r 1.5 MB/s |  33 kB     00:00
==> ami-packer.amazon-ebs.al2023: (12/13): mod_http2-2.0.27-1.amzn2023.0.3.x86_6
4 2.5 MB/s | 166 kB     00:00
==> ami-packer.amazon-ebs.al2023: (13/13): mod_lua-2.4.66-1.amzn2023.0.1.x86_64.
r 1.2 MB/s |  60 kB     00:00
==> ami-packer.amazon-ebs.al2023: ----------------------------------------------
----------------------------------
==> ami-packer.amazon-ebs.al2023: Total
  6.0 MB/s | 2.4 MB     00:00
==> ami-packer.amazon-ebs.al2023: Running transaction check
==> ami-packer.amazon-ebs.al2023: Transaction check succeeded.
==> ami-packer.amazon-ebs.al2023: Running transaction test
==> ami-packer.amazon-ebs.al2023: Transaction test succeeded.
==> ami-packer.amazon-ebs.al2023: Running transaction
==> ami-packer.amazon-ebs.al2023:   Preparing        :
                              1/1
==> ami-packer.amazon-ebs.al2023:   Installing       : apr-1.7.5-1.amzn2023.0.4.
x86_64                       1/13
==> ami-packer.amazon-ebs.al2023:   Installing       : apr-util-lmdb-1.6.3-1.amz
n2023.0.2.x86_64             2/13
==> ami-packer.amazon-ebs.al2023:   Installing       : apr-util-openssl-1.6.3-1.
amzn2023.0.2.x86_64          3/13
==> ami-packer.amazon-ebs.al2023:   Installing       : apr-util-1.6.3-1.amzn2023
.0.2.x86_64                  4/13
==> ami-packer.amazon-ebs.al2023:   Installing       : mailcap-2.1.49-3.amzn2023
.0.3.noarch                  5/13
==> ami-packer.amazon-ebs.al2023:   Installing       : httpd-tools-2.4.66-1.amzn
2023.0.1.x86_64              6/13
==> ami-packer.amazon-ebs.al2023:   Installing       : libbrotli-1.0.9-4.amzn202
3.0.2.x86_64                 7/13
==> ami-packer.amazon-ebs.al2023:   Running scriptlet: httpd-filesystem-2.4.66-1
.amzn2023.0.1.noarch         8/13
==> ami-packer.amazon-ebs.al2023:   Installing       : httpd-filesystem-2.4.66-1
.amzn2023.0.1.noarch         8/13
==> ami-packer.amazon-ebs.al2023:   Installing       : httpd-core-2.4.66-1.amzn2
023.0.1.x86_64               9/13
==> ami-packer.amazon-ebs.al2023:   Installing       : mod_http2-2.0.27-1.amzn20
23.0.3.x86_64               10/13
==> ami-packer.amazon-ebs.al2023:   Installing       : mod_lua-2.4.66-1.amzn2023
.0.1.x86_64                 11/13
==> ami-packer.amazon-ebs.al2023:   Installing       : generic-logos-httpd-18.0.
0-12.amzn2023.0.3.noarch    12/13
==> ami-packer.amazon-ebs.al2023:   Installing       : httpd-2.4.66-1.amzn2023.0
.1.x86_64                   13/13
==> ami-packer.amazon-ebs.al2023:   Running scriptlet: httpd-2.4.66-1.amzn2023.0
.1.x86_64                   13/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : apr-1.7.5-1.amzn2023.0.4.
x86_64                       1/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : apr-util-1.6.3-1.amzn2023
.0.2.x86_64                  2/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : apr-util-lmdb-1.6.3-1.amz
n2023.0.2.x86_64             3/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : apr-util-openssl-1.6.3-1.
amzn2023.0.2.x86_64          4/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : generic-logos-httpd-18.0.
0-12.amzn2023.0.3.noarch     5/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : httpd-2.4.66-1.amzn2023.0
.1.x86_64                    6/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : httpd-core-2.4.66-1.amzn2
023.0.1.x86_64               7/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : httpd-filesystem-2.4.66-1
.amzn2023.0.1.noarch         8/13
==> ami-packer.amazon-ebs.al2023:   Verifying        : httpd-tools-2.4.66-1.amzn
==> ami-packer.amazon-ebs.al2023:   mod_lua-2.4.66-1.amzn2023.0.1.x86_64
==> ami-packer.amazon-ebs.al2023:
==> ami-packer.amazon-ebs.al2023: Complete!
==> ami-packer.amazon-ebs.al2023: Created symlink /etc/systemd/system/multi-user.target.wants/httpd.service → /usr/lib/systemd/system/httpd.service.
==> ami-packer.amazon-ebs.al2023:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
==> ami-packer.amazon-ebs.al2023:                                  Dload  Upload   Total   Spent    Left  Speed
==> ami-packer.amazon-ebs.al2023: 100    56  100    56    0     0  30172      0 --:--:-- --:--:-- --:--:-- 56000
==> ami-packer.amazon-ebs.al2023: Stopping the source instance...
==> ami-packer.amazon-ebs.al2023: Stopping instance
==> ami-packer.amazon-ebs.al2023: Waiting for the instance to stop...
==> ami-packer.amazon-ebs.al2023: Creating AMI packer-linux-aws-20260113055908 from instance i-0795e504e4df305e3
==> ami-packer.amazon-ebs.al2023: Attaching run tags to AMI...
==> ami-packer.amazon-ebs.al2023: AMI: ami-0f77ca477385bf1bf
==> ami-packer.amazon-ebs.al2023: Waiting for AMI to become ready...
==> ami-packer.amazon-ebs.al2023: Skipping Enable AMI deprecation...
==> ami-packer.amazon-ebs.al2023: Skipping Enable AMI deregistration protection...
==> ami-packer.amazon-ebs.al2023: Terminating the source AWS instance...
==> ami-packer.amazon-ebs.al2023: Cleaning up any extra volumes...
==> ami-packer.amazon-ebs.al2023: No volumes to clean up, skipping
==> ami-packer.amazon-ebs.al2023: Deleting temporary security group...
==> ami-packer.amazon-ebs.al2023: Deleting temporary keypair...
==> ami-packer.amazon-ebs.al2023: Running post-processor:  (type manifest)
Build 'ami-packer.amazon-ebs.al2023' finished after 5 minutes 46 seconds.

==> Wait completed after 5 minutes 46 seconds

==> Builds finished. The artifacts of successful builds are:
--> ami-packer.amazon-ebs.al2023: AMIs were created:
us-west-2: ami-0f77ca477385bf1bf

--> ami-packer.amazon-ebs.al2023: AMIs were created:
us-west-2: ami-0f77ca477385bf1bf


```


## 🔧 Configuration

### Packer Template (`webserver.pkr.hcl`)

Key configuration parameters:

- **Region**: `us-west-2` (modify as needed)
- **Instance Type**: `t3.micro` (free tier eligible)
- **Base AMI**: Amazon Linux 2023
- **SSH Username**: `ec2-user`

To change the region or instance type, edit these lines:

```hcl
source "amazon-ebs" "al2023" {
  instance_type = "t3.micro"       # Change instance type here
  region        = "us-west-2"      # Change region here
  # ... rest of configuration
}
```

### Installation Script (`install_httpd.sh`)

The script performs the following actions:
1. Updates system packages
2. Installs Apache HTTP Server
3. Starts and enables Apache service
4. Creates a custom HTML page displaying the AMI ID

## 🖥️ Deploying EC2 Instances


```bash
# Get your AMI_ID="ami-xxxxxxxxx" from the build output(ami_manifest.json in the artifact_id)
{
  "builds": [
    {
      "name": "al2023",
      "builder_type": "amazon-ebs",
      "build_time": 1768284294,
      "files": null,
      "artifact_id": "us-west-2:ami-0f77ca477385bf1bf",
      "packer_run_uuid": "ae5ebd34-f056-7110-dd68-7bc94bc3b0a0",
      "custom_data": null
    }
  ],
  "last_run_uuid": "ae5ebd34-f056-7110-dd68-7bc94bc3b0a0"
}
```
<img src='pictures/AMIimage.png'>

Use the provided `main.tf` configuration:

```bash
terraform init
terraform plan
terraform apply
```

Update the AMI ID in `main.tf`:

```hcl
resource "aws_instance" "ec2" {
  ami = "ami-xxxxxxxxx"  # Replace with your Packer-built AMI ID
  # ... rest of configuration
}
```

## 🔐 SSH Access

### Connect to Your Instance

```bash
# SSH to the instance
ssh -i EC2_Keypair.pem ubuntu@<PUBLIC_IP>
```
<img src='pictures/SSHLogin.png'>

**Note**: For Amazon Linux 2023 AMIs, use `ec2-user` instead of `ubuntu`:

```bash
ssh -i EC2_Keypair.pem ec2-user@<PUBLIC_IP>
```


## 🧹 Cleanup

To avoid unnecessary AWS charges:

### 1. Terminate EC2 Instances
```
# Using Terraform
terraform destroy
```

### 2. Deregister AMI

Deregister the AMI if no longer needed:





**Built with ❤️ using HashiCorp Packer**
