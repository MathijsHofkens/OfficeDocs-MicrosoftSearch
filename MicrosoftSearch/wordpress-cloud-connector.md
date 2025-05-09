--- 
title: "WordPress.com Microsoft 365 Copilot connector (preview)" 
ms.author: rantang
author: ranran1998
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
description: "Set up the WordPress.com Microsoft 365 Copilot connector." 
ms.date: 04/23/2025
---

# WordPress.com Microsoft 365 Copilot connector (preview)

With the WordPress.com Microsoft 365 Copilot connector, your organization can index published posts and pages of your WordPress.com-built websites. After configuring the connector and index content from WordPress.com-built websites, end users can search for those published posts and pages in Microsoft Copilot and any Microsoft Search client. 

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a WordPress.com Copilot connector. 

## Capabilities
- Index published posts and pages of your WordPress.com-built website.    
- Set ingestion filters for published posts by categories. 
- Customize your crawl frequency.  
- Create workflows using this connection and plugins from Microsoft Copilot Studio.  
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content.

## Limitations
- Doesn't index comments. 
- Doesn't crawl user identities and access permissions. All published pages or posts indexed using the WordPress Copilot connector are visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- To connect to your WordPress.com-built website data, you need your organization's WordPress.com-built website URL. 
- To connect to WordPress.com and allow the WordPress.com Copilot connector to update webpages regularly, you need to configure and enable OAuth 2.0 Authentication in WordPress.com with the credentials to access your WordPress.com-built websites. OAuth2 is a protocol that allows applications to interact with blogs on WordPress.com-built sites running Jetpack. For more information, see [Wordpress.com documentation](https://developer.wordpress.com/docs/oauth2/). 

## Get Started

### 1. Choose Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. Display name is also used as a [content source filter](/MicrosoftSearch/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Add WordPress.com-built website URL
A WordPress.com-built website URL is the unique web address assigned to each WordPress.com-built website, allowing you to access your specific WordPress.com-built website.   

### 3. Provide authentication Type
We support the OAuth 2.0 authentication method.OAuth2 is a protocol that allows applications to interact with blogs on WordPress.com-built sites running Jetpack. To enable and configure OAuth 2.0 authentication for WordPress.com-built websites. For more information, see [Wordpress.com docs for developers](https://developer.wordpress.com/docs/oauth2/). 

### 5. Staged rollout to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience.

To create the connection for a WordPress.com-built website, click **Create* to publish your connection and index published posts and pages from your WordPress.com-built website.  

For other settings, like Access Permissions, Data inclusion rules, Schema, Crawl frequency, etc., we set defaults based on what works best with WordPress.com-built website data. The default values settings are as follows.

|Page|Settings|Default values|
|--- | ---- | ---|
|Users | Access Permissions | All published pages or posts indexed using the WordPress.com Copilot connector are visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot.|
|Content | Index Content | All published posts and pages are selected by default.|
|Content | Manage Properties | To check default properties and their schema, see [content](#content).|
|Sync | Incremental Crawl | Frequency: Every 15 mins|
|Sync | Full crawl | Frequency: Every day|

## Custom Setup 

In custom setup, you can edit any of the default values for users, content, and sync.

### Users 

#### Access permissions

Currently, only published pages and posts from your WordPress.com-built websites are indexed. All data indexed using the WordPress.com Copilot connector is visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot.

### Content 

#### Filter indexed content  

You can specify conditions for indexed content. For example, you can choose to index posts or pages, and choose to index posts associated to specific categories.  

Use the preview results button to verify the sample values of the selected properties and filters. 

#### Manage properties

To add or remove available properties from your WordPress.com data source, assign a schema to the property (define whether a property is **searchable, queryable, retrievable, or refinable**), change the semantic label, and add an alias to the property. Some properties are indexed by default.

|Default property|Label|Description|Schema| 
| --- | ---- | --- | ---
| Author | Authors | Name of all the people who participated/collaborated on the item in the data source.  | Search, Query, Retrieve.| 
| Categories  |  |Categories of Posts, not available for Pages  | Query, Retrieve, Refine.| 
| Content |  | The content of Posts or Pages| Search, Retrieve. | 
| Created | Created date time | Data and time that the item was created in the data source. | Query, Retrieve. | 
| CreatedBy | Created by| Name of the person who created the item in the data source.| Search, Query, Retrieve. | 
| Excerpt | |Summaries of Posts or Pages content  |Search, Retrieve. | 
| Title |Title| The title of Posts or Pages |Search, Retrieve.|  
| Type | |The type of the file, the potential value is Post or Page | Query, Retrieve, Refine.| 
| Updated | Last modified date time | Date and time the item was last modified in the data source. |Query, Retrieve. | 
| UpdatedBy | Last modified by | Name of the person who most recently edited the item in the data source |Search, Query, Retrieve. | 
| Url | url | The target URL of the item in the data source.  |Retrieve. | 

### Sync 

You can configure full and incremental crawls based on the scheduling options present here. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs.

## Troubleshooting
After publishing your connection, you can review the status under **Data Sources** in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/graph/support).
