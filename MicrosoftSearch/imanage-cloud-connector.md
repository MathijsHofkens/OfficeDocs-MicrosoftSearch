--- 

title: "iManage Cloud Microsoft Graph connector (preview)" 
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
description: "Set up the iManage Cloud Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 04/02/2025
---

# iManage Cloud Microsoft Graph connector (preview)

The iManage Cloud Microsoft Graph connector allows your organization to index content from iManage Cloud. After you configure the connector, end users can search for this content from iManage Cloud in Microsoft Copilot and from any Microsoft Search client.
 
This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors an iManage Cloud Microsoft Graph connector.

>[!NOTE]
>The iManage Cloud Microsoft Graph connector is in private preview for invited customers only. If you are invited and wish to get access to try it, you need to enable [Targeted release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- Index documents and emails from iManage Cloud while maintaining access control.
- Use content filters to selectively index content based on criteria such as time range filter and library filter.
- Exclude content designated as HIPAA compliant from the index to ensure that sensitive information is automatically excluded by default.
- Use [Semantic search](semantic-index-for-copilot.md) in Copilot to enable users to find relevant content.

## Limitations
- Support the iManage multi-tenant Cloud, also known as iManage Work at cloudimanage.com, as this connector is exclusively compatible with it.
- Exclude iManage Work on-premises or iManage single-tenant Cloud hosted in iManage Cloud at imanage.work and other domains, as they aren't supported at this time.
- Exclude iManage content marked as requiring HIPAA compliance from indexing.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- Get your organization's iManage Cloud instance URL, typically found at[https://cloudimanage.com](https://cloudimanage.com/).
- Use an iManage account with NRTADMIN permissions to complete OAuth 2.0 Authentication in Microsoft Admin Center.
- Obtain the OAuth Client_ID and Client_Secret from iManage support before configuring the iManage Cloud connection in Microsoft Admin Center.
- Add and authorize the Microsoft iManage Cloud application within the iManage Cloud Control Center.

### 1. Configure the display name 
A display name is used to identify each reference in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content.

### 2. Add the iManage Cloud instance URL
The iManage Cloud instance URL is essential to correctly access and update data from, which is typically: [https://cloudimanage.com](https://cloudimanage.com/).

### 3. Provide authentication details

#### iManage Cloud OAuth 2.0

We support OAuth 2.0 authentication for iManage Cloud. This connector is registered as an iManage Per-Customer Universal Application titled **Microsoft - iManage Cloud Microsoft Graph connector**, which you can find on the iManage Cloud application page. To enable this application for your organization, follow these steps.

1. Contact Microsoft to enable iManage Cloud Microsoft Graph connector for your organization.<br>

   The iManage Cloud Microsoft Graph connector is registered as an iManage Per-Customer Universal Application. You need to contact your Microsoft account representative to enable this application for your organization during the application preview phase. Please send an email using the template below once aligned with your Microsoft account representative. Microsoft will work with the iManage support team to register this application for your organization and share the OAuth 2.0 Client Secret to set up the iManage Cloud Microsoft Graph connector for your organization.
   
   The email template for application registration is:<br>

   To: iManageGCAppRegistra@microsoft.com<br>

   Subject: New cloudimanage.com  {{ApplicationName}}  application for CustomerName<br>

   Body: Please create a new application for iManage Cloud Microsoft Graph connector per-customer universal app.<br>

   CustomerName (Required): ____<br>
   Customer/Tenant ID (Required): _____<br>
   Microsoft Account representative (Optional): _____<br>

2. Add Microsoft iManage Cloud Microsoft Graph connector application.<br>

   A new application registered and authorized for your iManage Cloud environment isn't enabled by default. This application needs to be enabled in iManage Control Center by a user assigned to a Global Management role that has the App Management privilege. You need to add the **Microsoft - iManage Cloud Graph Connector** in iManage Control Center for your environment with the recommended values below.  [Learn more](https://docs.imanage.com/cloud/cc-help/en-US/Adding_an_application.html).

   |Area  |  Field | Recommended value|
   |:--- |:--- |:---|
   |Status | Status | Enabled|
   |Authentication | Allow Refresh Token | Yes|
   |Authentication | Refresh Token Expiry | 365 days|
   |Authentication | Access Token Expiry | 5,000 mins|
   |Security | Allow access to | All Users|

3. Authorize the OAuth Client<br>

   Enter the Client ID and Client Secret to authorize the client application to connect to your instance. Use an iManage NRTADMIN account credential to authorize the application in the browser popup window.

### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, see [Staged rollout for Microsoft Graph connectors](staged-rollout-for-graph-connectors.md).

To create the connection for iManage Cloud, click **create** to publish your connection and index content from your iManage account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, we have default values based on what works best with iManage data.

| Users | Description |
|:----|:---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Select the libraries | All |
| Select Time range | _Last half a year_ |
| Manage Properties | _29 default content properties_ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |


## Custom setup

In custom setup you can edit any of the default values for users, content, and sync.

### Users

#### Access permissions

The iManage Cloud Microsoft Graph connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

#### Mapping identities

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of iManage users is the same as the UserPrincipalName (UPN), or Mail of the users in Microsoft Entra. If you believe the default mapping wouldn't work for your organization, you can provide a custom mapping formula. To learn more about mapping Non-Microsoft Entra ID identities, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose **Microsoft Entra ID**, if the Email ID of iManage users is the **same** as the UserPrincipalName (UPN) or email of users in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Email ID of iManage users is **different** from the UserPrincipalName (UPN) and Email of users in Microsoft Entra ID.

### Content

1. To optimize the indexing process, consider setting up multiple connections or utilizing content filters to reduce the number of items indexed per connection if the content exceeds the [connection limits](/graph/connecting-external-content-api-limits).

2. Choose the specific libraries for the content to be indexed. Only the content within these selected libraries is indexed.

3. Define a time range for the content to be indexed. Only content with a last modified date and time within the specified range is to be indexed. Select an appropriate time range based on the volume of content to be indexed. 

   >[!CAUTION]
   > Selecting "All time" may significantly impact your platform's performance if there's a large volume of content to be indexed.

   >[!TIP]
   > If you have a substantial amount of content stored in your iManage libraries that needs to be indexed with this connector, we strongly recommend creating multiple connections. Each connection should cover only a small portion of the content stored in the iManage Cloud, with different full crawl starting times. This approach helps balance content freshness and performance. For example, each connection should index content less than 1-5 million items and have a full crawl starting time different from other connections.


4. Manage properties <br>

   To view available properties from your iManage Cloud, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias in the property. Some properties are selected by default.

   |Default property|Label|Description|Schema|
   |:---|:---|:---|:---|
   | Author             | Created by              | The person who created the content | Retrieve, Search.       |
   | CC                 |                         | Carbon copy recipients  | Query, Retrieve.        |
   | CoAuthors          |                         | Other authors of the content. |                        |
   | Authors            |                         | The main authors of the content | Retrieve, Search.       |
   | Comment            |                         | Comments associated with the content | Retrieve, Search.      |
   | Content            |                         | The main body of the content | Search.                |
   | ConversationName   |                         | The name of the conversation | Retrieve, Search.      |
   | CreateDate         | Created date time       | The date and time when the content was created | Query, Retrieve.        |
   | CustomProperties   |                         | Custom properties associated with the content | Query, Retrieve.        |
   | DocumentNumber     |                         | The document number     | Query, Retrieve.        |
   | EditDate           | Last modified date time | The date and time when the content was last modified | Query, Retrieve.        |
   | Extension          | File extension          | The file extension       | Query, Retrieve.        |
   | FileCreateDate     |                         | The date and time when the file was created | Query, Retrieve.        |
   | FileEditDate       |                         | The date and time when the file was last edited | Query, Retrieve.        |
   | From               |                         | The sender of the content | Retrieve, Search.       |
   | HasAttachment      |                         | Indicates if the content has an attachment | Retrieve.               |
   | ID                |                         | The unique identifier of the content | Query, Retrieve.        |
   | LastUser           | Last modified by        | The last user who modified the content | Query, Retrieve, Search.|
   | Library            |                         | The library where the content is stored | Query, Retrieve.        |
   | Name               | File name               | The name of the file    | Retrieve, Search.       |
   | ReceivedDate       |                         | The date and time when the content was received | Query, Retrieve.        |
   | RelatedDocuments   |                         | Documents related to the content | Retrieve, Search       |
   | SentDate           |                         | The date and time when the content was sent | Query, Retrieve.        |
   | Subject            |                         | The subject of the content | Retrieve, Search.       |
   | Title              | Title                   | The title of the content | Retrieve, Search.       |
   | To                 |                         | The recipients of the content | Retrieve, Search.       |
   | Url                | url                     | The URL of the content  | Retrieve, Search.       |
   | Version            |                         | The version of the content | Query, Retrieve.        |
   | WSType             |                         | The workspace type      | Query, Retrieve.       |
   | WorkspaceName      |                         | The name of the workspace | Query, Retrieve.        |

### Sync

The refresh interval determines how often your data is synced between the data source and the iManage Cloud Microsoft Graph connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more information, see [Refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

### Connection description
Upon creating the connection, navigate to the success page. Click **Auto suggestion** to use the default connection description. Alternatively, you may create a custom connection description to help Copilot better understand the indexed content and enhance the end user prompts when referencing content from this connection for your organization.

## Troubleshooting
After publishing your connection, you can review the status under **Data sources** in the [admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
