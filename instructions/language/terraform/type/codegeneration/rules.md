

The rules below this line apply only to Terraform code generation:
- The terraform syntax should match the version 1.5.5 or greater
- Resources in the azuread provider should always match the syntax of version 3.0 or greater
- Resources in the azurerm provider should always match the syntax of version 4.0 or greater
- Terraform symbolical names, variable and local names should use snake_case to separate words
- Using locals over variables is preferred when possible
- azurerm_role_assignment resources should explicitly specifiy 'principal_type' attribute
- for_each is preferred over count for resource iteration, except when evaluating a boolean expression
- for_each iterator should be human readable if possible, for instance it is easier for humans to read user_principal_name compared to object_id:
  - ```hcl
  - for_each         = { for user in data.azuread_users.readers.users : user.user_principal_name => user.object_id }
  - ``` 