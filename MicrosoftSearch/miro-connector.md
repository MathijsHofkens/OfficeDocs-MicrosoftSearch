--- 

title: "Miro Microsoft 365 Copilot connector (preview)" 
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
description: "Set up the Miro Microsoft 365 Copilot connector." 
ms.date: 03/11/2025
---

# Miro Microsoft 365 Copilot connector (preview)
The Miro Microsoft 365 Copilot allows your organization to index boards from Miro. After you configure the connector, users can search for these boards from Miro in Microsoft 365 Copilot and any Microsoft Search client.

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Miro Copilot connector.

> [!NOTE]
> The Miro Copilot connector is in public preview. To get access to the connector, enable the [Targeted release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- Access boards in Copilot by using the power of Semantic search.
- Customize your crawl frequency.
- Create an agent using the data source of the connection from Microsoft Copilot Studio.

## Limitations
- Only [text items](https://developers.miro.com/docs/text-1) on the board are indexed. Content in cards, sticky notes, embeds, tags, frames, mind maps, previews, and shapes is not indexed. For more information, see [Miro docs for developers](https://developers.miro.com/docs/board-items).   
- Doesn't index comments or replies.

## Prerequisites

### 1. Create a Developer team for your Miro account
Create or use an existing Miro account to access Miro and click the [link](https://miro.com/app/dashboard/?createDevTeam=1) to create a Developer team for your active Miro account. If your organization is on an Enterprise plan, go to [Enterprise Developer teams](https://help.miro.com/hc/articles/4766759572114). For more information, see [Create a Developer team](https://developers.miro.com/docs/create-a-developer-team).

### 2. Create your app in Miro
Sign in to Miro and create a new app in [Your apps](https://miro.com/app/settings/user-profile/apps).

### 3. Add permissions to your app
Add the `boards:read Read boards you have access to` plan in the app you created in your app's configuration

### 4. Add redirect URL to your app
In the app creation page, add the following links to the "Redirect URL for OAuth2.0" field. 

* For M365 Enterprise, copy and paste: `https://gcs.office.com/v1.0/admin/oauth/callback`

* For M365 Government, copy and paste: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

### 5. Install your app and record credentials
Click **Install app and get OAuth token** and record the `Client ID` and `Client secret` from the app credentials.

## Get started

### 1. Configure display name
A display name is used to identify each citation in Copilot to help users easily recognize the associated file or item. The display name also signifies trusted content and is used as a [content source filter](/MicrosoftSearch/custom-filters#Content-source-filters). A default value is provided for this field; you can customize it to a name that users in your organization recognize.

### 2. Add Team ID
A Miro Team ID is an identifier for a specific team within the Miro platform. To find your Team ID, sign in to Miro in a browser, go to the settings of the team from your dashboard, and copy the ID.

> [!NOTE]
> You can only associate one team ID in the connection. If you have multiple team IDs in your Miro workspace, create a separate connection.

### 3. Provide the authentication Type

Enter the Client ID and Client secret you obtained from your Miro app. For more information, see [Get started with OAuth 2.0 and Miro](https://developers.miro.com/docs/getting-started-with-oauth).

### 4. Roll out to limited audience

Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before you expand the rollout to a broader audience. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](staged-rollout-for-graph-connectors.md).

To create the connection for Miro, choose **Create** to publish your connection and index boards from your Miro account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, default values are set based on what works best with Miro data.

| Users | Description |
|----|---|
| Access permissions | Only people with access to the content in the data source. |
| Map identities | Data source identities mapped using Microsoft Entra IDs. |

| Content | Description |
|---|---|
| Manage properties | To check default properties and their schema. |

| Sync | Description |
|---|---|
| Full crawl | Frequency: Every day |

## Custom setup
In custom setup you can edit any of the default values for users, content, and sync. 

### Users

#### Access permissions
The Miro Copilot connector supports search permissions that are visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it.

#### Mapping identities
The default method for mapping your data source identities with Microsoft Entra ID is to verify that the email ID of Miro users is the same as the user principal name (UPN) or email of the users in Microsoft Entra. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is best for your organization:

- Choose the **Microsoft Entra ID** option if the email ID of Miro users is the **same** as the users' UPN or email in Microsoft Entra ID.
- Choose the **Non-Microsoft Entra ID** option if the email ID of Miro users is **different** from the users' UPN and email in Microsoft Entra ID.

### Content

#### Manage properties

To add or remove available properties from your Miro data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), and change the semantic label and add an alias to the property. Some properties are selected by default.

|Source property|Label|Description|Schema|
|:---|:---|:---|:---|
|	Body	|	NA	|	NA	|	Search	|
|	CreatedAt	|	Created date time	|	Date and time that the item was created in the data source	|	Query, Retrieve.	|
|	CreatedBy	|	Created by	|	The user who created the item 	|	Query, Retrieve, Search.	|
|	Description	|	NA	|	NA	|	Query, Retrieve.	|
|	Id	|	NA	|	NA	|	Query, Retrieve.	|
|	ModifiedAt	|	Last modified date time	|	Date and time the item was last modified in the data source	|	Query, Retrieve.	|
|	ModifiedBy	|	Last modified by	|	The user who made the last modification 	|	Query, Retrieve, Search.	|
|	Name	|	Title	|	The title of the item that you want shown in Copilot and other search experiences	|	Query, Retrieve, Search.	|
|	Team	|	NA	|	NA	|	Query, Retrieve.	|
|	ViewLink	|	url	|	The target URL of the item in the data source	|	Query, Retrieve.	|

#### Preview data

Click **preview results** to verify the sample values of the selected properties and query filter.

### Sync
The refresh interval determines how often your data is synced between the data source and the Miro Copilot connector index. Only full crawl refresh intervals are supported. For more information, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval.

## Troubleshooting
The following are common errors and how to resolve them.

1. Required permission scopes are missing. Ensure the necessary scopes are selected in the Miro App.
 
You don't have the required permission scopes. Make sure that you selected `boards:read Read boards you have access to` in the permission field of your Apps configuration.

2. OAuth 2.0 flow failed. Verify the credential information and make sure that the Miro App is configured with the correct settings.

This is a common authentication error. Go back to the Miro app and verify that the OAuth2 in **Settings** is correctly configured.

4. OAuth 2.0 flow failed. Confirm that the Miro user associated with this team access token holds the team admin role and is an active user.

This is a common authentication error. Go back to the Miro app console and verify that the creator has an admin role and the account status is active.

5. Your security credentials have expired for this session. Go back and sign in again with your App key and App secret.

Your credential information has expired. Refresh the Miro app and copy the latest Client ID and Client secret from the settings tab to authenticate.

6. Invalid Credentials detected. Check the credential info and check the permission scopes of the Miro App.

This is a common credential error. Go back to the Miro App and verify that the scopes in **Permissions** are correctly configured.

## Next steps
After you publish your connection, you can review the status in the **Agents and connectors** section of the [admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/graph/support).
