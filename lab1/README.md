# LAB 1 - Creating Redshift Clusters
In this lab you will launch a new Redshift Cluster, setup connectivity and configure a JDBC Client tool.

## Contents
* [Before You Begin](#before-you-begin)
* [Configure Security](#configure-security)
* [Launch Redshift Cluster ](#launch-redshift-cluster)
* [Run Sample Query](#run-sample-query)
* [Before You Leave](#before-you-leave)

## Before You Begin
* Determine and capture the following information and login to the [AWS Console](https://console.aws.amazon.com/). If you are new to AWS, you can [create an account](https://portal.aws.amazon.com/billing/signup).
  * [Your-AWS_Account_Id]
  * [Your_AWS_User_Name]
  * [Your_AWS_Password]
* Determine the [AWS Region Name] and [AWS Region Id] which is closest to you and switch your console to that [Region](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html).  

## Configure Security
### VPC
Identify a VPC where you will launch your Redshift cluster.  For our purposes we will reuse the **VPC** created on the Networking lab.

### Subnets
Identify a subnet with a default route to an Internet Gateway.

### Subnet Group
Create a Redshift **Cluster Subnet Group** containing the two subnets you created earlier.
```
https://console.aws.amazon.com/redshift/home?#subnet-groups:
```
![](../images/SubnetGroup.png)
### Security Group
Create a **Security Group** associated to the VPC you created earlier.  Edit the Security Group to create a rule which allows incoming connections from your IP Address.
```
https://console.aws.amazon.com/vpc/home#SecurityGroups:sort=groupId
```
![](../images/SecurityGroup.png)
### S3 Access
Create an **IAM Role** with the type "Redshift" and the use-case of "Redshift - Customizable" and attach the AmazonS3ReadOnlyAccess and AWSGlueConsoleFullAccess policies to the role.
```
https://console.aws.amazon.com/iam/home?#/roles$new?step=type
```
![](../images/Role.png)

## Launch Redshift Cluster
Navigate to the **Amazon Redshift Dashboard** and click on the "Launch Cluster" button.  
```
https://console.aws.amazon.com/redshift/home#cluster-list:
```
* Cluster Details - Enter values as appropriate for your organization.  Note the Master user password as you will not be able to retrieve this value later.
![](../images/ClusterDetails.png)
* Node Configuration - Modify the Cluster type to Multi Node and set the Number of compute nodes to 2.
![](../images/NodeConfiguration.png)
* Additional Configuration - Choose the VPC, Subnet Group, VPC Security group, and Role which you identified or created earlier.
![](../images/AdditionalConfiguration.png)  
![](../images/AssignRole.png)

## Run Sample Query
* Run the following query to list the users within the redshift cluster.  
```
select * from pg_user
```
* If you receive the following results, you have established connectivity and this lab is complete.  
![](../images/Users.png)
