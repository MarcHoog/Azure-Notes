---
tags:
  - bicep
  - syntax
---
## Add flexibility by using parameters and variables

Bicep files are powerful because of their reusability. You can use Bicep to write files that deploy multiple environments or copies of your resources.

A _parameter_ lets you bring in values from outside the Bicep file. For example, if you're manually deploying the file by using the Azure CLI or Azure PowerShell, you'll be asked to provide values for each parameter. You can also create a _parameter file_, which lists all of the parameters and values you want to use for the deployment. If the Bicep file is deployed from an automated process like a deployment pipeline, the pipeline can provide the parameter values.

A _variable_ is defined and set within the Bicep file. Variables let you store important information in one place and refer to it throughout the file without having to copy and paste it.

It's usually a good idea to use parameters for things that will change between each deployment, like:

- Resource names that need to be unique.
- Locations into which to deploy the resources.
- Settings that affect the pricing of resources, like their SKUs, pricing tiers, and instance counts.
- Credentials and information needed to access other systems that aren't defined in the Bicep file.

Variables are usually a good option when you'll use the same values for each deployment, but you want to make a value reusable within the file or when you want to use expressions to create a complex value. You can also use variables for resources that don't need unique names.
