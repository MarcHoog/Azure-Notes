A human can manually deploy Bicep files, or some sort of automated release process can deploy them. Either way, it's common to have some data from the file you need to send back to whoever or whatever is executing the file deployment.

Here are some example scenarios where you might need to get information from the Bicep file deployment:

- You create a Bicep file that deploys a virtual machine, and you need to get the public IP address so you can SSH into the machine.
- You create a Bicep file that accepts a set of parameters, like an environment name and an application name. The file uses an expression to name an Azure App Service app that it deploys. You need to output the app's name that the file has deployed so you can use it within a deployment pipeline to publish the application binaries.

You can use outputs for these scenarios. To define an output in a Bicep file, use the `output` keyword like this:

BicepCopy

```
output appServiceAppName string = appServiceAppName
```

The output definition includes a few key parts:

- The `output` keyword tells Bicep you're defining an output.
- `appServiceAppName` is the output's name. When someone deploys the Bicep file successfully, the output values include the name you specified so they can access the values they're expecting.
- `string` is the output type. Bicep outputs support the same types as parameters.
- A value must be specified for each output. Unlike parameters, outputs always need to have values. Output values can be expressions, references to parameters or variables, or properties of resources that are deployed within the file.

Here's another example of an output. This one will have its value set to the fully qualified domain name (FQDN) of a public IP address resource.

BicepCopy

```
output ipFqdn string = publicIPAddress.properties.dnsSettings.fqdn
```