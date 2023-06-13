## Demo Project: 
* Automate AWS Infrastructure 
##Technologiesused: Terraform, AWS, Docker, Linux, Git

## Project Description:

### Create TF project to automate provisioning AWS Infrastructure and its components, such as: VPC, Subnet, Route Table, Internet Gateway, EC2, Security Group

* Create VPC & Subnet
     
     
     ```
     # aws_vpc.myapp-vpc will be created
     + resource "aws_vpc" "myapp-vpc" {
      + arn                                  = (known after apply)
      + cidr_block                           = "10.0.0.0/16"
      + default_network_acl_id               = (known after apply)
      + default_route_table_id               = (known after apply)
      + default_security_group_id            = (known after apply)
      + dhcp_options_id                      = (known after apply)
      + enable_dns_hostnames                 = (known after apply)
      + enable_dns_support                   = true
      + enable_network_address_usage_metrics = (known after apply)
      + id                                   = (known after apply)
      + instance_tenancy                     = "default"
      + ipv6_association_id                  = (known after apply)
      + ipv6_cidr_block                      = (known after apply)
      + ipv6_cidr_block_network_border_group = (known after apply)
      + main_route_table_id                  = (known after apply)
      + owner_id                             = (known after apply)
      + tags                                 = {
          + "Name" = "dev-vpc"
        }
      + tags_all                             = {
          + "Name" = "dev-vpc"
        }
    }
     
     ```
     
     ```
    aws_subnet.myapp-subnet-1 will be created
  + resource "aws_subnet" "myapp-subnet-1" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "ap-southeast-1b"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.10.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = {
          + "Name" = "dev-subnet-1"
        }
      + tags_all                                       = {
          + "Name" = "dev-subnet-1"
        }
      + vpc_id                                         = (known after apply)
    }
     
     
     ```
     
  ![AWS Management Console - Google Chrome 10-06-2023 10_50_48](https://github.com/Rajib-Mardi/terrraform/assets/96679708/207a2580-799f-4c11-8a87-81ecdbe81c6d)

  ![AWS Management Console - Google Chrome 10-06-2023 10_51_02](https://github.com/Rajib-Mardi/terrraform/assets/96679708/65d93871-a556-463a-ab87-6a756ef4887f)

  
*  Configured Default/Main Route Table
  ```
  # aws_default_route_table.main-rtb will be created
  + resource "aws_default_route_table" "main-rtb" {
      + arn                    = (known after apply)
      + default_route_table_id = (known after apply)
      + id                     = (known after apply)
      + owner_id               = (known after apply)
      + route                  = [
          + {
              + cidr_block                 = "0.0.0.0/0"
              + core_network_arn           = ""
              + destination_prefix_list_id = ""
              + egress_only_gateway_id     = ""
              + gateway_id                 = (known after apply)
              + instance_id                = ""
              + ipv6_cidr_block            = ""
              + nat_gateway_id             = ""
              + network_interface_id       = ""
              + transit_gateway_id         = ""
              + vpc_endpoint_id            = ""
              + vpc_peering_connection_id  = ""
            },
        ]
      + tags                   = {
          + "Name" = "dev-main-rtb"
        }
      + tags_all               = {
          + "Name" = "dev-main-rtb"
        }
      + vpc_id                 = (known after apply)
   
   }

```

```
 # aws_internet_gateway.my-app-igw will be created
  + resource "aws_internet_gateway" "my-app-igw" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = {
          + "Name" = "dev-igw"
        }
      + tags_all = {
          + "Name" = "dev-igw"
        }
      + vpc_id   = (known after apply)
    }
```
*  Configured Default Security Group

```
 # aws_default_security_group.default-sg will be created
  + resource "aws_default_security_group" "default-sg" {
      + arn                    = (known after apply)
      + description            = (known after apply)
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 8080
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 8080
            },
          + {
              + cidr_blocks      = [
                  + "202.173.124.209/32",
                ]
              + description      = ""
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = {
          + "Name" = "dev-default-sg"
        }
      + tags_all               = {
          + "Name" = "dev-default-sg"
        }
      + vpc_id                 = (known after apply)
    }

```

## Configure TF script to automate deploying Docker container to EC2 instance
Configured ssh key pair in Terraform config file

```
   # aws_key_pair.ssh-key will be created
  + resource "aws_key_pair" "ssh-key" {
      + arn             = (known after apply)
      + fingerprint     = (known after apply)
      + id              = (known after apply)
      + key_name        = "server-key"
      + key_name_prefix = (known after apply)
      + key_pair_id     = (known after apply)
      + key_type        = (known after apply)
      + public_key      = (known after apply)
      + tags_all        = (known after apply)
    }
```


creeate local file to store the ssh private key locally

```
# local_file.TF-key will be created
  + resource "local_file" "TF-key" {
      + content              = (sensitive value)
      + content_base64sha256 = (known after apply)
      + content_base64sha512 = (known after apply)
      + content_md5          = (known after apply)
      + content_sha1         = (known after apply)
      + content_sha256       = (known after apply)
      + content_sha512       = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "tfkey"
      + id                   = (known after apply)
    }

  # tls_private_key.rsa will be created
  + resource "tls_private_key" "rsa" {
      + algorithm                     = "RSA"
      + ecdsa_curve                   = "P224"
      + id                            = (known after apply)
      + private_key_openssh           = (sensitive value)
      + private_key_pem               = (sensitive value)
      + private_key_pem_pkcs8         = (sensitive value)
      + public_key_fingerprint_md5    = (known after apply)
      + public_key_fingerprint_sha256 = (known after apply)
      + public_key_openssh            = (known after apply)
      + public_key_pem                = (known after apply)
      + rsa_bits                      = 4096
    }


```
❏ Created EC2 Instance
- Fetch AMI

- restrict permission

```

  # aws_instance.myapp-server will be created
  + resource "aws_instance" "myapp-server" {
      + ami                                  = "ami-0d4430d42d5b76bcd"
      + arn                                  = (known after apply)
      + associate_public_ip_address          = true
      + availability_zone                    = "ap-southeast-1b"
      + cpu_core_count                       = (known after apply)
      + cpu_threads_per_core                 = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = "t2.micro"
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = "server-key"
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + source_dest_check                    = true
      + subnet_id                            = (known after apply)
      + tags                                 = {
          + "Name" = "dev-server"
        }
      + tags_all                             = {
          + "Name" = "dev-server"
        }
      + tenancy                              = (known after apply)
      + user_data                            = "644ca0c7857bc782dacbe44f92d4391002808961"
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)
    }
```


* SSH into EC2 instance
![ec2-user@ip-10-0-10-107_~ 12-06-2023 20_22_49](https://github.com/Rajib-Mardi/terrraform/assets/96679708/a0ead0f1-7ec5-48d9-a02c-5a6e93cf0909)


* Configured Terraform to install Docker and run nginx image
   *  Extract shell commands to own shell script
   *  create an "script.sh" file in terraform folder and write the linux commands to execute the shell script
   *  Accessed nginx through Browser
 
 
 ![Welcome to nginx! - Google Chrome 13-06-2023 00_57_09](https://github.com/Rajib-Mardi/terrraform/assets/96679708/8a2cb1ca-bf94-4f5d-84a5-f900a4979202)


    
    


