---
tags:
  - azure
  - bicep
---


## Why use infrastructure as code?

With infrastructure as code you can:

- Increase confidence in your deployments.
- Manage multiple environments.
- Better understand your cloud resources.
### Increase confidence

One of the benefits of using infrastructure as code is the level of confidence you gain in your deployments from improvements in consistency and security.

- **Integration with current processes**: If your organization already uses standard software development practices, <mark style="background: #FFB8EBA6;">you can adopt those same processes for your infrastructure deployments</mark>. 

- **Consistency**: Adopting an infrastructure as code approach helps your team follow well-established processes to deploy infrastructure. By following these processes, <mark style="background: #FFB8EBA6;">responsibility shifts from a small group of individuals to your automation process and tooling. Infrastructure as code helps reduce human error in resource provisioning and ensure consistent deployments.</mark>

- **Automated scanning**: <mark style="background: #FFB8EBA6;">You can scan Infrastructure-as-code configurations</mark> with automated tooling that can check for errors in the code. Automated tooling can also review proposed changes to ensure that security and performance practices are followed.

- **Secret management**: Many solutions require secrets, like connection strings, encryption keys, client secrets, and certificates. In Azure, an Azure Key Vault is the service that's used to securely store these secrets. Many <mark style="background: #FFB8EBA6;">infrastructure-as-code tools can integrate with Key Vault to access these secrets securely at deployment.</mark>

- **Access control**: <mark style="background: #FFB8EBA6;">With infrastructure-as-code deployments, you have the option of using managed identities or service accounts to automate resource provisioning. This process ensures that only these identities can modify your cloud resources.</mark> It also helps prevent incorrect configurations deployed to production. If necessary, you can override this process by using an emergency access account (often called a _break glass account_) or by using the Microsoft Entra ID Privileged Identity Management feature.

- **Avoid configuration drift**: _I<mark style="background: #FFB8EBA6;">dempotence_ is a term frequently associated with infrastructure as code. When an operation is idempotent, it means that it provides the same result each time you run it.</mark> If you choose tooling that uses idempotent operations, you can avoid configuration drift.
## Better understand your cloud resources

Infrastructure as code can help you better understand the state of your cloud resources:

- **Audit trail**: Changes to your infrastructure-as-code configurations are version controlled in the same way as your application source code. These changes are tracked in your tooling, like with Git's version history. This audit trail means that you can review the details of each change, who made the change, and when the change was made.
    
- **Documentation**: You can use many infrastructure-as-code configurations to add metadata, like comments, which describe the purpose of the code in your configuration. If your organization already follows a code documentation process, consider adopting these same procedures with your infrastructure code.
    
- **Unified system**: Many times, when a developer is working on a new feature, they must make changes to application code and infrastructure code. When you use a common system, your organization can better understand the relationship between your applications and your infrastructure.
    
- **Better understanding of cloud infrastructure**: When you use the Azure portal to provision resources, <mark style="background: #FFB8EBA6;">many of the processes are abstracted from view</mark>. Infrastructure as code can help provide a <mark style="background: #FFB8EBA6;">better understanding of how Azure works</mark> and how to troubleshoot issues that might arise. For example, when you create a virtual machine by using the Azure portal, some created resources are abstracted from view. Managed disks and network interface cards are deployed behind the scenes. When you deploy the same virtual machine by using infrastructure as code, you have complete control over all resources that are created.