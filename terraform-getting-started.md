# Getting Started with Terraform

## Learning Objectives

After completing this tutorial, you will learn to:

- Describe downloading and installing Terraform
- Perform creating infrastructure
- Verify an infrastructure installation
- Perform destroying infrastructure

## Prerequisites

- A computer with an internet connection
- A hard drive with at least 80mb of free space
- An unzip utility


## Install Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC).

To install Terraform, find the [appropriate package](https://www.terraform.io/downloads.html) for your system and download the file.

## Create infrastructure

Now that you've installed Terraform, you can now start creating infrastructure.

Create a new directory named `terraform-demo`.

Then change directory to `terraform-demo`.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file and name it `main.tf`.

```shell
$ touch main.tf
```

Paste the following Terraform configuration into the file `main.tf`.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `init` command, which installs the NGINX server container.

```shell
$ terraform init
```

## Verify the installation

Check for any errors. If successful, provision the resource with `apply`.

```shell
$ terraform apply
```

The command will take a few minutes to run and will display a message indicating that the resource was created.

## Destroy infrastructure

To destroy the infrastructure, run `terraform destroy`.

```shell
$ terraform destroy
```

When Terraform asks you to confirm type `yes` and press `ENTER`.

You've now provisioned and destroyed an NGINX webserver with Terraform.

## Next Steps

Next, you will create real infrastructure in the cloud of your choice.

- [Amazon Web Services (AWS)](https://learn.hashicorp.com/tutorials/terraform/aws-build)
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-build)
- [Google Cloud Platform (GCP)](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-build)
- [Oracle Cloud Platform (OCI)](https://learn.hashicorp.com/tutorials/terraform/oci-build)
