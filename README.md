![Wortell Logo](images/wortell-logo.png)

|||
|-----|-----|
|**Challenges:**|Complexity, Reliability, Stability|
|**Industry:**|Security, Information Technology|
|**Location:**|Netherlands, Belgium, Luxembourg|
|**Cloud Type**|Public|
|**Product Type:**|SaaS, Managed Detection and Response, SOC|
|**Projects Used:**|Dapr, Kubernetes, Helm|

# Challenge

Vidara, Wortell's Managed Detection and Response software, increases in complexity over time due to introduction of new futures and services. Interaction with Cloud Resources for things like asynchronous messaging is a major part of the application architecture as it is build on many micro services. All of these Cloud Resources have their own SDK and required knowledge attached. Evolving the software requires more and more specialized expertise and time from the developers, impacting time spend on the actual business goals

# Solution

To deal with the ever-increasing complexity of the application and infrastructure architecture, Wortell adopted [**Dapr**](https://dapr.io/). Dapr solves many of the responsibilities of interacting with infrastructure and simplifies the inter-application communication. As the Vidara team were already using Kubernetes (Azure Kubernetes Service, AKS) and deployed their application with Helm charts, the sidecar architecture of Dapr was an easy fit for them to use. At first they started utilizing the pub/sub API and component and over time they gradually started using the other API components as well. Currently, the team are using pub/sub, secrets, secure service-to-service invocation and they are planning on using the state management API and policy features in the near future.

# Impact

By adopting Dapr, the Vidara team were able to remove several software packages and a considerable amount of code from all of their microservices. They adopted the simple Dapr APIs from the [.NET SDK](https://docs.dapr.io/developing-applications/sdks/dotnet/) and thereby offloaded dealing with the infrastructure integration and async inter-process communication to the Dapr runtime. This greatly reduced the complexity and amount of required infrastructure related code, allowing them to have more focus on the business features.

## By the numbers...

||||
|-|-|-|
**Reduction in SDK use**|**Number 2**|**Number 3**|
By using Dapr, x 3rd partySDKs are no longer required to be used.|description2 |description 3|