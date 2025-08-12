---
tags:
  - bicep
  - azure
  - cmd
  - errors
---
## Content already consumed
``` bash
bubble@Mac templates % az deployment group create --name main --template-file main.bicep The content for this response was already consumed
```
Weird error that returns everytime azure is supposed to return an error. Git hub issue open about it: https://github.com/Azure/azure-cli/issues/31581 This case it was that the default thing and resource groups need to have a unique name



