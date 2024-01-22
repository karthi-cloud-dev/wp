# WordPress Website on AWS

### <U>VPC CREATION</U> 

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/e09d9bdd-7671-434f-945b-2ddd8f28e725)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/fc20a991-d941-4a5b-8439-62cd8d36de19)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/820b5107-4ca0-4525-99dc-5d8dea668b47)

>[!note]
>Once a VPC is created a default route table is created. And by default the route table is private.

### <U>CREATE INTERNET GATEWAY AND ATTACH IT TO VPC</U>

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/f1e6a6b4-ade3-46dd-9aee-7c6fe739e151)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/015101b3-e082-4de9-9a22-276b79f6176c)
After creating the internet gateway, attach it to the VPC that was created. Select the IGW and click on Actions -> Attach VPC.

### <U>CREATE PUBLIC SUBNETS IN 2 AVAILABILITY ZONES</U>

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/1d5f4363-bcd1-4ce8-a099-c4d356eecea5)
>[!IMPORTANT]
>Always make sure to select the appropriate VPC, currently in the wp-app VPC there are no subnets.

<u>Public subnet-1</u>
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/8212cb0e-fb8d-4525-a4a0-4923e3033b2f)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/23fd3e87-cea4-4fe5-bac3-596c15aab659)

<u>Public subnet-2</u>
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/fd4798e2-afea-489f-a00f-7c63363f90ca)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/b65058c5-13c4-414f-8fb4-04a29ec530f6)
>[!Note]
>Please note that the availability zone should be us-east-1 and the CIDR block should be changed accordingly.

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/0db0abe4-849b-46e9-9cd8-cde9a31a2b6f)
>[!NOTE]
>Select a subnet and click on Actions -> Edit subnet settings and select Enable auto-assign public IPV4 address.
>We can also do this while creating an EC2 instance in which the Enable public IP address option can be enabled.

### <U>CREATE PUBLIC ROUTE TABLE</U>

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/ae2dbbf9-c0b9-4d88-b3f8-1663cee71f4d)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/c288d9a5-82a1-4bd3-8956-05196c97308c)
>[!Note]
>Select the route table and click on Actions -> Edit Route table. Here the Destination shall be anywhere in the internet and the target shall be Internet gateway.

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/83dded57-839d-4e23-98d1-13a82f40091a)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/6cb9fc13-27c3-47c6-b27f-3d866438fd07)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/77c1ca49-8d37-4879-8534-e7118392f1c8)
>[!Note]
>Click on the Edit subnet Associations.
>Select both the subnets and click on save.
### <u>CREATE PRIVATE SUBNETS</u>

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/049f5aa6-bdb8-41ac-a03a-7de26ee3df30)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/bcc10ad0-7f37-4404-8dda-40219ee64203)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/27f4d23a-74d9-44cc-bd7e-8b1c61a0ff48)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/a7343068-c5f4-4c3a-9bc5-bd80aa7a4bf1)
>[!Note]
>There are 2 private subnets each in one availability zone for the application.
>Another 2 private subnets each in one availability zone for the Database.

### <u>CREATE PRIVATE ROUTE TABLES</u>

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/b5f2a7bb-3e13-4b12-8f3b-999efb62f4ea)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7b3dbb59-59a9-46e3-87a1-c41e2337d3d8)
>[!note]
>Create private route tables with no internet gateway attached to it. Private subnets don't have internet access.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/cbb3c3b3-e019-4f89-b351-57d1abd78ec0)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7f53b7ac-4e4c-4caa-bc97-1a1c0f55b30e)

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/dd5b34d2-b9b7-441d-84ed-522cce4a51e6)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/1569583e-2541-4f8a-b868-13bcf1d6c8ce)
>[!note]
>Private subnet 2 is connected to the default route table that was created during the VPC creation. If we look into the column name "Main" it says "Yes", which means it is associated to the main route table.
### <u>CREATE NAT GATEWAY</u>

>[!INFO]
>NAT (**Network Address Translation**) Gateway allows the private subnets to have internet access to download packages. However the external services cannot initiate a connection with those instances.
>

>[!important]
>NAT gateway is always created in the public subnets.
>Before you create the NAT gateway make sure you are in the appropriate region 
>(ex: us-east-1)

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/857fcd53-513f-4508-8ff1-a2fcdd4d643e)
>[!Note]
>Create elastic IP addresses just by clicking on the "Allocate Elastic IP address" and there is not much settings to change inside it. 
>There will be 2 NAT gateways for each public subnet, that is why 2 IP address.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/6478f0f8-bc44-4562-838d-3e7c0072ecb6)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7c6ec6a0-2c39-46eb-b511-a829d1ea30b3)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/ecd7c54f-6441-4df8-8780-f157321f236c)
>[!note]
>In the above steps we have created a NAT gateway on the public subnet-1 and allocated a elastic IP to it.
>Next we have edited the private route table -1 and added the NAT gateway -1 to it so that the private subnet-1 can have access to the internet.
>Now do the same to NAT gateway - 2.

### <u>CREATING SECURITY GROUP</u>

>[!IMPORTANT]
>Before creating the SG we must understand that:
>- Application load balancer will accept traffic from anywhere in the internet
>- App servers will accept traffic only from the Application Load balancer
>- Database servers will accept traffic only from the App servers
>- EFS file system will accept traffic from the App servers.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/3244589f-3eff-4e82-ba56-ec7874cb8fab)
>[!note]
>This SG was created when the VPC was created. This a default one.

#### ALB Security group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/604adcfc-7a76-401c-b8fa-136d19f6c29f)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/9900d3d2-4744-4490-aa72-f851169c28f6)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/6fadb5fe-641f-4e80-89ca-80361d62327c)

#### Appserver Security Group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/f044531e-4ba2-463a-86b2-dc0f00bade34)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/144fb4c8-0f05-4d82-88c3-9a7b0eabcc26)
>[!note]
>As mentioned above the app server will accept traffic from ALB so select the source to be ALB.
>Outbound shall be all traffic.

#### Database Security Group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/69bf43a3-a4aa-49a1-8114-5049570ac0ac)
>[!note]
>Database shall accept traffic from App server only. and the type of database is MySql.

#### EFS Security Group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/222818a7-4381-4470-9a96-47c45f94e702)
>[!info]
>One point to be noted in EFS is, there is another inbound rule added after creating the EFS SG. The below image will show it. We have to add EFS SG as inbound rule along with App server SG.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/e3c48011-9521-4c8b-9910-acc23076d736)

### <u>CREATING MYSQL DATABASE</u>

#### Create subnet group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/f13f74d8-7232-4be8-b753-c9482af90d12)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/c4afe5dd-70dd-4457-971e-3afec4a3dae8)
>[!note]
>Choose the availability zone and select the subnets that were created for the database.

#### Create Database
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/8f94d4b9-7340-40a1-835e-276c1dd406f7)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/abb1a75e-4205-4314-99c8-c70888e1a735)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/4a8604b9-d747-41cb-8578-92b11640d3ef)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/b5a13a8b-5874-4680-ba83-e2ded78acacb)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/2166506a-638f-41eb-a914-aeae09a1e2a3)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/60ba2aae-7fe2-483f-b449-45f39c33aad4)
>[!important]
>Make sure to give a DB name and remember the password given to it.

### <u>CREATING ELASTIC FILE SYSTEM</u>

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/a17d104c-cddb-4240-b11e-271dfe6440e9)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/b330427c-4c9d-48a7-8eed-e5cf3dce3bb7)
>[!important]
>Uncheck the enable encryption of data at rest to avoid additional charges.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/ecf8c38c-585b-4bbe-9f27-8c92b1a1c638)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7672be7b-2861-4995-9f72-4f692c39e4b3)
>[!note]
>Make sure to select the private subnet that we created for the database.
>Make suer to select the SG that we created for the EFS.

#### Create an EC2 instance of the database
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/75174581-b8ed-4aa5-ac7c-9d976560d3fe)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/966175b3-ea47-4986-9ef1-8cb97d399404)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/3744a6d3-b003-4d99-9030-5dbf030ccd70)
>[!note]
>- Create a new EC2 instance and select the appropriate VPC and private subnet. 
>- Create a keypair so that we can ssh with the instance.
>- Make sure to enable the public IP address assignment.
>- Make the instance AZ and the public subnet AZ are the same to avoid cross-platform charges.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/452dca95-b668-4b0e-b885-a53960e39639)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/eafb1016-cf82-4d04-9720-499a8f17c838)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/df547bea-4b94-4471-80f1-63ebb1fa0327)

#### Mounting the EFS
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/615545e4-33ae-4717-ac4f-d6caa9f8faad)
>[!note]
>Get into the EFS that we created and click on "Attach". We shall get these commands. 
>Now we have to ssh in to the db instance and run these commands.
>Don't run the commands yet, these are only for references.

^MountingtheEFS


![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/98c67de2-82d2-4ae9-a9c9-381f64195f70)
>[!important]
>Before we get into the mounting part, we need to make sure that the DNS hostnames is enabled in the VPC.

###  <U>WORDPRESS INSTALLATION AND EFS FILES MIGRATION</u>

#### Creating Security group for SSH
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/589ac122-07a1-48a4-8ed8-d7217587cfc7)

#### Editing the EFS Security Group
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/c8fabd78-b719-402b-ab82-57ec1c90a18f)

#### Editing the App Server Security Group
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/b1834c9f-aa97-47e1-b98f-b54f0829eada)

#### Creating an EC2 instance for the WP server
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/1311c1ce-9c85-4e96-8b2d-035ea13db524)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/31781816-493f-4959-b04b-0a0b5591a264)
>[!important]
>Make sure to select the Security group mentioned in the image while creating the EC2 instance.

#### WP installation
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/2fd85b2e-6021-48ab-8a44-7eb85e342bfc)
>[!Note]
>SSH into the EC2 instance

```bash
1.
# create the html directory and mount the efs to it
sudo su
yum update -y
mkdir -p /var/www/html
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-06f48bf1a1e650a19.efs.us-east-1.amazonaws.com:/ /var/www/html

2.
# install apache 
sudo yum install -y httpd httpd-tools mod_ssl
sudo systemctl enable httpd 
sudo systemctl start httpd

3.
# install php 7.4
	sudo amazon-linux-extras enable php7.4
	sudo yum clean metadata
	sudo yum install php php-common php-pear -y
	sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y

4.
# install mysql5.7
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo nano /etc/yum.repos.d/mysql-community.repo

# when you are inside the mysql-community.repo add replace the key shown below:
gpgkey=https://repo.mysql.com/RPM-GPG-KEY-mysql-2022

sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld

5.
# set permissions
sudo usermod -a -G apache ec2-user
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
sudo find /var/www -type f -exec sudo chmod 0664 {} \;
chown apache:apache -R /var/www/html 

6.
# download wordpress files
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
cp -r wordpress/* /var/www/html/

7.
# create the wp-config.php file
cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php

8.
# edit the wp-config.php file
nano /var/www/html/wp-config.php

9
# restart the webserver
service httpd restart
```
>[!important]
>The mount command mentioned in the 1st block of code is unique and shall change for different account which needs to be updated. Commands are here -  [[Hosting-Wordpress-AWS/README#^MountingtheEFS|Mount]] ]

![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/2eed6381-a18b-414a-8e35-f32a236e6aae)

![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/f6e8584a-1cae-4ca2-b41b-fe9c7afc0d42)

![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/8782c53b-58ec-4f39-aa84-455d97e92944)

### CREATE APPLICATION LOAD BALANCER
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/1c45ab30-c812-4490-b98a-2c9e9efdc058)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/12885ab5-68ab-4569-b3d0-06a681013a58)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/e1793cfe-1150-414f-bffc-cef0d6842770)

```BASH
#!/bin/bash

yum update -y
sudo yum install -y httpd httpd-tools mod_ssl
sudo systemctl enable httpd 
sudo systemctl start httpd
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld
echo "fs-06f48bf1a1e650a19.efs.us-east-1.amazonaws.com:/ /var/www/html nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 0 0" >> /etc/fstab
mount -a
service httpd restart
```
>[!IMPORTANT]
>Change the EFC commands in the above block of code.
>This is the meta data that needs to be given during the EC2 creation.
>
>

>[!Note]
>Similarly create ALB-02 EC2 instance

#### ALB Configuration
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/1db1977d-0c36-4c4a-80a0-ba9858e7dbe6)
>[!Note]
>Select Application load balancer

![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/e23787b4-7805-40b1-9de4-ef5c8e73d424)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/bdeedcaf-77c9-4974-b2b6-f987992541f8)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/29cc78c6-8316-4461-b866-2b1b309f826d)
>[!important]
>Provide the target group

#### Target Group
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/063ef86c-68ec-430d-b7b6-518b6d199472)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/37254c3d-4baa-41ad-8e38-abe4bfdf515d)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/0d796395-0b1d-4d7b-a783-31f06926f751)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/8b0d0070-5a42-4aad-ad01-4f7e799d1252)

Back to ALB
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/58e003a5-c22d-4037-8e89-d6c53dbf6220)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/a91f6908-3e0b-464b-901f-c4490ee7c32c)
![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/e2b04260-48aa-4437-95f1-29f9b97682ce)

![image](https://github.com/karthi770/Hosting-Wordpress-AWS/assets/102706119/34d7ac54-fd98-4ba9-a084-50bcc6674b1d)
>[!info]
>Final WordPress Site







