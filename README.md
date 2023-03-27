

<p align="center">
  <img src="./images/logo-classicblue-800px.png" alt="Intel Logo" width="250"/>
</p>

# Intel® Cloud Optimization Modules for Terraform

© Copyright 2022, Intel Corporation

## Amazon ECS MOdule
In this module we create a ECS cluster utilizing the latest Intel Architecture available for the AWS ECS Service.  

## Usage

See examples folder for code ./examples/complete_example/main.tf

Example of main.tf

```hcl
provider "aws" {
  region = local.region
}

locals {
  region        = "us-east-1"
  name          = "ecs-ex-${replace(basename(path.cwd), "_", "-")}"
  duration      = 24
  instance_type = "m6i.large"
  #instance_type = ["m6i.large", "c6i.large", "m6i.2xlarge", "r6i.large"]
  user_data = <<-EOT
    #!/bin/bash
    cat <<'EOF' >> /etc/ecs/ecs.config
    ECS_CLUSTER=${local.name}
    ECS_LOGLEVEL=debug
    EOF
  EOT

  tags = {
    Owner    = local.name
    Name     = local.name
    Duration = local.duration
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