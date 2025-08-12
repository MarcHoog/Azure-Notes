---
tags:
  - bicep
  - syntax
---
Bicep modules allow you to organize and reuse your Bicep code by creating smaller units that can be composed into a Bicep file. Any Bicep file can be used as a module by another template. Throughout this learning module, you've created Bicep files. That means you've already created files that can be used as Bicep modules!


Imagine you have a Bicep file that deploys application, database, and networking resources for _solution A_. You might split this Bicep file into three modules, each of which is focused on its own set of resources. As a bonus, you can now reuse the modules in other templates for other solutions too; so when you develop a file for _solution B_, which has similar networking requirements to _solution A_, you can reuse the network module.

![Diagram that shows a Bicep file for solution A referencing three modules: application, database, and networking. The networking module is then reused in another Bicep file for solution B.](https://learn.microsoft.com/en-us/training/modules/includes/media/bicep-files-modules.png)

When you want the Bicep file to include a reference to a module file, use the `module` keyword. A module definition looks similar to a resource declaration, but instead of including a resource type and API version, you'll use the module's file name:

```
module myModule 'modules/mymodule.bicep' = {
  name: 'MyModule'
  params: {
    location: location
  }
}
```

Let's look closely at some key parts of this module definition:

- The `module` keyword tells Bicep you're about to use another Bicep file as a module.
- Just like resources, modules need a _symbolic name_ like `myModule`. You'll use the symbolic name when you refer to the module's outputs in other parts of the Bicep file.
- `modules/mymodule.bicep` is the path to the module Bicep file, relative to the file. Remember, a module file is just a regular Bicep file.
- Just like resources, the `name` property is mandatory. Azure uses the module name because it creates a separate deployment for each module within the Bicep file. Those deployments have names you can use to identify them.
- You can specify any _parameters_ of the module by using the `params` keyword. When you set the values of each parameter within the Bicep file, you can use expressions, file parameters, variables, properties of resources deployed within the file and outputs from other modules. Bicep will automatically understand the dependencies between the resources.
## Modules and outputs

Just like templates, Bicep modules can define outputs. It's common to chain modules together within a template. In that case, the output from one module can be a parameter for another module. By using modules and outputs together, you can create powerful and reusable Bicep files.

## Design your modules

A good Bicep module follows some key principles:

- **A module should have a clear purpose.** You can use modules to define all of the resources related to a specific part of your solution. For example, you might create a module that contains all of the resources used to monitor your application. You might also use a module to define a set of resources that belong together, like all of your database servers and databases.
    
- **Don't put every resource into its own module.** You shouldn't create a separate module for every resource you deploy. If you have a resource that has many complex properties, it might make sense to put that resource into its own module, but in general, it's better for modules to combine multiple resources.
    
- **A module should have clear parameters and outputs that make sense.** Consider the purpose of the module. Think about whether the module should manipulate parameter values, or whether the parent Bicep file should handle that, and then pass a single value through to the module. Similarly, think about the outputs a module should return, and make sure they're useful to the Bicep files that'll use the module.
    
- **A module should be as self-contained as possible.** If a module needs to use a variable to define a part of a module, the variable should generally be included in the module Bicep file rather than in the parent Bicep file.
    
- **A module shouldn't output secrets.** Just like templates, don't create module outputs for secret values like connection strings or keys.