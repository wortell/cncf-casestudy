# Challenge

[Wortell](https://www.wortell.nl/en) is an IT Services company based in the Netherlands and Belgium. One of the services offered by Wortell is [Managed Detect and Response (MDR)](https://www.wortell.nl/en/products/managed-detection-and-response-en) which is operated 24/7/365 by a team of dedicated security professionals. The service is facilitated by a build for purpose home grown software solution running on dotnet, called Vidara, which handles multiple customers, MDR / SOC processes, automation, and more.

As the software matures, it becomes much harder to focus most engineering on the business processes as the infrastructure and application architecture evolve into a complex system.

# Solution

To deal with the ever increasing complexity of the application and infrastructure architecture, we started adopting dapr. As we where already using Kubernetes (Azure Kubernetes Service) and deploy our application with Helm charts, the side car architecture of dapr was an easy fit for us. At first we started utilizing the pub/sub component and over time we gradually started using other components as well. Currently we are using pub/sub, secrets and secure service to service communication and are planning on using the state component and policy feature in the near future.

# Impact

By adopting dapr, we where able to remove several software packages and a great deal of code from all of our microservice. This greatly reduces the complexity and amount of required infrastructure related code, allowing us to have more focus on the business features.

# Local Development made easy

Local development was simplified as well. We switched from running a local kubernetes cluster to using project Tye together with dapr. Doing this, we can easily use dapr component configurations (yaml files) reflecting local target systems without the need to reflect this in code anymore. For example, we used to have code paths that dealt with Azure Service Bus for dtap and RabbitMQ for local development, switching desired targets by supplying application configuration at startup. With dapr, we still target Azure Service Bus for dtap and we switched to redis for local development. The application code however isn't aware of any of this. Configuration and interfacing with these system is fully external to the application.

# Reducing application interfacing with infrastructure

We started using dapr in production with version 0.12 preview 1 on februari 2021 and have been growing the use of dapr in production since.

As we first adopted the pub/sub component, we where able to remove the packages dealing with Azure Service Bus and RabbitMQ. Next we started using the secrets component. As this component only deals with getting secrets, not setting them, we where able to remove the packages dealing with Azure KeyVault from all our services besides the one that deals with setting the secrets.

Service to service communication was next. Using service to service communication with dapr results in mTLS based communication with service auto discovery for free.

With newer versions of dapr, Azure Managed Identities became supported to have dapr components interface with Azure components without the need to have configured secrets. We started using AKS Managed Pod Identity together to provide dapr with the required managed identity access and since then, we don't have any secrets anymore in our application configuration / helm chart.

Most recently we adopted the dapr secret store configuration provider. This allows dapr to pre-fetch application specific secrets from any secrets provider (in our case, Azure KeyVault) and inject them into the application configuration for use. Remaining application secrets are now provided at startup removing the need to have any secrets in local application settings or configuration files.