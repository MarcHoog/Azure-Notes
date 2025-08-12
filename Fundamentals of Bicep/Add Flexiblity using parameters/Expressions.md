---
tags:
  - bicep
  - syntax
---

### Expressions

When you're writing Bicep files, you often don't want to hard-code values or ask for them to be specified in a parameter. Instead, you want to discover values when the file runs. For example, you probably want to deploy all of the resources in a Bicep file into a single Azure region: the region where you've created the resource group. Or, you might want to automatically create a unique name for a resource based on a particular naming strategy your company uses.

_Expressions_ in Bicep are a powerful feature that helps you handle all sorts of interesting scenarios. Let's take a look at a few places where you can use expressions in a Bicep file.
#### Resource locations

When you're writing and deploying a template, you often don't want to have to specify the location of every resource individually. Instead, you might have a simple business rule that says, _by default, deploy all resources into the same location in which the resource group was created_.

In Bicep, you can create a parameter called `location`, then use an expression to set its value:
```
param location string = resourceGroup().location
```

Look at the default value of that parameter. It uses a _function_ called `resourceGroup()` that gives you access to information about the resource group into which the Bicep file is being deployed. In this example, the file uses the `location` property. It's common to use this approach to deploy your resources into the same Azure region as the resource group.

If someone is deploying this Bicep file, they might choose to override the default value here and use a different location.

### Resource names

Many Azure resources need unique names. In your scenario, you have two resources that need unique names: the storage account and the App Service app. Asking for these values to be set as parameters can make it difficult for whoever uses the Bicep file because they need to find a name that nobody else has used.

Bicep has another function called `uniqueString()` that comes in handy when you're creating resource names. When you use this function, you need to provide a _seed value_, which should be different across different deployments, but consistent across all deployments for the same resources.

If you choose a good seed value, you can get the same name every time you deploy the same set of resources, but you'll get a different name whenever you deploy a different set of resources by using the same Bicep file. Let's look at how you might use the `uniqueString()` function:

```
param storageAccountName string = uniqueString(resourceGroup().id)
```

This parameter's default value uses the `resourceGroup()` function again, like you did when you set the resource location. This time, though, you're getting the ID for a resource group. Here's what a resource group ID looks like:
```
/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/MyResourceGroup
```

The resource group ID includes the Azure subscription ID (`aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e`) and the resource group name (`MyResourceGroup`). The resource group ID is often a good candidate for a seed value for resource names because:

- Every time you deploy the same resources, they'll go into the same resource group. The `uniqueString()` function will return the same value every time.
- If you deploy into two different resource groups in the Azure subscription, the `resourceGroup().id` value will be different because the resource group names will be different. The `uniqueString()` function will give different values for each set of resources.
- If you deploy into two different Azure subscriptions, _even if you use the same resource group name_, the `resourceGroup().id` value will be different because the Azure subscription ID will be different. The `uniqueString()`function will again give different values for each set of resources.

### Combined strings

If you just use the `uniqueString()` function to set resource names, you'll probably get unique names, but they won't be meaningful. A good resource name should also be descriptive, so that it's clear what the resource is for. You'll often want to create a name by combining a meaningful word or string with a unique value. This way, you'll have resources that have both meaningful _and_ unique names.

Bicep has a feature called _string interpolation_ that lets you combine strings. Let's see how it works:

BicepCopy

```
param storageAccountName string = 'toylaunch${uniqueString(resourceGroup().id)}'
```

The default value for the `storageAccountName` parameter now has two parts to it:

- `toylaunch` is a hard-coded string that helps anyone who looks at the deployed resource in Azure to understand the storage account's purpose.
- `${uniqueString(resourceGroup().id)}` is a way of telling Bicep to evaluate the output of the `uniqueString(resourceGroup().id)` function, then concatenate it into the string.