# Module 12 - Best Practices

[< Previous Module](../modules/module11.md) - **[Home](../README.md)** - [Next Module >](../modules/module13.md)

Whitepapers that related to Azure Data Factory are published on [Microsoft Learn: Azure Data Factory whitepapers](https://learn.microsoft.com/en-us/azure/data-factory/whitepapers).

In addition to that published content, here are a few best practices to consider:

1. Define Data Factory boundary strategy. Here are 4 common boundaries:
    - Modular, or template, logic for common pipeline activitites (can be owned at the enterprise, department, or team levels).
    - Department owned Data Factory used for multiple projects.
    - Team owned Data Factory.
    - Project-specific Data Factory.
1. Define the security and/or data access model. Here are a few things to consider:
    - Azure Data Factory security [certifications](https://learn.microsoft.com/en-us/azure/data-factory/data-movement-security-considerations)
    - The SaaS model is fully secured and is referred to as the Private Link access strategy. See [the full list of access strategies](https://learn.microsoft.com/en-us/azure/data-factory/data-access-strategies#data-access-strategies-through-azure-data-factory) and [Choose the right integration runtime configuration for your scenario](https://learn.microsoft.com/en-us/azure/data-factory/choose-the-right-integration-runtime-configuration) to help you decide.
1. Never store credentials in the clear: 
    - Integrate Azure Data Factory with Azure Key Vault
    - Set the activity Secure input and Secure output settings appropriately for any activity through which credentials pass
    - Remember to set the encryption property to True for any parameter, variable, or global setting that stores credential information.
    - For connection strings that are parameterized, include an encryption property wehre appropriate. See ["Data encryption in transit" notes](https://learn.microsoft.com/en-us/azure/data-factory/data-movement-security-considerations#data-encryption-in-transit).
1. Create common observability standards
    - Monitor and troubleshoot performance
    - Use the same Log Analytics instance when configuring diagnostic settings.
    - Consider creating custom logging and error paths to give operational teams the detail needed to fix failures. These handlers can be wrapped up as template pipelines.
1. Follow modern development practices:
    - Connect Data Factory with Azure DevOps or GitHub.
    - Innersource as much as possible by sharing source code repository access
    - Create and socialize Azure Data Factory Template Gallery templates
    - Practice code review.
    - Implement continous integration and deployment (CI/CD) with at least 1 non-production environment.
1. Build it to be robust: Set appropriate Timeout and Retry values in activities.
1. Leverage schema drift where possible so source changes don't break downstream consumption.
1. Integrate Data Factory with data governance tooling for optimzied trust in the data.



[Continue >](../modules/module13.md)