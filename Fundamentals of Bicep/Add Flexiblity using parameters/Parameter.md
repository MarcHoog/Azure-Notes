---
tags:
  - bicep
  - syntax
---
Add a parameter
In Bicep, you can define a parameter like this:
```
param appServiceAppName string
```
Let's look at how each part of this definition works:
- `param` tells Bicep that you're defining a parameter.
- `appServiceAppName` is the name of the parameter. If you're deploying the Bicep file manually, you might be asked to enter a value, so it's important that the name is clear and understandable. The name is also how you refer to the parameter value within the file, just like with resource symbolic names.
- `string` is the type of the parameter. You can specify several different types for Bicep parameters, including `string`for text, `int` for numbers, and `bool` for Boolean true or false values. You can also pass in more complex parameters by using the `array` and `object` types.

### Provide default values

You can optionally provide a _default value_ for a parameter. When you specify a default value, the parameter becomes optional. The person who's deploying the Bicep file can specify a value if they want, but if they don't, Bicep uses the default value.
Here's how you can add a default value:

```
param appServiceAppName string = 'toy-product-launch-1'
```