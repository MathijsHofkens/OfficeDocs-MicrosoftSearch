---

title: "15Five High Fives Microsoft Graph connector (preview)" 
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
description: "Set up the 15Five High Fives Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot." 
ms.date: 02/27/2025
---

# 15Five High Fives Microsoft Graph connector (preview)

The 15Five High Fives Microsoft Graph connector enables your organization to index 15Five high five data to make it available to Microsoft 365 Copilot and Microsoft Search. 

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors the 15Five High Fives Microsoft Graph connector. 

## Capabilities

- Access 15Five high fives using the power of semantic search.
- Customize your crawl frequency.
- Create workflows by using this connection and plugins from Microsoft Copilot Studio.

## Limitations

- Only public high fives are indexed.

## Prerequisites

Before you create a Microsoft Graph 15Five High Fives connector, complete the following steps:

1. Create a 15Five account with HR administrator permission.
2. As an HR administrator, go to the Integrations admin setting page in 15Five. Create a company API key and get the access token.

## Get started

### 1. Choose display name   
Choose a display name that helps users easily recognize associated files or items in a Copilot response.

### 2. Add the instance URL
The default 15Five instance URL is `https://my.15five.com`.

### 3. Choose authentication type
Select the available authentication type and enter the access token you obtained from your 15Five company API keys setting.

### 4. Roll out to a limited audience
Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup 

Custom setup is for admins who want to edit the default values for the settings. When you choose **Custom setup**, you see three other tabs: **Users**, **Content**, and **Sync**. 

### Users 

**Access permissions**

All 15Five high five data indexed via the 15Five High Fives Microsoft Graph connector is visible to all Microsoft 365 users in your tenant in Microsoft Search or Copilot.

### Content 

**Manage properties**

You can add or remove available properties from your 15Five data source. Assign a schema, change the semantic label, and add an alias to the property. The following properties are indexed by default.

|Source property|Label|Description|
|--- | ---- | --- |
|Text |Not applicable  | Description of the high five content. |
|CreatorEmail |Not applicable  | Email of the user who gives a high five. |
|CreatorName | `createdBy` | Name of the user who gives a high five. |
|Receivers |Not applicable  | Name of the users who receive a high five. |
|CreateTime | `createdDateTime` | The time at which the high five was created. |
|UpdateTime	| `lastModifiedDateTime` | The last time the high five was modified. |


### Sync 

You can configure full and incremental crawls based on the scheduling options described. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. You can adjust these schedules to fit your data refresh needs.



## Troubleshooting

The following are common errors that can occur and how to resolve them.

**Your security credentials have expired for this session. Please go back and sign in again with your App key and App secret.**

Credential information has expired. Create a new key in 15Five integrations setting and copy the latest access token from the setting tab in 15Five to authenticate.

**Invalid Credentials detected. Please check the credential info and check the permission scopes of the 15Five App.**

This is a common credential error. Go to the 15Five integrations setting and verify that the access token is correct.

## Next steps

After you publish your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
