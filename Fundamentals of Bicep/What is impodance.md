---
tags:
  - azure
  - bicep
---
## Impodance 

``` bash
az group create --name storage-resource-group --location northeurope
```

<mark style="background: #FFB8EBA6;">If you run this command twice you receive the exact same output because this Azure CLI command was designed to be idempotent.</mark> You don't receive an error or a duplicate resource group.

When you use infrastructure as code, you can redeploy your environment at each release of your solution. These releases might incorporate small configuration changes or even significant updates. This process helps avoid configuration drift. If an accidental change is made to a resource, it can be corrected by redeploying the configuration. <mark style="background: #FFB8EBA6;">By following this approach, you're documenting your environment by using code.</mark>