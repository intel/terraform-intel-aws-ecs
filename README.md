

<p align="center">
  <img src="https://github.com/intel/terraform-intel-aws-mysql/blob/main/images/logo-classicblue-800px.png?raw=true" alt="Intel Logo" width="250"/>
</p>

# Intel® Cloud Optimization Modules for Terraform

© Copyright 2022, Intel Corporation

## Amazon ECS MOdule
In this module we create a ECS cluster utilizing the latest Intel Architecture available for the AWS ECS Service.  

## Usage

See examples folder for code ./examples/ec2-managed-example/main.tf

Example of main.tf

```hcl
locals {
  region        = "us-east-1"
  name          = "cluster-prod"
  instance_type = "m6i.large"
# See above recommended instance types for Intel Xeon 3rd Generation Scalable processors (code-named Ice Lake)
  user_data = <<-EOT
    #!/bin/bash
    cat <<'EOF' >> /etc/ecs/ecs.config
    ECS_CLUSTER=${local.name}
    ECS_LOGLEVEL=debug
    EOF
  EOT

  tags = {
    Owner    = "user@company.com"
    Duration = "24"
  }
}
```

Run Terraform

```hcl
terraform init  
terraform plan
terraform apply

```

Note that this example may create resources. Run `terraform destroy` when you don't need these resources anymore.

## Considerations  