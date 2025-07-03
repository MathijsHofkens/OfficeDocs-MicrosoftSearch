---

title: "Freshservice Microsoft 365 Copilot connector (preview)" 
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the Freshservice Microsoft 365 Copilot connector." 
ms.date: 03/27/2025
---

# Freshservice Microsoft 365 Copilot connector (preview)

The Freshservice Microsoft 365 Copilot connector enables your organization to index Freshservice solution article data to make it available to Microsoft 365 Copilot and Microsoft Search. 

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors the Freshservice Copilot connector. 

## Capabilities
- Access Freshservice solution articles using the power of semantic search.
- Customize your crawl frequency.
- Create workflows by using this connection and plugins from Microsoft Copilot Studio.

## Limitations
- Solution articles are indexed only if they are stored in folders set to be visible to **All**.

## Prerequisites
1. Create a Freshservice account with administrator permission in the Freshservice application.
2. Navigate to the user profile setting page with the administrator account in the Freshservice application. For more information, see [Where do I find my API key](https://support.freshservice.com/support/solutions/folders/50000000029) for details.

## Get started

### Choose display name   
Choose a display name that helps users easily recognize associated files or items in a Copilot response.

### Add the domain URL
Enter the domain URL of your Freshservice account.

### Provide authentication type
Select the available authentication type and enter the API key you obtained from your Freshservice user profile setting page.

### Roll out to a limited audience
Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup 
In custom setup you can edit any of the default values for users, content, and sync.

### Users 

#### Access permissions

Only public solution articles with folder visibility to all are indexed using the Freshservice Copilot connector. These solution articles will be visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot.

### Content 

#### Manage properties
To view available properties from your iManage Cloud data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias in the property. Some properties are selected by default.

|Default property|Label|Description|
|:--- |:---- |:--- |
|Id |Not applicable  | Unique ID of the solution article. |
|url |`url`  | URL of the solution article. |
|Title | `title` | Title of the solution article. |
|CreatedOn |`createdDateTime`  | The time at which the solution article was created. |
|LastModifiedOn | `lastModifiedDateTime` | The time at which the solution article was last modified. |
|LastModifiedUser	| `lastModifiedBy` | The name of the user who last modified the solution article. |
|FolderUrl	| `containedUrl` | The URL of folder containing the solution article. |
|FolderName	| `containerName` | The name of the folder containing the solution article. |
|Author	| `createdBy` | The name of the user who created the solution article. |
|CategoryName	|  | The category to which the folder belongs. |
|DscriptionText	|  | The content of the solution article. |
|Keywords	|  | The keywords of the solution article. |
|Tags	|  | The tags associated with the solution article. |

### Sync 
Only full crawl is supported by the Freshservice Copilot connector. The default schedule of the full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs. 

## Troubleshooting
The following are common errors that can occur and how to resolve them.

1. Your security credentials have expired for this session. Please go back and sign in again with your App key and App secret.
Credential info has expired. Please create a new key in the Freshservice API key setting and copy the latest key from the user profile setting page to authenticate.

2. Invalid credentials detected. Please check the credential info and check the permission scopes of the Freshservice App.
Common credential error. Please go back to the Freshservice API key setting and check if the key is correct.

## Next steps
After you publish your connection, you can review the status in the **Agents and connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
