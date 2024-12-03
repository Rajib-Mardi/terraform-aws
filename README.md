### Automate Provisioning EC2 with Terraform




### Project: 
* Automate AWS Infrastructure  and run Nginx container 
# ## Technologiesused: 
* Terraform, AWS, Docker, Linux, Git

### Project Description:

#### Create TF project to automate provisioning AWS Infrastructure and its components, such as: VPC, Subnet, Route Table, Internet Gateway, EC2, Security Group

* Terraform config  created a custom VPC  : VPC with a CIDR block from var.vpc_cidr_block and a dynamic name based on var.env_prefix.
* Terraform config created a custom subnet : Subnet within the VPC, with a CIDR block from var.subnet_cidr_block, in a specified availability zone (var.avail_zone), and a dynamic name.

     
     
     ![VPC Management Console - Google Chrome 13-06-2023 18_54_19](https://github.com/Rajib-Mardi/terrraform/assets/96679708/babb7b5e-39b8-40c9-b174-77aeca620d7c)



   ![VPC Management Console - Google Chrome 13-06-2023 18_54_29](https://github.com/Rajib-Mardi/terrraform/assets/96679708/7a99bc23-1fc3-4353-ae64-1b35d6d09027)

  
*  Configure Default/Main Route Table : Terraform config   the default route table for a VPC to route all traffic (0.0.0.0/0) to an Internet Gateway, and adds a name tag using a variable prefix.




![Route tables _ VPC Management Console - Google Chrome 13-06-2023 18_44_35](https://github.com/Rajib-Mardi/terrraform/assets/96679708/370d73b7-5a64-4525-80ea-8662a8980b27)

* Configure the internet gateway to allow the vpc to connect to the internet : Terraform configuration creates an Internet Gateway and attaches it to the VPC. It is tagged with a name based on ```var.env_prefix``` (```e.g., dev-igw```).



![Route tables _ VPC Management Console - Google Chrome 13-06-2023 18_45_00](https://github.com/Rajib-Mardi/terrraform/assets/96679708/36dc4f71-4600-43fd-824d-580c30f73db3)


*  Configured Default Security Group :   Terraform configuration creates a security group allowing SSH from a specific IP, HTTP from anywhere, and all outbound traffic, with a name tag based on a variable prefix



![Route tables _ VPC Management Console - Google Chrome 13-06-2023 18_45_29](https://github.com/Rajib-Mardi/terrraform/assets/96679708/a23a649e-4218-45ef-adb5-730d547dc196)


## Configure TF script to automate deploying Docker container to EC2 instance
* Configure ssh key pair in Terraform config file : This Terraform configuration creates an AWS EC2 key pair named ```tfkey``` using a public key from a local file specified by ```var.ssh_key```.



![Route tables _ VPC Management Console - Google Chrome 13-06-2023 18_46_10](https://github.com/Rajib-Mardi/terrraform/assets/96679708/d0e0bdad-9df4-4534-8d15-22471dd87a4b)




 * Fetch AMI :  Terraform configuration fetches the latest Amazon Linux 2 AMI (matching the name ```amzn2-ami-kernel-5.10-hvm-*```) and outputs its ID.

* Create EC2 Instance : Terraform config launches an EC2 instance with: AMI: Latest Amazon Linux 2 , Instance type: ```var.instance_type```,  Subnet: ```myapp-subnet-1```, Security group: Default,  Public IP: Yes., SSH key: ```ssh-key```, User data: ```entry-script.sh```, Tag: ```Name = var.env_prefix-server```. 









![Instances _ EC2 Management Console - Google Chrome 13-06-2023 18_50_09](https://github.com/Rajib-Mardi/terrraform/assets/96679708/d51db805-96d4-4d42-a673-8f2c805d03bd)


* Apply terraform command : 
```
terraform plan
terraform apply --auto-approve 
```


* SSH into EC2 instance
![ec2-user@ip-10-0-10-107_~ 12-06-2023 20_22_49](https://github.com/Rajib-Mardi/terrraform/assets/96679708/a0ead0f1-7ec5-48d9-a02c-5a6e93cf0909)

#### Configured  Terraform  script to automate deploying Docker container to EC2 instance
   * Configured Terraform to install Docker and run nginx image
   *  create an "script.sh" file in terraform folder and write the linux commands to execute the shell script
      *  script: Updates the system and installs Docker.
      *  Starts the Docker service.
      *  Adds the ec2-user to the Docker group.
      *  Runs an Nginx container, mapping port 8080 to 80.

   *  Accessed nginx through Browser
 
 
 ![Welcome to nginx! - Google Chrome 13-06-2023 00_57_09](https://github.com/Rajib-Mardi/terrraform/assets/96679708/8a2cb1ca-bf94-4f5d-84a5-f900a4979202)


    
    


