---
tags:
  - azure
  - bicep
---
### Declarative code

In Azure, a declarative code approach is accomplished by using _templates_. Many types of templates are available to use, including:

- JSON
- Bicep
- Ansible, by RedHat
- Terraform, by HashiCorp

``` 
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-05-01' = {
  name: 'mystorageaccount'
  location: 'eastus'
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
  properties: {
    accessTier: 'Hot'
    supportsHttpsTrafficOnly: true
  }
}
```

The resources section defines the storage account configuration. This section contains the name, location, and properties of the storage account, including its SKU and the kind of account.

You might notice that the Bicep template doesn't specify how to deploy the storage account. <mark style="background: #FFB8EBA6;">It specifies only what the storage account needs to look like. The actual steps that are executed behind the scenes to create this storage account or to update it to match the specification are left for Azure to decide.</mark>