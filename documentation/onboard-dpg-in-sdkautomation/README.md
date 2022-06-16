# Service Onboard DPG with Swagger CI Pipeline

Service Onboarding DPG with Swagger CI pipeline can help you get generated SDK and ApiView during the procedure of creating swagger PR.
The benefits are following:
1. API signature could be reviewed at the same time when we submit a Swagger PR. This could help to detect API issues at the early stage.
2. It enables service teams to access their SDKs even before their Swagger PR is merged.

This Document describes the process of how to onboard DPG with SDK automation pipeline. __This document is targeting for service team, who wants to onboard DPG.__ 

*If you want to go through details of pipeline implementation, please go to [Integrate DPG and ApiView in SDK Automation Pipeline](Integrate-dpg-and-apiview-in-sdk-automation-pipeline.md).*

## WorkFlow

![workflow-for-service-team](workflow-service-team.png)

__Description:__
1. Creates a swagger PR with [Guide to design and creation of Data Plane REST API and Client Libraries](https://aka.ms/azsdk/dpcodegen).
2. If you have added a comment, which contains autorest configuration, and run `/azp run` in the spec PR, the autorest configuration in the comment will be used to generate SDK.
Otherwise, pipeline will try to find autorest configuration file in sdk repository. If found, use the autorest configuration file to generate SDK. If not found, pipeline will stop.
   - Please refer to [Add autorest configuration in spec comment](./add-autorest-configuration-in-spec-comment.md) on how to add autorest configuration in spec comment.
3. SDK and ApiView will be generated in spec CI pipeline. Please refer to the [Guide of Reviewing the Api Design/Definition](https://dev.azure.com/azure-sdk/internal/_wiki/wikis/internal.wiki/591/Guide-to-design-and-creation-of-Data-Plane-REST-API-and-Client-Libraries?anchor=ii.-review-the-api-design/definition) to review the API definition.
4. If any change needed, please update the autorest configuration in spec PR comment and regenerate the SDK by adding a comment `/azp run` to swagger PR. Otherwise, go to [Next Steps After Generating Codes](./next-steps-after-generating-codes.md) if you want to do manual changes on generated codes.

## FAQ
 
1. What should I do when I encounter error in generating SDK in swagger PR CI pipeline?
   
    __Answer__: Please check the comment [Swagger Generation Artifacts] and the error message of failed pipeline. If you find the error messages ask you to fix autorest configuration comment or swagger, please fix it. If you cannot understand error message, please ask sdk owners for help with mail: azsdk-dpgsupport@microsoft.com.