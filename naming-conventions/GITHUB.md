# GitHub Repository Naming Standards

## IaC
| General Format                                                                      |
|-------------------------------------------------------------------------------------|


| Format |  |  |  |
| **org-language-provider-product*\[-env\]\[-desc\]*** |  |  |  |
| All values are lowercase, separated by a hyphen. The environment component is optional. |  |  |  |
| **Component** | **Required?** | **Description** | **Examples** |
| **org** | Yes | The name of the organization, written in lowercase  | nm, gsd |
| **language** | Yes | Refers to the IaC language being used, written in lowercase  | terraform, opentofu, pulumi, crossplane |
| **provider** | Yes | The cloud provider, written in lowercase  | gcp, aws, az |
| **product**(or purpose) | Yes | The product name or the purpose of the repository, written in lowercase  | lighthouse, logging, bootstrap |
| **env** | No | Indicates the deployment environment, written in lowercase | sbx, dev, stg, prd |
| **desc** | No | A description of the repository | module, sample |
| **Examples** |  |  |  |
| Cloud foundations required for a product (or product suite) *nm-terraform-gcp-bootstrap* Product (or product suite) that is environment-based *bcg-terraform-gcp-lighthouse-dev bcg-terraform-gcp-lighthouse-prd gsd-pulumi-gcp-genai-sbx gsd-pulumi-aws-widgetapi-sbx* Product (or product suite) that supports single-tenant and multi-tenant cloud instances *mos-terraform-az-coremulti-dev mos-terraform-az-coremulti-stg mos-terraform-az-coremulti-prd mos-terraform-az-coresingle-dtag* |  |  |  |
