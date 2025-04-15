---
title: "GitHub Cloud Issues Microsoft Graph connector (preview)"
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
description: "Set up the GitHub Cloud Issues Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot."
ms.date: 02/14/2025
---

# GitHub Cloud Issues Microsoft Graph connector (preview)
The GitHub Cloud Issues Microsoft Graph connector allows your organization to index issues stored in GitHub. After you configure the connector and index GitHub content, users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot.
This article is intended for Microsoft 365 administrators or anyone who configures, runs, or monitors GitHub Cloud Issues Microsoft Graph connector.

## Capabilities
- Index GitHub issues.
- Enable Microsoft Search and Microsoft 365 Copilot to retrieve GitHub data efficiently.
- Maintain GitHub ACLs and user permissions.
- Allow administrators to customize crawl frequency and indexing preferences.

## Limitations
- The connector does not support indexing GitHub CI/CD pipelines beyond status indexing.
- On-premises/self-hosted GitHub instances aren't currently supported.
- The connector is designed to support GitHub Enterprise. Users on Free or Team plans may experience limited functionality or reduced support.

## Prerequisites
1. Make sure that your GitHub instance is accessible via API.
2. Set up a GitHub App for authentication. You can specify which organizations and repositories a GitHub app is authorized to access, effectively determining what content the connector will crawl.
3. Generate a **Client ID** and **Client secret** from the GitHub App for authentication. 
4. Verify that the user account used for authentication has access to the repositories and issues to be indexed.
5. Verify that the GitHub App has the following permissions configured to read issues:
    - **Repository permissions**
        - Administration - **Read-only**
        - Metadata - **Read-only**
        - Issues - **Read-only**
    - **Organization permissions**
        - Administration - **Read-only**
        - Members - **Read-only**
    - **Account permissions**
        - Email addresses - **Read-only**
6. Make sure that users who access indexed GitHub data have corresponding **Microsoft Entra ID** identities for permission mapping.
7. For enterprise-managed users who authenticate via Single Sign-On (SSO), the account must be signed in before performing any actions, as the GitHub authentication flow does not currently support SSO login.

## Get started

### 1. Choose display name
Choose a display name that helps users recognize the connection in a Copilot response.

### 2. Provide authentication details
- Enter your **Client ID** and **Client secret** from your GitHub App.
- Choose **Authorize** to sign in and grant access. We recommend using separate user accounts for OAuth authentication with each connection, as GitHub's rate limit is calculated individually per user.
- Grant the required API scopes.

### 3. Roll out to limited audience
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

## Firewall settings (for the Azure SQL Microsoft Graph connector only)

For added security, you may configure IP firewall rules for your Azure SQL Server or database. For more information, see [IP firewall rules](/azure/azure-sql/database/firewall-configure). 
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
