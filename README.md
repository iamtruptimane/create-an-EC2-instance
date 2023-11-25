# Create Your First Amazon EC2 Instance (Linux)
Amazon Elastic Compute Cloud (EC2) is one of the most popular AWS services. EC2 allows you to launch different types of cloud instances and pay for them with a pay-per-use model. EC2 allows you to have operating system level control of your computing resources while running in Amazon’s computing environment. Amazon EC2 reduces the time required to obtain and boot new server instances from days or weeks to minutes. This allows you to quickly scale capacity, both up and down, as your computing requirements change. Amazon EC2 allows you to build and configure your instances as you like, from your desired operating system to your applications.

## Project Objectives
* Configure and launch an instance in EC2
* Understand the Instance States and other critical instance information
* Generate and use a Secure Shell (SSH) public/private key pair
* Terminate an instance

## Project Prerequisites
* Conceptual understanding of EC2
* Conceptual understanding of SSH client software, protocol, and keys

## Step 1: Logging In to the Amazon Web Services Console
login to the AWS account with your credentials.

## Step 2: Creating an EC2 Instance
1. In the AWS Management Console search bar, enter EC2, and click the EC2 result under Services:

2. Since this may be your first exposure to the EC2 Dashboard, it's worth spending a minute or two learning a few important parts of the dashboard:

From left to right, top to bottom:
* Additional navigation options are across the top-left of the Dashboard
* Basic account information, current region, and Support options are across the top-right
* Navigation to additional EC2 resources and features are located in the left pane
* Resources section - provides a high-level summary of current EC2 resource usage
* Launch Instance section - Offers a single click to start the process of launching a new EC2 instance (you'll do that next)
* Service Health section - Simple and quick way to obtain the high-level service health in your region (or click Service Health Dashboard for a more comprehensive AWS health check)
* Additional Information - Context sensitive help on Getting Started (with EC2) or a complete listing of all AWS documentation

3. Click the Launch instance:

4. In the Name and tags section, an optional name can be added that will create a tag that will have the key of Name. Additional tags can also be created here. 

Tags are specified as Key/Value pairs. They are not mandatory although it is useful to tag all of your AWS resources in production environments to stay organized.

5. In the Application and OS Images section, select the Amazon Linux option under Quick Start.

As you can see, Amazon provides many AMIs, including the most popular versions of Linux and Windows, often in 32-bit and 64-bit variants. Look at the supporting text to find out what other software packages and development languages are already installed on the image (such as Perl, Python, Java, etc.). You can think of AMIs as the blueprint or DNA of the instance you plan to launch.

6. In the Instance Type section, you should not change any options. Simply make sure the default t2.micro is selected:

7. In the Key pair section, click on Create new key pair, enter _keypair_ for the Key pair name, keep the default value for Key pair type and Private key file format, and click Create key pair. The key pair will begin downloading a file named keypair.pem on your local system. It contains a private key that you can use to connect to the EC2 instance via SSH. 

8. In the Network settings section, read the supporting text under Security groups (Firewall), and ensure the Allow SSH traffic from box is checked and Anywhere is selected:

9. In the Configure storage section, ensure the default values of 8 GiB and gp3 Root volume is selected:

The default values work fine here. There is no need to add additional volumes, encrypt volumes, or change any other settings. Simply note this is where you can change storage settings if needed.

10. Click on Advanced details to expand the section and take a minute to look over the various configurations: 

You can configure many different options on this page of the wizard, but it's best to keep your first launch simple. The information icon is a useful feature for easing your learning curve while using the AWS Console. 

11. Review the Summary section, and click Launch instance when ready:

12. Click the View all instances (lower right) to close the confirmation page and return to the Instances screen of the EC2 console.



A confirmation page will let you know that your instance is launching:
The Details tab contains a wealth of information on your instance. When you launch an instance, its initial Instance state defaults to Pending. After the instance starts, its Instance state transitions to Running, and it receives a Public IPv4 address and Public IPv4 DNS name. It typically takes about 30 seconds for the AWS Linux instance to transition to a running state.

_Congratulations...you just launched your first EC2 instance!_

## Summary
In this step, you launched an EC2 instance. you also learned how to generate your own SSH key pair for connecting to a running Linux instance.Now that you have a running instance, you can treat it as any other Linux host. That is, you can connect to it, install and configure software, develop applications, and other tasks.

## Step 3: Connecting to an Instance using SSH
In order to manage a remote Linux server, you must employ an SSH client. Secure Shell (SSH) is a cryptographic network protocol for securing data communication. It establishes a secure channel over an insecure network. Common applications include remote command-line login and remote command execution.

Linux distributions and macOS ship with a functional SSH client that accepts standard PEM keys.

## Instructions (Linux / macOS Users)
1. Open your Terminal application

2. Run the following ssh command: 
```
ssh -i /path/to/your/keypair.pem user@server-ip
```
* server-ip is the Public IP of your server, found on the Details tab of the running instance in the EC2 Console
* user is the remote system user (ec2-user for Amazon Linux) that will be used for the remote authentication.

Note that the Amazon Linux AMIs typically use ec2-user as a username. Other popular Linux distributions use the following user names:
* Debian: admin
* RedHat: ec2-user
* Ubuntu: ubuntu

Assuming that you selected the Amazon Linux AMI, your assigned public IP is 123.123.123.123, and your keypair (named "keypair.pem") is stored in /home/youruser/keypair.pem, the example command to run is: 
```
ssh -i /home/youruser/keypair.pem ec2-user@123.123.123.123

```
_Note: You can find the Public IP under the AWS EC2 console, and choosing the available EC2 instance._

_Important! Your SSH client may refuse to start the connection, warning that the key file is unprotected. You should deny the file access to any other system users by changing its permissions. From the directory where the public key is stored on your local machine, issue the following command and then try again:_
```
chmod 400  /home/youruser/keypair.pem
```
The change mode (chmod) command shown above will change the permissions on your private key file so only you can read it. No other users on the system can modify it, or even read it.

## EC2 instance connect
_Tip: The Instances page provides a helpful shortcut for connecting to a Linux instance. Select the running instance and click the Connect button. It will formulate an example ssh command for you, including the required key name and public IP address. However, it is still useful to learn the basics of manually using the ssh command._

## Step 4: Terminating an EC2 Instance
AWS bills EC2 usage per second in most cases.When you are sure that you no longer need an instance, you can terminate it. The specific instance and the data on the root volume (system disk) is not recoverable (by default) however. So be sure you don't need it before terminating an instance. If you stop an instance, you can start it again later (and access data on all the disks). In this step, you will terminate a running EC2 instance.

1. Return to the EC2 console in your browser.

2. Click Instances in the left navigation pane. Select the running instance, then click the dropdown menu at the top middle of the page Instance State > Terminate instance.

3. Read the Warning from AWS, then click the Terminate button in the Terminate Instances confirmation dialog:

 4. Watch as the Instance State transitions from running to shutting-down and finally to terminated:

Your instance and the data stored on its root volume are completely destroyed. 






























