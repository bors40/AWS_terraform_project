# AWS_tf_project
AWS terraform project

This file creates these resources
Provider = AWS
Network = VPC, IG, Subnet, RT, RTA, EIP, SG
S3 buckets
LB = TG, TGA, LB, LB_listeners
Default Page = ami Data Block, ec2
Autoscaling = LC, ASP, ASG, CWM, ASA

Steps to create Jenkins Master ec2
1- Spin up a ec2 instance
2- Attach an eip to the ec2 instance
3- Create an IAM role as adminaccess for the ec2 instance and attach it.
4- Install jenkins on ec2
https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/
https://exerror.com/error-package-jenkins-2-306-1-1-noarch-jenkins-requires-daemonize/
systemctl status jenkins
5- Install terraform on the ec2 instance.
https://learn.hashicorp.com/tutorials/terraform/install-cli
terraform --help
6- Install git on the ec2 instance
sudo yum install git 
git --help
7- Add port 8080 in the inbound rules.

Copy the Public IPv4 address of ec2 and paste on the browser:
http://Public-IPv4-address:8080

Jenkins Plugins needs to installed
1- Terraform Plugin
2- GitHub Authentication plugin
3- GitHub Integration Plugin
4- GitHub plugin

Github integration to Jenkins
Dashboard > Manage Jenkins > Manage Credentials > Jenkins > Global Credentials > Add Credentials

Pipeline job