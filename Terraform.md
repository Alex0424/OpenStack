# Create an Simple Instance With Terraform

### recomended to have openstack client so you can work faster

download "OpenStack RC File" from horizon API Access
```
source project_name-openrc.sh #enter you openstack password
sudo apt install python3-openstackclient
```
### Usefull commands for this tutorial
```
openstack flavor list
openstack image list
openstack keypair list
openstack network list
openstack security group list
openstack router list
openstack server list
```
### Download Terraform on linux terminal
visit https://developer.hashicorp.com/terraform/install?product_intent=terraform#linux
```
wget terraform_link
unzip your_terraform_version.zip
sudo chown root:root terraform
sudo mv terraform /usr/local/bin/
```
### Create Directory And Terraform File
```
mkdir terraform-directory && cd terraform-directory
```
### Create and configure main Terraform File
```
vim main.tf
```
```
# Select openstack as our provider
terraform {
  required_providers {
    openstack = {
      source  = "terraform-provider-openstack/openstack"
    }
  }
}

# Openstack provider
provider "openstack" {
  user_name   = var.openstack_username
  tenant_name = var.openstack_project
  password    = var.openstack_user_password
  auth_url    = var.openstack_auth_url
  insecure    = true
}
# Compute instance
resource "openstack_compute_instance_v2" "instance_name" {
  name            = "instance_name"
  image_id        = "your_image_id"
  flavor_name     = "your_instance"
  key_pair        = "yur_pair_name"
  security_groups = [openstack_compute_secgroup_v2.secgroup_1.name]

  network {
    name = "your external network"
  }
}

# Security Groups
resource "openstack_compute_secgroup_v2" "secgroup_1" {
  name        = "my_secgroup"
  description = "my security group"

  rule {
    from_port   = 22
    to_port     = 22
    ip_protocol = "tcp"
    cidr        = var.administrator_ip
  }

  rule {
    from_port   = 80
    to_port     = 80
    ip_protocol = "tcp"
    cidr        = "0.0.0.0/0"
  }
}
```
### Create and configure Variables Terraform File
```
vim variables.tf
```
```
variable "administrator_ip" {
  type    = string
  default = "0.0.0.0/0"
}

variable "openstack_auth_url" {
  type    = string
  default = "your_auth_url"
}

variable "openstack_project" {
  type    = string
  default = "your_project_name"
}

variable "openstack_username" {
  type    = string
  default = "your_username"
}

variable "openstack_user_password" {
  type    = string
  default = "your_password"
}
```
### Launch Instance with Terraform
```
terraform init
terraform plan
terraform apply
```
### Smart and time saving commands
```
terraform fmt && terraform validate
```
updates configurations in the current directory for readability and consistency.
### Tutorials And Documentation

https://opensource.com/article/23/1/terraform-manage-openstack-cluster

https://registry.terraform.io/providers/terraform-provider-openstack/openstack/latest/docs

https://github.com/elastx/getting-started-elx-openstack/tree/master/01_Router_Networking
