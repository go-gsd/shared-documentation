# GitHub Repository Naming Standards

## Infrastructure as Code (IaC) Repositories

### Naming Format

**General Format:** `org-language-provider-product[-env][-desc]`

- All values are lowercase, separated by hyphens
- Environment and description components are optional
- Use descriptive names that clearly indicate the repository's purpose

### Components

| Component | Required? | Description | Examples |
|-----------|-----------|-------------|----------|
| **org** | Yes | The name of the organization, written in lowercase | nm, gsd, bcg, mos |
| **language** | Yes | The IaC language being used, written in lowercase | terraform, opentofu, pulumi, crossplane |
| **provider** | Yes | The cloud provider, written in lowercase | gcp, aws, az |
| **product** | Yes | The product name or purpose of the repository, written in lowercase | lighthouse, logging, bootstrap, genai, widgetapi |
| **env** | No | The deployment environment, written in lowercase | sbx, dev, stg, prd |
| **desc** | No | Additional description of the repository | module, sample, multi, single |

### Examples

#### Cloud Foundations
- `nm-terraform-gcp-bootstrap`

#### Environment-Based Products
- `bcg-terraform-gcp-lighthouse-dev`
- `bcg-terraform-gcp-lighthouse-prd`
- `gsd-pulumi-gcp-genai-sbx`
- `gsd-pulumi-aws-widgetapi-sbx`

#### Multi-Tenant and Single-Tenant Instances
- `mos-terraform-az-coremulti-dev`
- `mos-terraform-az-coremulti-stg`
- `mos-terraform-az-coremulti-prd`
- `mos-terraform-az-coresingle-dtag`
