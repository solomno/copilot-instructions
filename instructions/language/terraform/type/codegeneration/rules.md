The rules below this line apply only to Terraform code generation:
- Our resources should not specify tags.
- Our resource should specify general properties such as name, display_name, location, and resource_group_name at the top of the resource block (if required)
- Do not specify provider blocks when asked to generate resources, assume these are set in other files
- Do not generate locals named "workload", "subnets" or "generated_suffix", these already exist. The subnets local uses the function `cidrsubnets` over an allocated range.
- Do not generate virtual networks, subnets,private endpoints, NICs or other resources outside modules unless asked to do so, otherwise, assume these are already in place
- Do not generate code containing passwords
- location parameters should be = `module.shared.resource_location["default_region"]`
- The terraform syntax should match the version 1.5.5 or greater
- Resources in the azuread provider should always match the syntax of version 3.0 or greater
- Resources in the azurerm provider should always match the syntax of version 4.0 or greater
- We do not use the `data "azuread_client_config"` resource
- We do not explicitly set tenant_id, assume this is set already
- Assume existing azuread_group data resources have the following symbolic and display names:
  - `readers` = display_name = "az rbac sub ${local.workload} readers"
  - `contributors` = display_name = "az rbac sub ${local.workload} contributors"
  - `owners` = display_name = "az rbac sub ${local.workload} owners"
  - `workload_identities = display_name = "aks rbac ns ${local.env}-aks-${local.repo} workload identities"`
- If child resources for storage accounts or key vaults are created, they should be generated using the `azure/azapi` Terraform provider
- Terraform symbolical names, variable and local names should use snake_case to separate words
- Terraform resource and data properties should use generic names and use locals to supply the specific values where needed.
- Azure key vaults uses RBAC for access control, and should not use access policies
- Use locals over variables is preferred when possible
- Prefer using modules from the terraform registry over local modules. The registry modules should be sources from `miljodir`, e.g.
    - ```hcl
    module "sql" {
        source  = "miljodir/sql-server/azurerm"
        version = "~> 1.0"
    ...
    }
    ```
    - Use default values from the module, do not specify more optional values than required
    - For modules, the p-dns provider should be specified ```hcl
      providers = {
        azurerm.p-dns = azurerm.p-dns
     }
    ```
- Do not create azurerm_role_assignment resources unless asked to
- azurerm_role_assignment resources should explicitly specifiy 'principal_type' attribute
- azurerm_role_assignment resources should never be granted to user objects, only groups or service principals
- for_each is preferred over count for resource iteration, except when evaluating a boolean expression
- Do not use for_each unless iterating over multiple object