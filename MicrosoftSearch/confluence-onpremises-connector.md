---
ms.date: 11/28/2024
title: "Confluence On-premises Microsoft 365 Copilot connector (preview)"
ms.author: mansipakhale
author: Mansipakhale10
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: install-set-up-deploy
ms.service: mssearch
ms.localizationpriority: high
search.appverid:
- BFB160
- MET150
- MOE150
description: "Set up the Confluence On-premises Microsoft 365 Copilot connector"
---

# Confluence On-premises Microsoft 365 Copilot connector

The Confluence On-premises Microsoft 365 Copilot connector allows your organization to index Confluence server or data center content. After you configure the connector and index data from the Confluence site, end users can search for that content in Microsoft Search and Microsoft 365 Copilot.

This article is intended for Microsoft 365 administrators who are responsible for configuring, running, and monitoring the Confluence On-premises Copilot connector. It supplements the general instructions provided for setting up Microsoft Copilot connectors in the Microsoft 365 admin center.

## Capabilities
- Ask natural language questions about Wiki content in Copilot, such as summarizing the architecture document and how to get access to a portal, with enhanced search capabilities.
- Perform natural language queries for accurate responses using Semantic Search support.
- Support Confluence versions above 8.0 for compatibility.

## Limitations
- Doesn't index blogs, attachment files, or comments.
- Only indexes current pages; archived pages are excluded.
- CQL (Confluence Query Language) isn't supported for Confluence on-premises; however, we support a space and page-level filter.

## Prerequisites
1. **Install the GCA [Graph Connector Agent]**: Ensure that the GCA is installed on a Windows machine within the same network as the data source, accessible via the Confluence URL. You can find more information [Graph Connector Agent](./graph-connector-agent.md)
2. **Install plugin**: Download and install the Confluence on-prem plugin from the Atlassian marketplace on your Confluence setup. Get the plugin from [Confluence On-prem Plugin for Copilot connectors | Atlassian Marketplace](https://marketplace.atlassian.com/apps/1234846?tab=reviews&hosting=datacenter).
3. **Validate plugin**: Navigate to **Administration** > **Manage apps** and set app type filter to **System**, verify that **Confluence Mobile Web Plugin** is installed and enabled. This plugin is installed and enabled by default.
  * If the plugin is not installed, get the plugin from [Mobile Plugin for Confluence Data Center](https://marketplace.atlassian.com/apps/1218250/mobile-plugin-for-confluence-data-center?hosting=server&tab=overview) and install it.
  * If the plugin is installed but disabled, enable it.
4. **Authentication**: Ensure that you have authentication credentials with the right access. 

>[!IMPORTANT]
> **Recommended: The Confluence Global Administrator should create the connection** </br>
> **Who is the Confluence global administrator?**
 > A Confluence Administrator is a user who has full administrative permissions. </br>
 > * To check permissions: Go to **Administration** > **General Configuration** > **Global Permissions** </br>
 > * Look for the group **Confluence-administrators**, which has all permissions enabled, including - Can Use, Personal Space, Create Space, Confluence Administrator, and System Administrator.
 > * Any user creating a token must be a member of this group.

## Get started

### 1. Display name

A Display name is used to identify each reference in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. Display name is also used as a [content source filter](./custom-filters.md#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Confluence on-premises URL

To connect to your Confluence On-premises data, you need your organization's Confluence instance URL. Your organization's Confluence instance URL typically looks like 'https://contoso.atlassian.net'.

### 3. Graph connector Agent (GCA)

To index your Confluence server or data center content, you must install and register the connector agent. See [Install the Graph Connector Agent](./graph-connector-agent.md) for details. You must be the administrator for your organization's Microsoft 365 tenant and the administrator for your organization's Confluence site.

>[!NOTE]
> GCA can be installed on a different Windows machine and need not be on the same machine as the On-premises server. The machine can help generate an App ID and secret, which can be used for the setup. You must ensure that the GCA machine is on during the crawling. 
> You may find answers to common GCA-related questions in [FAQ section](./frequently-asked-questions.md).

### 4. Install the Confluence on-premises plugin

Verify that the Copilot connectors Confluence On-prem Plugin is installed. You don't need to install the plugin for each Confluence Copilot connector; if it's already installed in your Confluence instance, you can skip this step for subsequent Confluence on-prem connections.

   - Download the app from [Copilot connectors Confluence On-prem plugin | Atlassian Marketplace](https://marketplace.atlassian.com/apps/1234846?tab=overview&hosting=datacenter).
   - Log in to your Confluence system.
   - Go to **Settings** > **Manage apps**.
[![Screnshot that shows clicking on settings icon -> clicking on manage apps.](https://github.com/user-attachments/assets/16a6a8f0-844e-49bd-9939-694d8741eaea)](https://github.com/user-attachments/assets/16a6a8f0-844e-49bd-9939-694d8741eaea#lightbox)
   - Click **upload app**.
[![Screnshot that shows clicking on upload app](https://github.com/user-attachments/assets/e1216fef-7c35-4e87-a1ad-4aef7062fd1a)](https://github.com/user-attachments/assets/e1216fef-7c35-4e87-a1ad-4aef7062fd1a#lightbox)
   - Choose the downloaded file and proceed.
[![Screnshot that shows Plugin sussuesfully installed)](https://github.com/user-attachments/assets/58ba9e9e-e2c9-47e9-967d-401cd79a7c5d)](https://github.com/user-attachments/assets/58ba9e9e-e2c9-47e9-967d-401cd79a7c5d#lightbox)

>[!NOTE]
>Plugin is supported for Confluence version above 8.0.

### 5. Authentication type

To authenticate and synchronize content from Confluence On-prem, choose **one of three** supported methods:<br>

   **a. Basic authentication** <br>
   To authenticate to your instance, enter the username and password of your Confluence account. <br>

   **b. OAuth1.0a** <br>
   Generate a public/private key pair and create an application link in the Confluence On-premises site so that the connector agent can access the instance. For more information, see [step 1 in Atlassian developer documentation](https://developer.atlassian.com/server/jira/platform/oauth/#step-1--configure-jira).<br>
 
   **c. OAuth 2.0 (recommended)** <br> 
   The following steps provide guidance on how to register the app [Configure an incoming link](https://confluence.atlassian.com/doc/configure-an-incoming-link-1115674733.html). 

  1. Go to **Administration** > **General configuration** > **Application links**. 
  2. Select **Create link**.
  3. Select **External application**, and then choose **Incoming** as the direction.
  4. Select **Admin** as the scope.
  5. Fill in the redirect URL: `https://gcs.office.com/v1.0/admin/oauth/callback`.

### 6. Rollout to limited audience

Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](./staged-rollout-for-graph-connectors.md).

At this point, you are ready to create the connection for Confluence. You can click on the "Create" button and the Microsoft Graph connector starts indexing page from your Confluence account.

For other settings, like access permissions, data inclusion rules, schema, and crawl frequency. We set defaults based on what works best with Confluence data. The default values are as follows:

|**Users** |&nbsp;|
|----|---|
|Access permissions|_Only people with access to content in Data source._|
|Map Identities|_Data source identities mapped using Microsoft Entra IDs._|

|**Content**|&nbsp;|
|---|---|
|Include/Exclude space|_All_|
|Manage Properties|_To check default properties and their schema, click here_|

|**Synchronization**|&nbsp;|
|---|---|
|Incremental Crawl|_Frequency: Every 15 mins_|
|Full Crawl|_Frequency: Every Day_|

If you want to edit any of these values, you need to choose the `Custom Setup` option.

## Custom Setup

Custom setup is for those admins who want to edit the default values for settings listed in the default table. Once you click on the **Custom Setup** option, you see three more tabs – Users, Content, and Sync.

### Users

**Access Permissions**

The Confluence On-premises Copilot connector supports search permissions visible to Everyone or Only people with access to this data source. If you choose Everyone, indexed data appears in the search results for all users. If you choose Only people with access to this data source, indexed data appears in the search results for users who have access to it. 
In Confluence On-premises, security permissions for users and groups are defined using space permissions and page restrictions. The permission evaluation follows these rules:
- Retrieve the permission configuration from the page-level restrictions.
- Retrieve the permission configuration from the parent page restrictions.
- Retrieve the permission configuration from the space permissions.
- Compute the intersection of the above three configurations to determine the final effective permission on the page.
This final permission set is then synchronized to Microsoft 365 Copilot


>[!IMPORTANT]
>Anonymous access settings defined at the space level are not considered in this evaluation.


If you choose Only people with access to this data source, you need to further choose whether your Confluence site has Microsoft Entra ID provisioned users or non-AAD users.

To identify which option is suitable for your organization:
1. Choose the **Microsoft Entra ID** option if the email ID of Confluence users is **same** as the UserPrincipalName (UPN) of users in Microsoft Entra ID.
2. Choose the **non-AAD** option if the email ID of Confluence users is **different** from the UserPrincipalName (UPN) of users in Microsoft Entra ID. 

>[!IMPORTANT]
   >
   > * If you choose Microsoft Entra ID as the type of identity source, the connector maps the email IDs of users obtained from Confluence directly to UPN property from Microsoft Entra ID.
   > * If you chose "non-AAD" for the identity type, see [Map your non-Azure AD Identities](map-non-aad.md) for instructions on mapping the identities. You can use this option to provide the mapping regular expression from email ID to UPN.
   > * Updates to users or groups governing access permissions are synced in full crawls only. Incremental crawls do not currently support the processing of updates to permissions.

### Content

**Include or exclude data that you want to index**

In this step, you can add or remove available properties from your Confluence data source. Microsoft 365 selects a few properties.
By default, the connector will index all spaces. However, you can choose to include or exclude specific spaces using the space filter option. 

Enter the list of space keys you wish to include or exclude, and you see a preview of the results. Enter Space key: Each Confluence space has a space key, which is a short, unique identifier that forms part of the URL for that space. To get the space key, contact the Confluence admin. For more information, see: [Space Keys](https://confluence.atlassian.com/doc/space-keys-829076188.html)

**Page filter**

In this step, you can specify the date range for indexing your documents. The parameters are as follows:
- Last Created Date: The date when a document was created. Only documents modified after this date are indexed.
- Last Modified Date: The date when a document was modified. Only documents modified after this date are indexed.

>[!IMPORTANT]
   >
   > * Ensure that the dates are in chronological order. The "Last Created Date" should not be later than the "Last Modified Date."
   > * If no dates are specified, all documents are considered for indexing.

**Manage properties**

Add or remove available properties from your Confluence On-prem data source. Assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable). Additionally, you can change the semantic label and add an alias to the property. Default properties are as follows:

|Source Property|Label|Schema|
|----|----|----|
|Author|authors|Query, Retrieve|
|Content| |Search|
|CreatedByName|Created by|Search, Query, Retrieve|
|CreatedOn|Created date time|Query, Retrieve|
|Id| |Query, Retrieve|
|PageTree| |Retrieve|
|SpaceName| |Search, Query, Retrieve|
|Title|title|Search, Retrieve|
|UpdatedByName|lastModifiedBy|Retrieve|
|UpdatedOn|lastModifiedDateTime|Query, Retrieve, Refine|
|URL|url|Retrieve|

**Preview data**

Go to preview results to view the selected properties and filters.
> [!NOTE]
> The preview only respects space-level filtering.

### Synchronization

The refresh interval determines how often your data is synchronized between the data source and the Copilot connector index. There are two types of refresh intervals – full crawl and incremental crawl. For more details, click [here](configure-connector.md#guidelines-for-sync-settings).
You can change the default values of the refresh interval from here if you want to.

### Review and test your connection

- For testing, you can choose [publish to limited audience](./staged-rollout-for-graph-connectors.md#modify-or-stop-staged-rollout).
- Search and validate your indexed content and permissions using [Index browser](./connectors-index-search.md).
- Find answers to common questions in our [FAQ section](./frequently-asked-questions.md).

For Microsoft Search, if you need to customize the search results page. To learn about customizing search results, see [Customize the search results page](customize-search-page.md).

## Troubleshooting

After publishing your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).
For more information, see [Troubleshooting the Confluence On-premises Copilot connector](troubleshoot-confluence-onpremises-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
