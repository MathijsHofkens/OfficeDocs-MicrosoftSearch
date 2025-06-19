--- 

title: "Smartsheet Sheet Microsoft 365 Copilot connector (preview)" 
ms.author: depang
author: dennypanggh
manager: jecui
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the Smartsheet Sheet Microsoft 365 Copilot connector." 
ms.date: 03/13/2025
---

# Smartsheet Sheet Microsoft 365 Copilot connector (preview)

The Smartsheet Sheet Microsoft 365 Copilot connector allows your organization to index sheet content from Smartsheet. After you configure the connector, end users can search for this content from Smartsheet in Microsoft Copilot and from any Microsoft Search client.
 
This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Smartsheet Sheet Copilot connector.

>[!NOTE]
>The Smartsheet Sheet Copilot connector is in public preview. If you wish to get access to try it, you need to enable [Targeted Release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- Index Smartsheet Sheet content from Smartsheet Pro and Business edition.
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- Only content from the Smartsheet Sheet Pro and Business editions will be indexed.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **Smartsheet Sheet instance region**: To connect to your Smartsheet Sheet data, you will need to choose the region for your organization's Smartsheet instance. Use one of the following Smartsheet instance regions: “Default” (`https://api.smartsheet.com`) or “Europe”(`https://api.smartsheet.eu`).
- **Smartsheet Sheet account**: To connect to Smartsheet Sheet and allow the Copilot to update Smartsheet sheet content and metadata regularly, you need Smartsheet Sheet Access Tokens of System Admin Users to access published content and metadata.

## Get Started

### 1. Display name 
Choose a display name that helps users easily recognize the associated file or item in a Copilot response.

### 2. Smartsheet Sheet instance region
The Smartsheet Sheet region is essential to correctly access and update data from. Use one of the following regional domain URLs: `https://api.smartsheet.com` (Non-Europe) or `https://api.smartsheet.eu` (Europe).

### 3. Authentication Type

**Smartsheet Basic Authentication**

We support the Smartsheet API access token authentication for Smartsheet Sheet, make sure the access token is created by a System Admin user account.

API Access token owner email address: the API access token owner's email address.

API Token: The API Token value generated from Smartsheet Personal Settings -> API Access page. To learn more, see [Generate an API key](https://aka.ms/gc_smartsheet_APItoken) in the Smartsheet documentation.
   
### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, [click here](staged-rollout-for-graph-connectors.md).

At this point, you're ready to create the connection for Smartsheet Sheet. You can click on the "Create" button to publish your connection and index content from your Smartsheet account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, we have default values based on what works best with Smartsheet data.


| Users | Description |
|----|---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Manage Properties | _To check default properties and their schema._ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |

If you want to edit any of these values, you need to choose the "Custom Setup" option.

## Custom setup

Custom setup is for those admins who want to edit the default values for settings listed in the above table. Once you click on the **Custom Setup** option, you see three more tabs - **Users**, **Content**, and **Sync**.

### Users

**Access permissions**

The Smartsheet Sheet Copilot connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

**Mapping identities**

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of Smartsheet users is the same as the UserPrincipalName (UPN), or Mail of the users in Microsoft Entra. If you believe the default mapping wouldn't work for your organization, you can provide a custom mapping formula. To learn more about mapping Non-Microsoft Entra ID identities, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose the **Microsoft Entra ID** option if the Email ID of Smartsheet users is the **same** as the UserPrincipalName (UPN) or email of users in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Email ID of Smartsheet users is **different** from the UserPrincipalName (UPN) and Email of users in Microsoft Entra ID.

### Content

**Content filter**

**Select time range**: Select a time range for the content to be indexed. Only content with a Last modified date time within the selected range will be indexed. Choose an appropriate time range based on the volume of content to be indexed. Selecting "All time" may significantly impact your platform's performance if there is a large volume of content to be indexed.

**Manage properties**

Here, you can view available properties from your Smartsheet Sheet, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below.

|Source property|Label|Description|Schema|
|---|---|---|---|
| Content  |  |  | Search   |
| CreatedAt  | Created date time | Data and time that the item was created in the data source. | Query, Retrieve   |
| CreatedBy  | Created by | Name of the person who created the item in the data source. | Query, Retrieve, Search |
| HasAttachment  |  |  | Query, Retrieve |
| Id   |  |  | Query, Retrieve  |
| ModifiedAt   | Last modified date time | Date and time the item was last modified in the data source. | Query, Retrieve   |
| Name   | File name |   | Query, Retrieve, Search |
| SheetPermaLink   | URL | The target URL of the item in the data source. | Query, Retrieve, Search |
| Title  | Title | The title of the item that you want to be shown in Copilot and other search experiences. | Query, Retrieve, Search |
| WorkspaceName  |  |  | Query, Retrieve, Search |


### Sync

The refresh interval determines how often your data is synced between the data source and the Smartsheet Sheet Copilot connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more details, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

## Troubleshooting
After publishing your connection, you can review the status under the **Data Sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

For more information about index browser search, see [How to get Smartsheet | Smartsheet Learning Center](https://help.smartsheet.com/articles/2482711-get-smartsheet-ids). 

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
