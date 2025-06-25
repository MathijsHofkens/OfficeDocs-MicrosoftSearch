--- 

title: "Guru Microsoft 365 Copilot connector" 
ms.author: rantang
author: ranran1998
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
description: "Set up the Guru Microsoft 365 Copilot." 
ms.date: 3/14/2025
---

# Guru Microsoft 365 Copilot connector (preview)

With the Guru Microsoft 365 Copilot connector, your organization can index Guru cards of your Guru. After you configure the connector and index content from Guru, end users can search for those cards in Microsoft Copilot and from any Microsoft Search client. 

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors an Guru Copilot connector. 

## Capabilities
- Index cards of your Guru and supports ingestion filters by Guru Query Language 
- Retain access control lists (ACLs) defined by your organization
- Customize your crawl frequency.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.  
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content.

## Limitations
- Comments aren't indexable

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **Guru Instance Admin Account**: To connect to your Guru instance and allow Guru Microsoft 365 Copilot connector to update Guru cards regularly, you need an admin user account of your Guru instance with the permission to create an user token. Find more details [here](https://help.getguru.com/docs/gurus-api#obtaining-a-user-token).

## Get started

### Choose display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. The display name is also used as a [content source filter](/MicrosoftSearch/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.


### Provide authentication type
We support the Basic Authentication for Guru, please use User token. You can find more details [here](https://help.getguru.com/docs/gurus-api#obtaining-a-user-token).

### Staged rollout to a limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience.

At this point, you are ready to create the connection for Guru. You can click the **Create** button to publish your connection and index cards from your Guru instance. 

For other settings, like Access Permissions, Data inclusion rules, Schema, Crawl frequency, etc., we set defaults based on what works best with Guru data. You can see the default values below: 

**Page** | **Settings** | **Default values**
--- | ---- | ---
Users | Access permissions | Only people with access to this data source.
Users | Map Identities |Data source identities mapped using Microsoft Entra IDs.
Content | Index content | All cards, except the cards in personal space. 
Content | Manage properties | To check default properties and their schema, [click here](#content).
Sync | Incremental crawl | Frequency: Every 15 mins
Sync | Full crawl | Frequency: Every day

If you want to edit any of these values, you need to choose the **Custom setup** option. 

## Custom setup 

In custom setup you can edit any of the default values for users, content, and sync.

### Users 

#### Access permissions

The Guru Microsoft 365 Copilot connector supports data visible to Only people with access to this data source (recommended) or Everyone. If you choose Everyone, indexed data appears in the search results for all users. 

If you choose Only people with access to this data source, you need to further choose whether your Guru instance has Microsoft Entra ID provisioned users or non-AAD users. 

To identify which option is suitable for your organization: 

1. Choose the **Microsoft Entra ID** option if the email ID of Guru users is same as the UserPrincipalName (UPN) of users in Microsoft Entra ID. 

2. Choose the **non-AAD** option if the email ID of Guru users is **different** from the UserPrincipalName (UPN) of users in Microsoft Entra ID.

>[!Important]
>- If you choose Microsoft Entra ID as the type of identity source, the connector maps the email IDs of users obtained from Guru directly to UPN property from Microsoft Entra ID.
>- If you chose "non-AAD" for the identity type see Map your non-Azure AD Identities for instructions on mapping the identities. You can use this option to provide the mapping regular expression from email ID to UPN.
>- Updates to users or groups governing access permissions are synced in full crawls only. Incremental crawls do not currently support the processing of updates to permissions.

### Content 

**Content ingestion filters**   

You can choose what data you want to index. Use the Guru Query Language to filter your data before it is indexed, allowing you to control what data is searchable. You may use the GQL filter to index e.g. content modified after a certain time using, lastModified > 2016-01-01T00:00:00.000-00:00. [Learn more](https://developer.getguru.com/docs/guru-query-language). 

Use the preview results button to verify the sample values of the selected properties and filters. 

**Manage properties**

Here, you can check available properties from your Guru. Assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. Properties that are selected by default are listed below. 

| Properties       | Semantic Label          | Schema                      |
|-----------------|------------------------|-----------------------------|
| CollectionLink  |                        | Retrieve                    |
| CollectionName  |                        | Query, Retrieve, Search     |
| Content        | `CONTENT`               | Search                      |
| CreatedTime    | Created date time       | Query, Retrieve             |
| LastModifiedBy | Last modified by        | Query, Retrieve, Search     |
| Link          | url                      | Retrieve                    |
| ModifiedTime   | Last modified date time | Query, Refine, Retrieve     |
| Owner         | Created by               | Query, Retrieve, Search     |
| Title         | Title                    | Query, Retrieve, Search     |


### Sync 

You can configure full and incremental crawls based on the scheduling options present here. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs.

## Troubleshooting
After publishing your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
