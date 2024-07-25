# AWS-Jenkins-Pipeline

## Setting up a CI/CD pipeline by integrating Jenkins with AWS CodeBuild and AWS CodeDeploy
 
 
 
 Jenkins open-source automation server is used to deploy AWS CodeBuild artifacts with AWS CodeDeploy, creating a functioning CI/CD pipeline. 
 When properly implemented, the CI/CD pipeline is triggered by code changes pushed to your GitHub repo, automatically fed into CodeBuild, then the output is deployed on CodeDeploy.
  
 
The functioning pipeline creates a fully managed build service that compiles your source code. It then produces code artifacts that can be used by CodeDeploy to deploy to your production environment automatically.


![image](https://user-images.githubusercontent.com/48589838/89983289-e5fc2900-dc94-11ea-9258-685375cad1dd.png)



### Walkthrough 

Creating resources to build the infrastructure, including the Jenkins server, CodeBuild project, and CodeDeploy application.

Accessing and unlocking the Jenkins server.

Creating a project and configuring the CodeDeploy Jenkins plugin.

Testing the whole CI/CD pipeline.

### Create the resources
how to launch an AWS CloudFormation template, a tool that creates the following resources:

Amazon S3 bucket—Stores the GitHub repository files and the CodeBuild artifact application file that CodeDeploy uses.
IAM S3 bucket policy—Allows the Jenkins server access to the S3 bucket.
JenkinsRole—An IAM role and instance profile for the Amazon EC2 instance for use as a Jenkins server. This role allows Jenkins on the EC2 instance to access the S3 bucket to write files and access to create CodeDeploy deployments.
CodeDeploy application and CodeDeploy deployment group.
CodeDeploy service role—An IAM role to enable CodeDeploy to read the tags applied to the instances or the EC2 Auto Scaling group names associated with the instances.
CodeDeployRole—An IAM role and instance profile for the EC2 instances of CodeDeploy. This role has permissions to write files to the S3 bucket created by this template and to create deployments in CodeDeploy.
CodeBuildRole—An IAM role to be used by CodeBuild to access the S3 bucket and create the build projects.
Jenkins server—An EC2 instance running Jenkins.
CodeBuild project—This is configured with the S3 bucket and S3 artifact.
Auto Scaling group—Contains EC2 instances running Apache and the CodeDeploy agent fronted by an Elastic Load Balancer.
Auto Scaling launch configurations—For use by the Auto Scaling group.
Security groups—For the Jenkins server, the load balancer, and the CodeDeploy EC2 instance

![image](https://user-images.githubusercontent.com/48589838/89985330-87d14500-dc98-11ea-9964-c1211d0c8a03.png)

![image](https://user-images.githubusercontent.com/48589838/89985319-83a52780-dc98-11ea-8442-3e8e7eb3e403.png)


### Access and unlock your Jenkins server

Copy the JenkinsServerDNSName value from the Outputs tab of the CloudFormation stack, and paste it into your browser.

To unlock the Jenkins server, SSH to the server using the IP address and key pair, following the instructions from Unlocking Jenkins.

Use the root user to Cat the log file (/var/log/jenkins/jenkins.log) and copy the automatically generated alphanumeric password (between the two sets of asterisks). Then, use the password to unlock your Jenkins server, as shown in the following screenshots.

![image](https://user-images.githubusercontent.com/48589838/89985442-ba7b3d80-dc98-11ea-9cb4-9014339ba6e3.png)

![image](https://user-images.githubusercontent.com/48589838/89985456-be0ec480-dc98-11ea-9f0a-32333a15e9ce.png)

![image](https://user-images.githubusercontent.com/48589838/89985477-c666ff80-dc98-11ea-8313-dcdec60d39f8.png)

![image](https://user-images.githubusercontent.com/48589838/89985469-c23ae200-dc98-11ea-9243-9c8994fa4f28.png)



### Create a project and configure the CodeDeploy Jenkins plugin

![image](https://user-images.githubusercontent.com/48589838/89985612-fadabb80-dc98-11ea-84cf-c2add128ffc0.png)
![image](https://user-images.githubusercontent.com/48589838/89985621-ff06d900-dc98-11ea-9fee-f80963c8291f.png)
![image](https://user-images.githubusercontent.com/48589838/89985634-05955080-dc99-11ea-9187-db635bdeca9a.png)
![image](https://user-images.githubusercontent.com/48589838/89985688-15149980-dc99-11ea-8810-8e7a43c1e4ff.png)
![image](https://user-images.githubusercontent.com/48589838/89985702-1c3ba780-dc99-11ea-90c3-220b906d91a7.png)
![image](https://user-images.githubusercontent.com/48589838/89985709-1fcf2e80-dc99-11ea-8caf-4962b2721915.png)
![image](https://user-images.githubusercontent.com/48589838/89985726-25c50f80-dc99-11ea-9955-68b7897cb6db.png)
![image](https://user-images.githubusercontent.com/48589838/89985715-22ca1f00-dc99-11ea-9fe5-4a1b0c79e65c.png)
![image](https://user-images.githubusercontent.com/48589838/89985694-180f8a00-dc99-11ea-8a3c-fa211b9ea87e.png)
![image](https://user-images.githubusercontent.com/48589838/89985744-28c00000-dc99-11ea-8e62-e3d18baa5152.png)
![image](https://user-images.githubusercontent.com/48589838/89985756-2c538700-dc99-11ea-9318-a0cb7a6aed0a.png)
![image](https://user-images.githubusercontent.com/48589838/89985781-31b0d180-dc99-11ea-969e-407595b211ad.png)
![image](https://user-images.githubusercontent.com/48589838/89985795-35dcef00-dc99-11ea-816f-2ce6a2bacece.png)
![image](https://user-images.githubusercontent.com/48589838/89985806-38d7df80-dc99-11ea-8cd8-b003ccac1c45.png)
![image](https://user-images.githubusercontent.com/48589838/89985848-45f4ce80-dc99-11ea-9a47-c8256c083864.png)
![image](https://user-images.githubusercontent.com/48589838/89985864-4a20ec00-dc99-11ea-8dbf-fcecdedec7e6.png)
![image](https://user-images.githubusercontent.com/48589838/89985875-4db47300-dc99-11ea-8288-fb7e30a5cb11.png)
