# Create Instance With Terraform

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
vim example.tf
```
### Configure Terraform File
```
terraform {
  required_providers {
    openstack = {
      source = "terraform-provider-openstack/openstack"
    }
  }
}

provider "openstack" {
  user_name = "your_openstack_username"
  tenant_name = "your_opensack_project_name"
  password = "your_openstack_password"
  auth_url = "your_openstack_Authentication_URL"
  insecure = true
}

resource "openstack_compute_instance_v2" "test-server" {
  name = "test-server"
  image_id = "c861958a-0ec5-4b43-b337-7b85314c63c9"
  flavor_name = "a1-ram2-disk80-perf1"
  key_pair = "alex-ssh"
  security_groups = ["default"]

  network {
    name = "ext-net1"
  }
}
```
### Launch Instance with Terraform
```
terraform init
terraform plan
terraform apply
```
