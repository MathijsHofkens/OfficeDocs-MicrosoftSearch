--- 

title: "Seismic Content Microsoft Graph connector" 
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
description: "Set up the Seismic Content Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 03/13/2025
---

# Seismic Content Microsoft Graph connector (preview)

The Seismic Content Microsoft Graph connector allows your organization to index content from Seismic. After you configure the connector, end users can search for this content from Seismic in Microsoft Copilot and any Microsoft Search client.
 
This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Seismic Content Graph connector.

>[!NOTE]
>The Seismic Content Microsoft Graph connector is in public preview. If you wish to get access to try it, you need to enable [Targeted release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- Index Seismic content from Seismic Content Enterprise edition.
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- Only content from the Seismic Content Enterprise edition will be indexed.
- Only content that has been published is indexed. Any content that has not been published in Workspace isn't indexed.
- To connect to Seismic Content and allow the Microsoft Graph connector to update public content and metadata regularly, you need Seismic Content OAuth 2.0 credentials.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- To connect to your Seismic Content data, you need your organization's Seismic Content instance URL, which typically follows this format: https://&lt;your domain&gt;.seismic.com.
- To connect to Seismic Content and allow the Microsoft Graph connector to update public content and metadata regularly, you need Seismic Content OAuth 2.0 credentials to access public content and metadata.

## Get Started

### 1. Choose display name 
A display name is used to identify each reference in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content.

### 2. Add Seismic Content instance URL
The Seismic Content instance URL is essential to correctly access and update data from, which typically follows this format: https://&lt;your domain&gt;.seismic.com.
By the instance URL, the Seismic Content Microsoft Graph connector can reliably synchronize data changes and ensure accurate content delivery from Seismic Content to connected Microsoft 365.

### 3. Provide authentication Type

We support the OAuth 2.0 authentication for Seismic Content. To use the Seismic OAuth for authentication, follow these steps.

A Seismic administrator needs to create an OAuth client in the [Seismic App Registration portal](https://apps.seismic.com/apps). To learn more, see [Login with authorization_code flow](https://developer.seismic.com/seismicsoftware/reference/authorization-code-login) in the Seismic documentation.

The following table provides the mandatory values for OAuth client creation:

|Field | Description | Recommended value|
|:--- |:--- |:--- |
|Authentication Method | The OAuth 2 Authentication Method to authenticate and authorize users securely | OAuth2 - Authorization Code Flow (User Authentication)|
|Redirect URIs (redirect_uri) | The callback URL for the Microsoft Graph connector | `https://gcs.office.com/v1.0/admin/oauth/callback`  |
|Scopes | The scopes to create a new version and a new client ID and secret. | Below scopes are mandatory: seismic.user.view, seismic.configuration.view, seismic.reporting, seismic.library.view |
   
Enter the client ID (Unique identifier) and Secret to connect to your instance. After connecting, use a Seismic administrator account credential to authenticate permission to crawl.

### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, [click here](staged-rollout-for-graph-connectors.md).

To create the connection for Seismic Content, click "Create" to publish your connection and index content from your Seismic account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, we have default values based on what works best with Seismic data.

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

## Custom setup

In custom setup, you can edit any of the default values for users, content, and sync.

### Users

#### Access permissions
Currently, the Seismic Content Microsoft Graph connector only supports permissions visible to **Everyone** due to Seismic API restrictions. All public content indexed using the Seismic Content graph connector will be visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot. 

#### Mapping identities
The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of Seismic users is the same as the UserPrincipalName (UPN), or Mail of the users in Microsoft Entra. If you believe the default mapping wouldn't work for your organization, you can provide a custom mapping formula. To learn more about mapping Non-Microsoft Entra ID identities, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose the **Microsoft Entra ID** option if the Email ID of Seismic users is the **same** as the UserPrincipalName (UPN) or email of users in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Email ID of Seismic users is **different** from the UserPrincipalName (UPN) and Email of users in Microsoft Entra ID.

### Content

#### Content filter
Select a **time range** for the content to be indexed. for the content to be indexed. Only content with a last modified date and time within the selected range will be indexed. Choose an appropriate time range based on the volume of content to be indexed. Selecting **All time** may significantly impact your platform's performance if there is a large volume of content.

Select one or more **Seismic content profiles** to index. All content under the selected profiles is indexed and publicly accessible to everyone within your organization. 


#### Manage properties

To view available properties from your Seismic Content, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. Some properties are indexed by default.

|Default property|Label|Description|Schema|
|---|---|---|---|
| AssignedToProfiles | | | Search |
| Content |  | | Search |
| CreatedAt | Created date time | Data and time that the item was created in the data source. | Query, Refine, Retrieve |
| CreatedBy | Created by | Name of the person who created the item in the data source. | Query, Retrieve, Search |
| Description | | | Query, Retrieve, Search |
| ExpiresAt | | | |
| Format | File extension | | Query, Refine, Retrieve |
| IconUrl | IconUrl | | Query, Retrieve, Search |
| Id | | | |
| ModifiedAt | Last modified date time | Date and time the item was last modified in the data source. | Query, Refine, Retrieve |
| ModifiedBy | Last modified by | Name of the person who most recently edited the item in the data source. | Query, Retrieve, Search |
| Name | Title | The title of the item that you want to be shown in Copilot and other search experiences. | Query, Retrieve, Search |
| Properties | | | Search |
| Repository | | | Query, Retrieve, Search |
| Size | | | |
| Status | | | |
| Type | | | |
| Url | url | The target URL of the item in the data source. | Query, Retrieve, Search |
| Version | | | |

### Sync

The refresh interval determines how often your data is synced between the data source and the Seismic Content Microsoft Graph connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more details, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

## Troubleshooting
After publishing your connection, you can review the status under **Data Sources** in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
