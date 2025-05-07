---
title: "BambooHR Microsoft 365 Copilot connector"
ms.author: shivansingh
author: shivaniolso
manager: helgesol
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: Medium
search.appverid:
- BFB160
- MET150
- MOE150
description: "Set up the BambooHR Microsoft 365 Copilot connector."
ms.date: 04/07/2025
---

# BambooHR Microsoft 365 Copilot connector

The BambooHR Microsoft 365 Copilot connector allows organizations to index profiles from BambooHR into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot. 

This guide is for Microsoft 365 administrators or anyone responsible for configuring, managing, and monitoring the BambooHR Copilot connector. 

## Capabilities

- Index profile information from BambooHR.
- Enable your end users to ask questions related to BambooHR profiles. 
- Use [Semantic search](https://learn.microsoft.com/en-us/microsoftsearch/semantic-index-for-copilot) in Copilot to enable users to find relevant profiles based on keywords, personal preferences, and social connections. 

## Limitations

- Time off, documents, benefits, trainings, assets, notes, emergency, onboarding, offboarding, and custom properties are not indexable.  

## Prerequisites

1. Set up the application on BambooHR developer portal.
2. Configure a BambooHR app with a unique App name 
 ![Screenshot of Add application.](media/bamboohr-connector/bamboohr-addapp.png)
3. Add direct URLs** into the "Redirect URLs" field in the app details section.
   For M365 Enterprise, copy and paste: https://gcs.office.com/v1.0/admin/oauth/callback 

 ![Screenshot of App Details.](media/bamboohr-connector/bamboohr-appdetails.png)
 ![Screenshot of Direct Urls form.](media/bamboohr-connector/bamboohr-redirecturis.png)
4. Add application ccopes  

On the Application Scopes section, select the following scopes with read access only:  

Claims: 

            email, 

            openid, 

Employee: 

            employee, 

            employee:contact, 

            employee:identification, 

            employee:job, 

            employee:management, 

            employee:name, 

            employee_directory, 

Miscellaneous: 

            app, 

            field, 

            offline_access, 

            public.user, 

            user, 

            user:management, 

Reports: 

            report  

 ![Screenshot of Select Scopes.](media/bamboohr-connector/bamboohr-selectscopes.png)
 ![Screenshot of Scope Selection.](media/bamboohr-connector/bamboohr-scopeselection.png)

**5. Get App Client ID and App Secret**

Navigate to the app credentials section to get the App client ID and App client secret.   
 ![Screenshot of Client Id and Client Secret Section.](media/bamboohr-connector/bamboohr-clientidandsecret.png)


## Get started

[Add BambooHR Copilot connector.](https://admin.microsoft.com/adminportal/home?#/MicrosoftSearch/Connectors/add)

### 1. Choose a display name

Choose a display name e.g., BambooHR Profiles, that helps users easily recognize associated profiles in a Copilot response.

### 2. Add the instance URL

Enter your BambooHR instance URL e.g., https://contoso.bamboohr.com/ 

### 3. Choose authentication type

Select OAuth 2.0 from the list of authentication types, and enter the client ID and client secret from BambooHR App portal.

<br>
For other settings like Access permissions, Schema, and Crawl frequency, we have set defaults based on what works best with BambooHR people data. The default values are: 


| Users ||
| :--- | :--- |
| Access permissions | Data is visible to everyone. |
| Map identities | Data source identities mapped using Microsoft Entra IDs. |

<br>

| Source Property | Description | [Property in Microsoft 365 User Profile Schema](https://learn.microsoft.com/en-us/graph/api/resources/profile?view=graph-rest-beta) |
| :--- | :--- | :--- |
| First Name | Employee's First Name | names->first |
| Last Name | Employee's Last Name | names->last |
| Name | Employee's Full Names | names->displayName |
| Email | Employee's Work Email Address | emails->address[type='work']<br><br>*Note: Email is converted to the Microsoft Entra objectId of the end user and is used for internal processing.* |
| Birth Date | Employee's Date of Birth | anniversaries->date[type='birthday'] |
| Job Information Department | Employee's Job Department e.g., Human Resources | positions->detail->company->department |
| Job Information Division | Employee's Job Division e.g., North America | position->detail->company->division |
| Employee Number | Employee's Number | position->detail->employeeId |
| Employee Eeid | Employee's ID in BambooHR | webAccounts->userId<br><br>*Note: The employee's eeid is also utilized internally to periodically check for any updates for a given Employee in BambooHR.* |
| Employment Status | Employee's Status e.g., Full-Time, Contractor Etc. | position->detail->employeeType |
| Original Hire Date Time | Employee's data of hire | anniversaries->date[type='originalHireDate'] |
| Job Information Job Title | Employee's Job Title e.g., Senior HR Administrator | positions->detail->jobTitle |
| Supervisor Id | Employee's Manager Identifier | positions->manager->userId<br><br>*Note: The supervisor ID is used to find the supervisor's email, which is then converted to the Microsoft Entra objectId of the manager for internal processing.* |
| Mobile Phone | Employee's Mobile Phone | phones->number(type=mobile) |
| Work Phone | Employee's Work Phone | phones->number(type=work) |
| Job Information Location | Employee's Office Location | positions->positionDetail->companyDetail->officeLocation |
| Status | Employee's Status e.g., Active or Inactive | N/A<br><br>*Note: Internal use for filtering inactive employees, ensuring they are excluded from BambooHR data retrieval.* |

<br> 


| Sync ||
| :--- | :--- |
| Incremental Crawl | Frequency: Every 15 minutes. |
| Full Crawl | Frequency: Every day. |


## Custom setup

Custom setup is for admins who want to edit the default values for settings. When you choose Custom setup, you see the other three tabs: Users, Content, and Sync.

**Users**

The BambooHR Copilot connector only supports data visible to Everyone. This means indexed data appears in the search results for all users.
The BambooHR Copilot connector only supports mapping your data source identities with Microsoft Entra ID by checking whether the email address of BambooHR profiles is the same as UserPrincipalName (UPN), or Mail of users in Microsoft Entra ID. 


**Content**

The BambooHR Copilot connector does not support the addition of new properties or the removal of existing properties on this tab. Within this tab, there is a property named AnnotationSerialized that encompasses all the default properties previously mentioned.


**Sync**

The refresh interval determines how often your data is synced between the data source and the people connector index. There are two types of refresh intervals – full crawl and incremental crawl. For more information, see [refresh settings](https://learn.microsoft.com/en-us/microsoftsearch/configure-connector#guidelines-for-sync-settings).


## Troubleshooting

**1. Invalid Credentials. Verify the credential information from BambooHR App**

Ensure that the scopes are correctly configured in the BambooHR App, and verify that the client ID and secret entered match those in the BambooHR App. 

## Next steps

After you publish your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
