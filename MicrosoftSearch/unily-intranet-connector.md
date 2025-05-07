--- 
title: "Unily Connector for Microsoft Search and Copilot" 
ms.author: rerabo
author: vivg
manager: ereza
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the Unily Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 03/19/2025
---

# Unily Microsoft Graph connector (Preview)

The Unily Graph connector allows your organization to index content from Unily intranet. After you configure the connector, end users can search for this content in Microsoft Copilot and from any Microsoft Search client. 

This documentation is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Unily Graph connector.

## Capabilities
- Index Unily content (the following document types are supported: App, Doc Brand Asset, Image Brand Asset, FAQ, Form, Quiz, Idea, Location, Mandatory Read Article, Mandatory Read Doc, Media Content, Story, Knowledge Article).
- Enable users within the company to ask questions in natural language using Copilot and receive answers based on content from Unily. Examples:
   - What are the company holidays for 2025?
   - What events are planned for national heritage month?
   - What training programs are available?
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- The connector doesn't index restricted content (supporting only content that doesn't have "Manage Read Access").
- Currently, Copilot responses aren't customized for specific audiences as defined in Unily, such as utilizing the 'target audience' property.
- The connector doesn't support ACLs (access control lists). All the data indexed using the Unily Knowledge connector is visible to all Microsoft 365 users in your tenant, accessible through Microsoft Copilot or Search.

## Prerequisites
- To create a new connection, you must be the search admin for your organization's Microsoft 365 tenant.
- To create a new connection, use your organization’s Unily instance URL. This URL is the specific web address used to access and interact with Unily API services for content retrieval, which usually looks like https://[your-organization-name].unily.com
- To complete the authentication, you need a Client ID and Client Secret. To get your Unily Client ID and Secret, contact Unily directly. A Unily instance may have multiple applications, each with different permissions. Ensure that you obtain the correct credentials for the application to be used for the Graph connector.


## Get Started

### 1. Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated item. The display name also signifies trusted content. Display name is also used as a content source filter. A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Unily URL
Use your organization’s Unily URL. This URL is the specific web address used to access Unily, which typically looks like https://[your-organization-name].unily.com

### 3. Authentication Type
For Unily Knowledge graph connector, use OAuth 2.0 for authentication.

To authenticate, enter the Client ID and Client Secret. The Client ID is a unique identifier assigned to your application for making requests to the Unily API. The Client Secret is a confidential key used alongside the Client ID to securely authenticate your application with the Unily API.
 
### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, see [staged rollout](staged-rollout-for-graph-connectors.md).

At this point, you're ready to create the connection for Unily. You can click on the "Create" button to publish your connection and index posts from your Unily account.

## Custom Setup

Custom setup is for admins who want to edit the default values for settings. Once you click on the 'Custom Setup' option, you see three other tabs: Users, Content, and Sync.

### Users

**Access Permissions**

All the data indexed using the Unily connector is visible to all Microsoft 365 users in your tenant, accessible through Microsoft Copilot or Search.
The Unily connector is currently in preview. Once it becomes generally available, Access Control Lists (ACLs) will be valid. This capability ensures that all user permissions and group access available in Unily are supported through the connector in Microsoft apps like Copilot and Search.

 
### Content

**Manage properties**

Here, you can add or remove available properties from your Unily data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below:

**Source Property** | **Semantic Label** |**Description**| **Schema**
--- | ---- | --- | ---
Authors | Authors | Names of the content authors | Query, Retrieve, Search
Content | | The main body of the content, including all written information and details | Search
CreatedBy | The email address of the individual who initially created the entity | Query, Retrieve, Search
CreatedDate | Created date time | The specific date when the content was originally created | Retrieve
Date | | The date when the content was first made available to the public |
Description | | A concise summary that provides an overview of the main points and purpose of the content | Retrieve, Search
DocumentType | | The type of the document within the Unily platform | Query, Retrieve
ID | | Post title | Query, Retrieve
LastModifiedDate | Last modified date time | The most recent date when the content was modified or updated | Retrieve
ParentId | | Post title | Retrieve
Title | Title | The heading or title that appears on the content page | Query, Retrieve, Search
UniqueId | | Post title | Query, Retrieve
Url | url | The link that directs to the specific page in Unily where the content is located | Retrieve

### Sync

The refresh interval determines how often your data is synced between the data source and the Graph connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more information, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

## Troubleshooting
After publishing your connection, you can review the status under the **Data Sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md). 

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
