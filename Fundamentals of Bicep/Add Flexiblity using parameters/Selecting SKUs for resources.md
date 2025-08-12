### Selecting SKUs for resources

The other members of your team are impressed with the Bicep code you've built so far. You've decided together that you'll use your Bicep file to deploy the resources to support all your new toy launches.

One of your colleagues has suggested that you create non-production environments for each product launch to help the marketing team test the sites before they're available to customers. However, you want to make sure you don't spend too much money on your non-production environments, so you decide on some policies together:

- In production environments, storage accounts will be deployed at the `Standard_GRS` (geo-redundant storage) SKU for high resiliency. App Service plans will be deployed at the `P2v3` SKU for high performance.
- In non-production environments, storage accounts will be deployed at the `Standard_LRS` (locally redundant storage) SKU. App Service plans will be deployed at the free `F1` SKU.

One way to implement these business requirements is to use parameters to specify each SKU. However, specifying every SKU as a parameter can become difficult to manage, especially when you have larger Bicep files. Another option is to embed the business rules into the file by using a combination of parameters, variables, and expressions.

First, you can specify a parameter that indicates whether the deployment is for a production or non-production environment:

BicepCopy

```
@allowed([
  'nonprod'
  'prod'
])
param environmentType string
```

Notice that this code uses some new syntax to specify a list of _allowed values_ for the `environmentType` parameter. Bicep won't let anyone deploy the Bicep file unless they provide one of these values.

Next, you can create variables that determine the SKUs to use for the storage account and App Service plan based on the environment:

BicepCopy

```
var storageAccountSkuName = (environmentType == 'prod') ? 'Standard_GRS' : 'Standard_LRS'
var appServicePlanSkuName = (environmentType == 'prod') ? 'P2V3' : 'F1'
```

Notice some new syntax here, too. Let's break it down:

- `(environmentType == 'prod')` evaluates to a Boolean (true or false) value, depending on which allowed value is used for `environmentType` parameter.
- `?` is called a _ternary operator_, and it evaluates an `if/then` statement. The value after the `?` operator is used if the expression is true. If the expression evaluates to false, the value after the colon (`:`) is used.

We can translate these rules to:

- For the `storageAccountSkuName` variable, if the `environmentType` parameter is set to `prod`, then use the `Standard_GRS` SKU. Otherwise, use the `Standard_LRS` SKU.
- For the `appServicePlanSkuName` variable, if the `environmentType` parameter is set to `prod`, then use the `P2V3` SKU and the `PremiumV3` tier. Otherwise, use the `F1` SKU.