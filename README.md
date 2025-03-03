# Authentication-to-AWS-API

## Overview

This project illustrates the steps required in setting up secure authentication on AWS for resource management in the cloud.

**Creating an IAM Role**

We begin by establishing an IAM Role that spells out the permissions required for the operations our script will perform.

![alt text](<Images/Image 1.PNG>)

**Creatin an IAM Policy**

Next is configuring an IAM policy that grants full access to both EC2 and S3 resources on AWS.

### STEPS

* On the AWS console, locate IAM, choose policies
* In the policy editor section, find and select an AWS service
**Note**: You can only choose one service within  a visual editor performance block. To grant access to more than one service, add multiple permission blocks by choosing "Add more permissions".
In the Actions allowed, choose the actions to add to the policy.

With all steps completed we create a Policy; EC2_S3-access@Policy


![alt text](<Images/Image 2.PNG>)


**Creating an IAM User**

Here, we instantiate an IAM User; _test_user2_ and enable the AWS console access.
This being the primary entity our script uses to interact with AWS services.
On the _test_user2_ page, we go to security credentials and ensure console access is enabled.
After completing all required fields, we review and create a User.


![alt text](<Images/Image 3.PNG>)


**Assigning the User to the IAM Role**

This is achieved by linking the automation_user to the previously created IAM Role. This step is vital for enabling the necessary access levels for our automation tasks

### STEPS

* On the AWS console
* Click on Users
* Seect _test_user2_
* On the permissions section, go to Add Permissions
* Choose Create inline policy
* Select the Json editor
* Under Action, input "Sts AssumeRole"
* For Resources, Enter the ARN of the IAM Role created earlier.
   (ie, go back to role panel, locate the role name then copy the ARN or the role and paste in the resources field).
   Once done, click on next then click on create policy.


  ![alt text](<Images/Image 4.PNG>)


  **Attaching the IAM Policy to the User**
  This is the process of explicitly granting _test_uesr2_ the permissions defined in our IAM Policy. Also, this solidifies the user’s access to EC2 and S3 resources.

  ### STEPS

  * On the IAM Console, select the desired User
  * Go to the Permissions tab
  * Click Add Permissions
  * Choose Attach Policies directly
  * Select the Policy you want to attach to the User.

  **Creating Programmatic Access Credentials**

  We proceed to generate programmatic access credentials- access key ID and secret access key for the user.
  This we use when installing and configuring AWS CLI.


 **Installiing and Configuring AWS CLI**

 On Windows we downloaded, ran the installer and verify the installation for the AWS Command Line Interface(CLI).

 1. * Download the installer:
 Visit the <ins>official AWS CLI Version 2  download page and <ins>download the MSI installer for Windows

 
 The AWS CLI is a tool that allows you to interact with AWS services directly from your terminal enabling automation and simplification of AWS resource management.

 2. * Run the Installer:
   Execute the downloaded MSI installer and follow the on-screen instructions to complete the installation.

 3. * Verify Installation:

   Now open the command prompt and type aws --version to ensure the CLI is installed correctly.
   The version of the AWS CLI should be displayed

   ![alt text](<Images/Image 5.PNG>)

   ### Configuring the AWS CLI
   This step is where we configure it to use the **access key ID** and **secret access key** generated for **test_user2**.
   This will authenticate your CLI (Command Line Interface) requests to the AWS API.

   ### Configuring AWS CLI for access to AWS.

    On the terminal or command prompt, we run command

    aws configure

   This command initiates the set up process for your AWS CLI installation
   ![alt text](<Images/Image 6.PNG>)
    

   Next, we enter our credentials when prompted.
   Here, we enter the **AWS Access Key ID** and **AWS Secret Access Key** for the **test_user2**
   Next, we specify the default _**region**_ name and the default _**output**_ format.
   Note: The region should be the one you plan to deploy resources in and the common output format is **json**.

   Tip: We used the vim editor to properly apply the AWS Access key ID and AWS Secret Access Key as well as the default region and default output format.

   
   ![alt text](<Images/Image 7.PNG>)

   
    
   ![alt text](<Images/Image 8.PNG>)

   ![alt text](<Images/Image 9.PNG>)

   **Testing the Configuration**

    Now we verify that our AWS CLI is configured correctly and can communicate with AWS services.
    We try running a basic command to list all the AWS regions.

    aws ec2 describe-regions --output table

    This command queries the EC2 service for a list of all regions and formats the output as a table.

   ![alt text](<Images/Image 10.PNG>)
    
    Now we are ready to begin our automation!

