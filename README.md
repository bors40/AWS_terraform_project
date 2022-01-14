# AWS_tf_project
AWS terraform project

This repo creates these resources
Provider = AWS
Network = VPC, IG, Subnet, RT, RTA, EIP, SG
S3 buckets
LB = TG, TGA, LB, LB_listeners
Default Page = ami Data Block, ec2
Autoscaling = LC, ASP, ASG, CWM, ASA

Steps to create Jenkins Master ec2
- Spin up a ec2 instance
- Attach an eip to the ec2 instance
- Create an IAM role as adminaccess for the ec2 instance and attach it.
- Install jenkins on ec2
    - https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/
    - https://exerror.com/error-package-jenkins-2-306-1-1-noarch-jenkins-requires-daemonize/
    - systemctl status jenkins
- Install terraform on the ec2 instance.
    - https://learn.hashicorp.com/tutorials/terraform/install-cli
    - terraform --help
- Install git on the ec2 instance
    - sudo yum install git 
    - git --help
- Add port 8080 in the inbound rules.

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
- Click on New Item on the dashboard > Give a name for your project
- Click on pipeline and save
- Under the General tab
    - Click on This project is parameterized
    - Name = action
    - Choices = 
        plan
        apply
        destroy
    - Description = Do you want to perform Plan, Apply or Destroy?

- Scroll all the way down to the Pipeline script
    here is a sample script

pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bors40/AWS_terraform_project.git']]])
            }
        }
        
        stage('terraform init') {
            steps {
                sh ("terraform init");
            }    
        }
        
        stage('terraform Action') {
            steps {
                echo "terraform action from the parameter is --> ${action}"
                sh ("terraform ${action}");
            }    
        }        
        
    }
}

- Apply and Save
- Go to dashboard and click on the pipeline job
- Click on Build with Parameters
- THEN THE MOMENT OF TRUTH by Burhan