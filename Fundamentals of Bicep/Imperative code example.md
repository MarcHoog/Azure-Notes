---
tags:
  - azure
  - bicep
  - cmd
---


In Azure, an imperative code approach is accomplished programmatically by using a scripting language like Bash or Azure PowerShell. The scripts execute a series of steps to create, modify, and even remove your resources.

This example shows two Azure CLI commands that create a resource group and a storage account.

Azure CLICopy

``` bash
#!/usr/bin/env bash
az group create \
  --name storage-resource-group \
  --location northeurope

az storage account create \
  --name mystorageaccount \
  --resource-group storage-resource-group \
  --location northeurope \
  --sku Standard_LRS \
  --kind StorageV2 \
  --access-tier Hot \
  --https-only true
```

The first command creates a resource group named `storage-resource-group` in the North Europe. The second command creates a storage account named `mystorageaccount` in the `storage-resource-group` resource group that was created in the first command. The second command also configures some properties for the storage account, including the kind of storage account and its access tier.

You can use an imperative approach to fully automate resource provisioning, but the approach has some disadvantages. <mark style="background: #FFB8EBA6;">As your architecture matures, scripts can become complex to manage. Commands could be updated or deprecated, which requires reviews of existing scripts.</mark>