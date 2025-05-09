---

title: "15Five Priorities Microsoft Graph connector (preview)" 
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the 15Five Priorities Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot." 
ms.date: 02/28/2025
---

# 15Five Priorities Microsoft Graph connector (preview)

The 15Five Priorities Microsoft Graph connector allows your organization to index 15Five priority data, using Microsoft 365 Copilot and Microsoft Search. 

This documentation is for Microsoft 365 administrators or anyone who configures, runs, and monitors 15Five Priorities Microsoft Graph connector. 

## Capabilities
- Access 15Five priorities by using the power of semantic search.
- Customize your crawl frequency.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.

## Limitations

- Only the employee and their direct manager have access to the priority data using Microsoft 365 Copilot and Microsoft Search.

## Prerequisites

- Set up a 15Five account with HR administrator permissions.
- Go to the integrations admin setting page in 15Five with your HR administrator account. Create a company API key and get the access token.

## Get started

### 1. Choose display name   
Choose a display name that helps users easily recognize associated files or items in Copilot responses.

### 2. Add the instance URL
The default 15Five instance URL is `https://my.15five.com`.

### 3. Choose authentication type
Select the available authentication type and enter the access token you obtained from your 15Five company API keys setting.

### 4. Roll out to a limited audience
Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup 

Custom setup is for admins who want to edit the default values for settings. When you choose **Custom setup**, you see three other tabs: **Users**, **Content**, and **Sync**. 

### Users 

**Access permissions**

Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.  

### Content 

**Manage properties**

You can add or remove available properties from your 15Five data source. Assign a schema to the property, change the semantic label, and add an alias to the property. The following properties are indexed by default.

|Source property|Label|Description|
|--- | ---- | --- |
|Text |Not applicable  | Description of the priority. |
|Status |Not applicable  | Status of the priority. |
|UserEmail |Not applicable  | Email of the priority submitter. |
|ManagerEmail |Not applicable  | Email of the manager of the submitter. |
|CreateTime | `createdDateTime` | The time at which the file was created. |
|UpdateTime	| `lastModifiedDateTime` | The last time the file was modified. |

### Sync 

You can configure full and incremental crawls based on the scheduling options described. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. You can adjust these schedules to fit your data refresh needs.

## Troubleshooting

The following are common errors that can occur and how to resolve them.

**Your security credentials have expired for this session. Please go back and sign in again with your App key and app secret.**

Credential information has expired. Create a new key in 15Five integrations setting and copy the latest access token from the setting tab in 15Five to authenticate.

**Invalid credentials detected. Please check the credential info and check the permission scopes of the 15Five App.**

This is a common credential error. Go to the 15Five integrations setting and verify that the access token is correct.

## Next steps

After you publish your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
