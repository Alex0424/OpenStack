# Create an Simple Instance With Terraform

### Download Terraform on linux terminal
visit https://developer.hashicorp.com/terraform/install?product_intent=terraform#linux
```
unzip your_terraform_version.zip
sudo chown root:root terraform
sudo mv terraform /usr/local/bin/
```
### Create Directory And Terraform File
```
mkdir terraform-directory & cd terraform-directory
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
# Configure the openstack provider
provider "openstack" {
  user_name   = var.openstack_username
  tenant_name = var.openstack_project
  password    = var.openstack_user_password
  auth_url    = var.openstack_auth_url
  insecure    = true
}
#Configure the compute instance
resource "openstack_compute_instance_v2" "test-server" {
  name            = "instance_name"
  image_id        = "your_image_id"
  flavor_name     = "your_instance"
  key_pair        = "yur_pair_name"
  security_groups = ["default"]

  network {
    name = "your external network"
  }
}
```
### Create and configure Variables Terraform File
```
vim variables.tf
```
```
variable "administrator_ip" {
  type = string
  default = "0,0,0,0/0"
}

variable "openstack_auth_url" {
  type = string
  default = "your_auth_url"
}

variable "openstack_project" {
  type = string
  default = "your_project_name"
}

variable "openstack_username" {
  type = string
  default = "your_username"
}

variable "openstack_user_password" {
  type = string
  default = "your_password"
}
```
### Launch Instance with Terraform
```
terraform init
terraform plan
terraform apply
```
