--- 

title: "Zendesk TicketMicrosoft 365 Copilot connector (preview)" 
ms.author: anggao
author: ms-anggao
manager: jecui
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the Zendesk Ticket Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 02/27/2025
---

# Zendesk Ticket Microsoft 365 Copilot connector (preview)

The Zendesk Ticket Microsoft 365 Copilot connector allows your organization to index tickets from Zendesk. After you configure the connector, users can search for these tickets from Zendesk in Microsoft 365 Copilot and from any Microsoft Search client.

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Zendesk Ticket Copilot connector.

>[!NOTE]
>The Zendesk Ticket Copilot connector is in public preview. To get access to the connector, enable the [Targeted Release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- Index Ticket tickets.
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- Doesn't index attachments.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **Zendesk Instance URL**: To connect to your Zendesk Ticket data, you need your organization's Zendesk instance URL, which is typically the following: `https://<your-organization-domain>.zendesk.com`. If you don't have an instance already, for information about how to create a test instance, see [How do I create a Support trial account?](https://support.zendesk.com/hc/en-us/articles/4408823799962-How-do-I-create-a-Support-trial-account).
- **Service Account**: To connect to Zendesk Ticket and allow the Zendesk Ticket Copilot connector to update knowledge tickets regularly, you need a service account with read permissions granted to the service account. The service account must have either the Admin, Agent, or Light agent role. The Contributor role does not provide read permissions in Zendesk.

## Get Started

### 1. Display name

The display name identifies each citation in Copilot to help users recognize the associated file or item. The display name also signifies trusted content and is used as a [content source filter](/MicrosoftSearch/custom-filters#Content-source-filters). A default value is provided for this field; you can customize it to a name that users in your organization recognize.

### 2. Zendesk URL

To connect to your Zendesk data, you need your organization's Zendesk instance URL. Your organization's Zendesk instance URL is typically  `https://<your-organization-domain>.zendesk.com`.

### 3. Authentication type

#### Zendesk OAuth

Use the following steps to use Zendesk OAuth for authentication.

A Zendesk admin needs to create an OAuth client in the [Zendesk Admin Center](https://support.zendesk.com/hc/en-us/articles/4581766374554-Using-Zendesk-Admin-Center#topic_hfg_dyz_1hb). For more information, see [Managing access to the Zendesk API](https://support.zendesk.com/hc/articles/4408889192858-Managing-access-to-the-Zendesk-API#topic_mmh_gm1_2yb) in the Zendesk documentation.

Use the information in the following table to fill out the OAuth client creation form.

Field | Description | Recommended Value
--- | --- | ---
Client name | Unique value that identifies the application that you require OAuth access for. | Microsoft Search
Description | (Optional) A short description of the OAuth client. | Use an appropriate description
Company | The name of your company. | Use an appropriate value
Logo | A file that contains the image for the application logo. | Any appropriate logo or use default.
Client kind | Choose between Confidential and Public Oauth client. | Confidential
Redirect URL | A required callback URL that the authorization server redirects to. | For **Microsoft 365 Enterprise**: https://<span>gcs.office.</span>com/v1.0/admin/oauth/callback</br></br>For **Microsoft 365 Government**: https://<span>gcsgcc.office.<span>com/v1.0/admin/oauth/callback|

Enter the client ID (unique identifier) and secret to connect to your instance. After you connect, use a Zendesk account credential to authenticate permission to crawl.

### 4. Roll out to limited audience

Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before you expand the rollout to a broader audience. For more information, see [Staged rollout for Zendesk Ticket Copilot connectors](staged-rollout-for-graph-connectors.md).

Now you're ready to create the connection for Zendesk Ticket. Choose **Create** to publish your connection and index tickets from your Zendesk account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, default values are provided based on what works best with Zendesk data.

| Users | Description |
|----|---|
| Access permissions | Only people with access to content in Data source. |
| Map identities | Data source identities mapped using Microsoft Entra IDs. |

| Content | Description |
|---|---|
| Manage properties | To check default properties and their schema. |

| Sync | Description |
|---|---|
| Incremental crawl | Frequency: Every 15 mins |
| Full crawl | Frequency: Every day |

If you want to edit any of these values, choose **Custom Setup**.

## Custom setup

Custom setup is for admins who want to edit the default values for any settings. When you choose **Custom Setup**, you see three more tabs - **Users**, **Content**, and **Sync**.

### Users

#### Access permissions

The Zendesk Ticket Copilot connector supports **Everyone** or **Only people with access to this data source** search permissions. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

#### Mapping identities

The default method for mapping your data source identities with Microsoft Entra ID is to verify that the email ID of Zendesk users is the same as the user principal name (UPN) or email address of the users in Microsoft Entra. If the default mapping don't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose the **Microsoft Entra ID** option if the Zendesk users' email ID is the **same** as the UPN or email in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Zendesk users' email ID is **different** from the UPN and email in Microsoft Entra ID.

### Content

#### Manage properties

You can add or remove available properties from your Zendesk Ticket, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists the properties that are selected by default.

|Source property|Label|Description|Schema|
|---|---|---|---|
| AssigneeEmail |  |  | Query, Retrieve, Search |
| Brand |  |  | Query, Retrieve, Search |
| Collaborators |  |  | Query, Retrieve, Search |
| CreateDate | Created date time |Date and time that the item was created in the data source | Query, Refine, Retrieve |
| Description |  |  | Search |
| DueDate |  |  | Query, Refine, Retrieve |
| EmailCcs |  |  | Query, Retrieve, Search |
| ExternalId |  |  | Query, Retrieve |
| Followers |  |  | Query, Retrieve, Search |
| Group |  |  | Query, Retrieve, Search |
| Id |  |  | Query, Retrieve |
| Organization |  |  | Query, Retrieve, Search |
| Priority |  |  | Query, Retrieve, Search |
| ProblemId |  |  | Query, Retrieve |
| Recipient |  |  | Query, Retrieve, Search |
| Requester |  |  | Retrieve, Search |
| Status |  |  | Query, Retrieve, Search |
| Subject | Title |  The title of the item that you want shown in Copilot and other search experiences | Query, Retrieve, Search |
| Submitter |  |  | Query, Retrieve, Search |
| Tags |  |  | Query, Retrieve, Search |
| Type |  |  | Query, Retrieve, Search |
| UpdateDate | Last modified date time | Date and time the item was last modified in the data source. | Query, Refine, Retrieve |
| Url | url | The target URL of the item in the data source | Query, Retrieve, Search |
| ViaChannel |  |  | Query, Retrieve, Search |
| ViaSourceFromAddress |  |  | Query, Retrieve, Search |
| ViaSourceFromName |  |  | Query, Retrieve, Search |
| ViaSourceToAddress |  |  | Query, Retrieve, Search |
| ViaSourceToName |  |  | Query, Retrieve, Search |

#### Preview data

Use the preview results button to verify the sample values of the selected properties and query filter.

### Sync

The refresh interval determines how often your data is synced between the data source and the Zendesk Ticket Copilot connector index. There are two types of refresh intervals: full crawl and incremental crawl. For more information, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval.

## Next steps

After you publish your connection, you can review the status under **Data Sources** in the [admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

For help and support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
