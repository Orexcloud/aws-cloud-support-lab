### AWS Cloud Support Lab

This repository documents a hands-on AWS lab I built to refresh my cloud support skills and practise working through common infrastructure, Linux, networking, monitoring and troubleshooting tasks.

Rather than using the default AWS network, I built a small environment from the VPC level up, launched an Amazon Linux EC2 instance, deployed an Apache web server and used CloudWatch to monitor and test the instance.

I also documented the problems I encountered during the build and a simulated web server outage.

### Environment

The lab included:

* Custom VPC (`10.0.0.0/16`)
* Public subnet (`10.0.1.0/24`)
* Internet Gateway and custom route table
* EC2 security group with restricted SSH access
* Amazon Linux 2023 EC2 instance
* Apache HTTP server
* CloudWatch EC2 monitoring and CPU alarm
* SNS topic for alarm notification testing
* IAM review and security checks

The EC2 instance was accessed over SSH from Windows PowerShell.

### What I worked on

#### Networking

I created the VPC and public subnet, attached an Internet Gateway and configured a route to allow internet connectivity.

SSH access was restricted to my current public IPv4 address using a `/32` security group rule rather than exposing port 22 to all addresses.

[View VPC setup](documentation/vpc-setup.md)

#### EC2 and Linux

I launched an Amazon Linux 2023 EC2 instance and connected to it using SSH from Windows.

On the instance I checked system resources, storage, CPU information, interfaces and routing before installing and configuring Apache.

I created a simple web page and made it accessible over HTTP.

[View EC2 and web server setup](documentation/ec2-setup.md)

#### Monitoring

I used the standard EC2 `CPUUtilization` metric in CloudWatch to establish a baseline and then generated controlled CPU load using `stress-ng`.

I created a CloudWatch alarm with a 70% CPU threshold and observed it move through:

`OK -> In alarm -> OK`

An SNS email notification was also configured during testing. The CloudWatch alarm worked, but the email subscription did not remain subscribed, so email delivery was not recorded as a successful part of the test.

[View monitoring notes](documentation/monitoring.md)

#### Troubleshooting

Some of the most useful parts of the lab came from troubleshooting problems rather than the initial setup.

I worked through:

* an SSH timeout caused by my public IP changing while the security group was restricted to the previous `/32` address
* an Apache `403 Forbidden` response caused by an empty document root
* a simulated website outage where Apache was inactive and nothing was listening on TCP port 80

For the simulated outage, I worked from the client symptom through the Linux service and listening port checks before restoring the service and confirming external access.

[View troubleshooting notes](documentation/troubleshooting.md)

#### IAM

I also reviewed IAM configuration and documented the security checks performed as part of the lab.

[View IAM notes](documentation/iam-security.md)

### Evidence

Screenshots from the build and troubleshooting exercises are stored in the [`screenshots`](screenshots/) directory.

They include VPC and subnet configuration, EC2/SSH access, Apache testing, CloudWatch CPU metrics and the triggered CPU alarm.

### Cleanup

After completing the lab, I terminated the EC2 instance and removed the lab resources I no longer needed, including the EBS volume, CloudWatch alarm, SNS topic, security group, subnet, route table, Internet Gateway and VPC.

This was also part of the exercise: checking for resources that could continue generating AWS charges after the lab was finished.

### Background

I'm an AWS Certified Solutions Architect – Associate working towards a career in cloud support and cloud operations.

This is a personal learning project, so the repository reflects my own hands-on practice, troubleshooting and notes rather than a production environment.
