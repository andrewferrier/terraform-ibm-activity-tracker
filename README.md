# Activity Tracker terraform module

Terraform module to provision Activity Tracker on IBM Cloud.

If an existing instance of the activity tracker service already exists within the user's account in the specified region, then creation will **NOT** fail, and the outputs of this module will be the values of the existing instnace, not of a newly created instance. 

**Note:** This module follows the Terraform conventions regarding how provider configuration is defined within the Terraform template and passed into the module - https://www.terraform.io/docs/language/modules/develop/providers.html. The default provider configuration flows through to the module. If different configuration is required for a module, it can be explicitly passed in the `providers` block of the module - https://www.terraform.io/docs/language/modules/develop/providers.html#passing-providers-explicitly.

## Software dependencies

The module depends on the following software components:

### Command-line tools

- terraform - v13

### Terraform providers

- IBM Cloud provider >= 1.5.3

## Module dependencies

None

## Example usage

```hcl-terraform
terraform {
  required_providers {
    ibm = {
      source = "ibm-cloud/ibm"
    }
  }
  required_version = ">= 0.13"
}

provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
  region = var.region
}

module "dev_activity-tracker" {
  source = "github.com/ibm-garage-cloud/terraform-ibm-activity-tracker"

  resource_group_name = var.resource_group_name
  resource_location   = var.region
  tags                = []
  plan                = "7-day"             
}
```

