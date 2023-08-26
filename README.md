<p align="center">
<img src="https://github.com/kura-labs-org/kuralabs_deployment_1/blob/main/Kuralogo.png">
</p>
<h1 align="center">C4_deployment-2<h1> 

Demonstrate your ability to run a Jenkins build and manually deploy to Elastic Beanstalk.

- Create a separate GitHub repository for this application 

- Download the files from this repository and upload them to your newly created repository 

- Be sure to follow the deployment instructions from this Repository  

- Document your progress in a .md file in your repository. Also, document any issues you may run into and what you did to fix them.
  
- Make sure your documentation includes these sections:
  - Purpose
  - Issues
  - Steps
  - System Diagram
  - Optimization (How would make this deployment more efficient)

- Lastly, save your documentation and diagram into your repository. Submit your repository link to the LMS

## Deployment instructions Link:
-  [Link to instructions: https://github.com/kura-labs-org/C4_deployment-2/blob/main/Deployment-instructions.md



# Creating a Jenkins Server on Amazon EC2 using Jenkins Debian Packages

Follow these steps to set up a Jenkins server on an Amazon EC2 instance using Jenkins Debian Packages:

1. **Sign in to your AWS Account:**
   - Logged in to [Amazon Web Services (AWS) Console](https://aws.amazon.com/)

2. **Launch an EC2 Instance:**
   - From the AWS Management Console, navigate to the EC2 Dashboard.
   - Click on "Launch Instances."
   - Named the Instance "Deployment 2 Jenkins Instance"
   - Chose Ubuntu.
   - Selected an instance type "t2.micro".
   - Configured instance details (key pair login), network settings, and storage.
   - Configured security groups to allow SSH (port 22) and HTTP (port 8080) access (ssh-access & Jenkins).

3. **Connect to the EC2 Instance:**
   - Once the instance is running, I connected to it using SSH.
   - On my local device, I copied my public ssh key and pasted it in the "authorized_keys" file on the EC2 instance
   - I used Windows PowerShell terminal.
   - Use the following command to connect:
     ```bash
     ssh ubuntu@your-instance-ip
     ```

4. **Install Python 3.10 and python3.10-venv:**
   - Update the package list:
     ```bash
     sudo apt update
     sudo apt install python3.10 python3.10-venv -y
     ```

5. **Install Java and Jenkins:**
   - Install Java and Jenkins using the Jenkins Debian Packages:
     ```bash
     # Add the Jenkins repository key to the system
     curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
       /usr/share/keyrings/jenkins-keyring.asc > /dev/null
     # Add Jenkins apt repository entry
     echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
       https://pkg.jenkins.io/debian binary/ | sudo tee \
       /etc/apt/sources.list.d/jenkins.list > /dev/null
     # Update local package index
     sudo apt-get update
     # Install required packages
     sudo apt-get install fontconfig openjdk-17-jre
     # Install Jenkins
     sudo apt-get install jenkins
     ```
   
6. **Start Jenkins and Enable on Boot:**
   - Start the Jenkins service:
     ```bash
     sudo systemctl start jenkins
     ```
   - Enable Jenkins to start on boot:
     ```bash
     sudo systemctl enable jenkins
     ```

7. **Access Jenkins Web Interface:**
   - Open a web browser and navigate to `http://your-instance-ip:8080`.
   - Retrieve the initial admin password from the server:
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```
   - Copy the password and paste it into the Jenkins Unlock page.

8. **Install Recommended Plugins:**
   - Choose the "Install suggested plugins" option during the setup wizard.

9. **Create an Admin User:**
   - Fill out the required information to create an admin user for Jenkins.

10. **Adding Plugins to Jenkins - Install "Pipeline Utility Steps" Plugin:**
    - In the Jenkins dashboard, click on "Manage Jenkins" in the left-hand menu.
    - From the drop-down menu, select "Manage Plugins."
    - In the "Filter" search bar, type "Pipeline Utility Steps" to find the plugin.
   - Locate the "Pipeline Utility Steps" plugin in the list of available plugins.
   - Click the "Install without restart" button at the bottom of the page. This will download and 
     install the selected plugin.

11. **Start Using Jenkins:**
    - Once the setup is complete, you can start using Jenkins to create jobs and pipelines for your projects.

## Jenkins Build Test and Download of zip.

Follow these steps to build the application onto Jenkins:

1. **Download and Extract Files:**  
   - Download the files from KuraLabs and unzip them.

2. **Repository Setup:**  
   - Create a new repository.
   - Paste the downloaded files into the repository.

3. **Jenkins Configuration:**  
   - Log in to the Jenkins instance created above.
   - Created a new build with the name "Deployment2EthanArteta".

4. **Github Token Generation:**  
   - Generate a new token from GitHub for authentication.

5. **Jenkins Credentials:**  
   - Create new credentials in Jenkins to enable deployment of GitHub files.

6. **Pipeline Setup:**  
   - Apply and save the pipeline build configuration.

7. **Application Build:**  
   - Successfully ran the application build in Jenkins without encountering errors.

8. **Application Zip file:**
   - Enter the logs on Jenkins to find the location of your application after it has been zipped by Jenkins.

9. **Downloading a File from EC2 Instance using `scp`:**
   - Use the `scp` (Secure Copy) command to download a file from your EC2 instance to your local device.
     # Step 1: Open a Terminal on Your Local Machine
	   Open a terminal window on your local device. You'll use this terminal to run the `scp` 
           command.
     # Step 2: Run the `scp` Command
	   Use the following syntax to copy a file from your EC2 instance to your local device:
	   ```bash
	      scp -i /path/to/your-key.pem ubuntu@your-instance-ip:/path/to/remote/file.zip /path/to/local/
     
10. **Manual Deployment to Elastic Beanstalk:**  
    - Download the zip folders for manual deployment onto Elastic Beanstalk.

## Creating AWS IAM Roles permissions.

1. **Navigate to AWS IAM Console.**
   
2. **Click "Roles"**

3. **Click "Create role"**

4. **Click the "AWS service" field in the "Trusted entity type".**

5. **Click on the drop down link under "Use cases for other AWS Services".**

6. **Type "elastic"**

7. **Select "Elastic Beanstalk"**

8. **Click the "Elastic Beanstalk - Customizable" field.**

9. **Click "Next"**

10. **Do not edit anything in the "Add permissions" field and instead click "Next"**

11. **Click the "Role name" field and enter "aws-elasticbeanstalk-service-role"**

12. **Click "Create role"**

13. **Click "Create role" to create a second Role**

14. **Click the "AWS service" field.**

15. **Click the "EC2" field.**

16. **Click "Next"**

17. **Click the "Filter policies by property or policy name and press enter." field and find "AWSElasticBeanstalkWebTier"**

18. **Click the checkbox associated with "AWSElasticBeanstalkWebTier".**

19. **Click the "Filter policies by property or policy name and press enter." field and find "AWSElasticBeanstalkWorkerTier"**

20. **Click this checkbox "AWSElasticBeanstalkWorkerTier".**

21. **Click the "Filter policies by property or policy name and press enter." field and find "AWSElasticBeanstalkMulticontainerDocker"**

22. **Click this checkbox associated with "AWSElasticBeanstalkMulticontainerDocker".**

23. **Click "Next"**

24. **Click the "Role name" field and enter "Elastic-EC2"**

25. **Click "Create role"**

26. **All Done!!**

## Deploying an Application on AWS Elastic Beanstalk

1. **Navigate to AWS Elastic Beanstalk Console.**
   
2. **Click "Create application"**

3. **Click the "Application name" field.**

4. **Type "url-shortener"**

5. **Scroll down to Platform.**

6. **Click on the drop down field and click on "Python"**

7. **Click on the Platform branch selection.**

8. **Click "Python 3.9 running on 64bit Amazon Linux 2023"**

9. **Scroll down to Application code and click the upload code button.**

10. **Click the "Version label" field.**

11. **Type "v1"**

12. **Click the local file button.**

13. **Click "Choose file" and upload the zipped file from Jenkins**

14. **Click "Next"**

15. **Under "Service access" Click the "Existing service role" drop down field.**

16. **Click "ElasticEC2"**

17. **Under "EC2 key pair" drop down field select your corresponding key pair.**

18. **Under "EC2 instance profile" Click the "EC2 instance profile" drop down field.**

19. **Click "ElasticEC2"**

20. **Click "Next"**

21. **Click on the VPC drop down field for VPC selection.**

22. **Select your default VPC**

23. **Select any Availability Zone**

24. **Click "Next"**

25. **Click "Root volume type" drop down field.**

26. **Click "General Purpose (SSD)"**

27. **Change the size field to 10 GB**

28. **On the same page, scroll down to the section called "Instance types" deselect the current instances, and choose a "T.2 MICRO"**

29. **Click "Next"**

30. **Scroll down on the "Configure updates, monitoring, and logging - optional" page and Click "Next"**

31. **Review your configuration and Click "Submit"**

32. **When your environment completes, the health status should say "OK", and then you can select your Domain Name.**

33. **Successful Deployment:**  
    - Successfully deployed the application onto Elastic Beanstalk.
