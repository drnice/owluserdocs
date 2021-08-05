# Role Based Access Control \(RBAC\)

### RBAC Usages <a id="HRBACUsages"></a>

Owl supports RBAC configuration with both core roles and custom roles. Core roles include the following:

| Role | Access Description |
| :--- | :--- |
| ROLE ADMIN | Modify any access, config settings, connections, role delegation |
| ROLE DATA GOVERNANCE MANAGER | Ability to manage \(create / update / delete\) Business Units and Data Concepts |
| ROLE USER MANAGER | Create / modify users, add users to roles |
| ROLE OWL ROLE MANAGER | Create roles, edit role mappings to users / AD groups / datasets |
| ROLE DATASET MANAGER | Create / modify datasets to roles, masking of dataset columns |
| ROLE OWL CHECK | Only role that can run DQ scans if Owlcheck security is enabled |
| ROLE DATA PREVIEW | Only role that can view source data if data preview security is enabled |
| ROLE DATASET TRAIN | Only role that can train datasets if dataset train security is enabled |
| ROLE DATASET RULES | Only role that can add / edit / delete rules if dataset rules security is enabled |
| ROLE PUBLIC | Public: Access to scorecards, no dataset access when dataset security is enabled |

Custom roles can be added via the Role Management page by navigating to the Admin Console and clicking on the Roles Icon. Custom roles can also be added 'on the fly' during the Active Directory Role Mapping step.

It is these custom roles that will determine the users that have access to datasets \(including profile/rules/data preview/scoring\), and database connections

Additional information regarding setting up Dataset and Connection security can be found in those documents respectively.

