# **GitHub Repository Naming Standards \- IaC**

| Format |  |  |  |
| :---- | :---: | :---- | :---- |
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

‘

# **Google Cloud Terraform Resource Naming Standards**

| Resource | Format |  |  |  |
| :---- | :---- | ----- | ----- | ----- |
| ***General*** | **resource-product-env***\[-desc\]\[-id\]* |  |  |  |

| Resource | Acronym | Format | Example | Notes |
| :---- | :---: | :---- | :---- | :---- |
| Project | \- | org-product*\[-env\]\[-desc\]\[-id\]* | nm-ace- | 30 character max |
| Shared VPC | vpcs | vpcs-product-env*\[-desc\]\[-id\]* | svpc-rcs-stg |  |
| VPC | vpc | vpc-product-env*\[-desc\]\[-id\]* | vpc-rcs-stg |  |
| Subnet | \- | vpc-product-env-region*\[-desc\]\[-id\]* | vpc-rcs-stg-us-central1-apps vpc-rcs-stg-us-central1-dbs or snet-rcs-stg-us-central1-apps snet-rcs-stg-us-central1-dbs |  |
| Firewall | fw | fw-product-env*\[-desc\]\[-id\]* | fw-rcs-stg-allow-ssh-rdp | Per VPC |
| NAT | nat | nat-product-env*\[-desc\]\[-id\]* | nat-rcs-prd | nat-config, per vpc, region so add region? |
| Router | rt | rt-product-env*\[-desc\]\[-id\]* | rtr-rcs-prd | nat-router, attached to a nat config |
| VM | vm | vm-product-env*\[-desc\]\[-id\]* | vm-rcs-sbx-0a1b | 63 character max |
| VM Name |  |  | dev-vm | No spaces, unique |
| ServiceAccount | sa | **sa-product-env-desc***\[-id\]* | sa-rcs-dev-gke | 30 character max |
| StorageBucket | sb | sb-\[organization|product\]-env-desc*\[-id\]* | sb-nm-prd-logs-0xa1 | 63 character max |
| Log Storage Bucket | lsb | lsb-product-env-desc*\[-id\]* | lsb-nm-prd-shared lsb-nm-nonprd-shared |  |
| Labels &Tags | \- | \\w+(-\\w+)\* | dev-server | Anything just use hyphens |
| IP Address | ip | ip-product-env-(ext|int)*\[-desc\]\[-id\]* | ip-rcs-dev-ext-ingress |  |
| Forwarding Rule | fwd | fwd-product-env-desc*\[-id\]* | fwd-rcs-dev-https-coreapp |  |
| Certificate | ssl | ssl-product-env-desc*\[-id\]* | ssl-rcs-sbx-appcreator |  |
| HealthCheck | hc | hc-product-env-desc*\[-id\]* | hc-rcs-sbx-ingress |  |
| Instance Group | ig | mig | k8s | (ig|mig|k8s)-product-env*\[-desc\]\[-id\]* | ig-rcs-dev-coreapp |  |
| URL Map | map |  | map-rcs-prd\[-desc\] |  |
| Backend Service | (ig | mig | k8s)-be |  | ig-be-rcs-prd\[-desc\] |  |
| Persistent Disk | pd |  | pd-rcs-prd\[-desc\] |  |
| Hyperdisk | hd |  |  |  |
| Local SSD | ssd |  |  |  |
| Analytics Hub | hub |  | hub-rcs-prd |  |

