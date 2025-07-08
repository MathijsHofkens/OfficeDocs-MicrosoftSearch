---
title: "GitHub Server Knowledge Microsoft 365 Copilot connector (preview)"
ms.author: dannyyao
author: dannyyaou
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
description: "Set up the GitHub Server Knowledge Microsoft 365 Copilot connector."
ms.date: 03/06/2025
---

# GitHub Server Knowledge Microsoft 365 Copilot connector (preview)
The GitHub Server Knowledge Microsoft 365 Copilot connector allows your organization to index knowledge stored in GitHub. After you configure the connector and index GitHub content, users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot.
This article is intended for Microsoft 365 administrators or anyone who configures, runs, or monitors GitHub Server Knowledge Copilot connector.

## Capabilities
- Index GitHub knowledge from all public repositories and the internal repositories within organizations where the corresponding GitHub App is installed.
- Enable Microsoft Search and Microsoft 365 Copilot to retrieve GitHub data efficiently.
- Maintain GitHub ACLs and user permissions.
- Allow administrators to customize crawl frequency and indexing preferences.

## Limitations
- The connector does not support indexing GitHub CI/CD pipelines beyond status indexing.
- On-premises/self-hosted GitHub instances aren't currently supported.
- The connector is designed to support GitHub Enterprise. Users on Free or Team plans may experience limited functionality or reduced support.

## Prerequisites
Before you set up the connector:

1. Make sure that your GitHub instance is accessible via API.
2. Set up the GitHub App for authentication.
3. Verify that the user account used for authentication has access to the repositories and knowledge to be indexed.
4. Make sure that users who access indexed GitHub data have corresponding **Microsoft Entra ID** identities for permission mapping.
5. Install and register the Graph Connector Agent (GCA) on the a device with access to the GitHub instance. The version must be 3.1.11.0 or later.

### Set Up a GitHub App for Authentication 
Follow the steps below to create a GitHub App for use with your Copilot Connector:

1. In GitHub, click your profile photo (top right), select **Your organizations**, and choose the organization where the Graph Connector should pull data from.

   :::image type="content" alt-text="Screenshot that shows how to access 'Your organizations'." source="media/github-connector/organizations-nav.png" lightbox="media/github-connector/organizations-nav.png":::

2. On the organization overview page, click **Settings**.

   :::image type="content" alt-text="Screenshot that shows how to access 'Settings' within the organization page." source="media/github-connector/organization-overview.png" lightbox="media/github-connector/organization-overview.png":::

3. In the left sidebar, scroll down to **Developer settings** and click **GitHub Apps**.

   :::image type="content" alt-text="Screenshot that shows how to access GitHub Apps." source="media/github-connector/github-apps.png" lightbox="media/github-connector/github-apps.png":::

4. Click **New GitHub App**.

   :::image type="content" alt-text="Screenshot that shows entry point to creation of new app." source="media/github-connector/new-github-app.png" lightbox="media/github-connector/new-github-app.png":::

5. Configure the app:
   - **GitHub App name**: Enter a name of your choice.
   - **Homepage URL**: Copy the URL from your browser’s address bar (refer to the image if needed).
   - **Callback URL**:  
     - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`  
     - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

       :::image type="content" alt-text="Screenshot that shows the initial part of the app configuration including name and URLs." source="media/github-connector/github-app1.png" lightbox="media/github-connector/github-app1.png":::

6. Check **Request user authorization (OAuth) during installation** and disable the **Webhook** option.

   :::image type="content" alt-text="Screenshot that of some check boxes required for the app configuration." source="media/github-connector/github-app2.png" lightbox="media/github-connector/github-app2.png":::

7. Set the following permissions:
    - **Repository permissions**
        - Administration - **Read-only**
        - Metadata - **Read-only**
        - Contents - **Read-only**
    - **Organization permissions**
        - Administration - **Read-only**
        - Members - **Read-only**
    - **Account permissions**
        - Email addresses - **Read-only**

8. Under **Where can this GitHub App be installed**, select **Any account**, then click **Create GitHub App**.

   :::image type="content" alt-text="Screenshot that shows the final steps of the GitHub app set up." source="media/github-connector/github-app3.png" lightbox="media/github-connector/github-app3.png":::

9. On the GitHub App’s **General** page, generate and copy the **client secret** by clicking **Generate a new client secret**. Then click **Install App**.

   :::image type="content" alt-text="Screenshot that shows the credentials of the app including Client Id and Client secret." source="media/github-connector/github-app-credentials.png" lightbox="media/github-connector/github-app-credentials.png":::

10. Select the organization where you want the app to be installed. **After installation**, you're ready to configure the connector.

    :::image type="content" alt-text="Screenshot that shows the app installation dialog." source="media/github-connector/github-install.png" lightbox="media/github-connector/github-install.png":::

## Get started

### Choose display name
Choose a display name that helps users recognize the connection in a Copilot response.

### Provide authentication details
- Enter your **Client ID** and **Client secret** from your GitHub App.
- Choose **Authorize** to sign in and grant access. We recommend using separate user accounts for OAuth authentication with each connection, as GitHub's rate limit is calculated individually per user.
- Grant the required API scopes.

### Instance URL 
Enter the instance URL of your GitHub Enterprise Server. This is the root domain of your internal GitHub server. For example, https://github.yourdomain.com. 

### Graph connector agent 
Set up the Graph connector agent in a device with access to your GitHub instance following the [setup guide](./graph-connector-agent.md). And select the name of your Graph connector agent instance. 

### Roll out to limited audience
Before you deploy the connector, test the connection with a limited user base in Copilot and Microsoft Search.

## Custom setup
In custom setup you can edit any of the default values for users, content, and sync.

### Users
#### Identity mapping
To ensure correct permission enforcement, map GitHub user identities to Microsoft Entra ID. The following are the options:
  - **Email:** Maps GitHub email to Microsoft Entra ID user properties.
  - **Login:** Maps GitHub logins with Microsoft Entra ID user properties.
  - **Name:** Maps GitHub name with Microsoft Entra ID user properties.

If direct mapping fails, use **regular expressions (regex)** to transform the data. For example: `[a-zA-Z0-9]+`
For personal accounts, mapping accuracy may be impacted due to variations in email domains and individual email visibility settings.

### Content
On the **Content** tab, you can verify property mappings in the sample data for metadata such as **content**, **labels**, **description**, and **timestamps**.

#### Time-range filter 
You can configure a time-range filter in the content tab. The default setting is 365 days.

### Sync
You can configure incremental and full crawls. The following are the default values:

  - Incremental crawl runs every 15 minutes by default.
  - Full crawl runs daily to ensure up-to-date indexing.

## Firewall settings

For added security, you may configure IP firewall rules for your GitHub instance. For more information, see [IP firewall rules](/azure/azure-sql/database/firewall-configure). 
Add the following client IP ranges in the firewall settings.

| Region | Microsoft 365 Enterprise                  | Microsoft 365 Government                 |
|--------|-------------------------------------------|------------------------------------------|
| NAM    | 52.250.92.252/30, 52.224.250.216/30       | 52.245.230.216/30, 20.141.117.64/30      |
| EUR    | 20.54.41.208/30, 51.105.159.88/30         | NA                                       |
| APC    | 52.139.188.212/30, 20.43.146.44/30        | NA           

Setting up an IP restriction could cause the connector to stop working and lead to crawl failures. Administrators can resolve this issue and resume crawling by adding the connector's IP address to the allowlist according to the above table.

## Next steps
- Click Auto generation to quickly populate your connection description with recommended defaults. It saves time and ensures consistency in your setup.
- Review the connection status in the Microsoft 365 Admin Center.
- For configuration about GitHub Apps and authentication, please check out below documentations

| Topic                                                | Documentation link                                                                                                                                                                                                                                                                                                                                 |
|:------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| How to create/register a GitHub App                  | [Registering a GitHub App](https://docs.github.com/en/enterprise-cloud@latest/apps/creating-github-apps/registering-a-github-app/registering-a-github-app)                                                                                                                                                                                          |
| How to install a GitHub App into organizations       | [Installing your own GitHub App](https://docs.github.com/en/enterprise-cloud@latest/apps/using-github-apps/installing-your-own-github-app)                                                                                                                                                                                                        |
| How to authenticate a GitHub App on behalf of a user | [About creating GitHub Apps (acting on behalf of a user)](https://docs.github.com/en/enterprise-cloud@latest/apps/creating-github-apps/about-creating-github-apps/about-creating-github-apps#github-apps-that-act-on-behalf-of-a-user)<br>[Authenticating with a GitHub App on behalf of a user](https://docs.github.com/en/enterprise-cloud@latest/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-with-a-github-app-on-behalf-of-a-user) |

If you have issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
