---
title: "GitLab Microsoft Graph connectors"
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
description: "Set up the GitLab Microsoft Graph connectors for Microsoft Search and Microsoft 365 Copilot."
ms.date: 02/14/2025
---

# GitLab Microsoft Graph connectors

The GitLab Microsoft Graph connectors (GitLab Issue, GitLab Merge Request, and GitLab Knowledge) allow your organization to index merge requests, issues, wikis, and documentation stored in GitLab. After you configure the connector and index GitLab content, users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot.

This article is intended for Microsoft 365 administrators or anyone who configures, runs, or monitors GitLab Microsoft Graph connectors.

## Capabilities

- Index GitLab repositories, merge requests, and access issues, wikis, and documentation.
- Enable Microsoft Search and Microsoft 365 Copilot to retrieve GitLab data efficiently.
- Maintain GitLab ACLs and user permissions.
- Allow administrators to customize crawl frequency and indexing preferences.

## Limitations

- The connector does not support indexing GitLab CI/CD pipelines beyond status indexing.
- Only repositories, issues, merge requests, .md, .txt files, and wikis are indexed.
- On-premises/self-hosted GitLab instances aren't currently supported.
- Banning users is not supported as a permission rule. As a workaround, administrators can remove users from groups instead.
- Restricting group access by IP address is not supported. We recommend that administrators create a private group to manage access.

## Prerequisites

Before you set up the connector, make sure that:

1. Your GitLab instance is accessible via API.
2. You generate a **Client ID** and **Client secret** from GitLab for authentication.
3. The user account used for authentication has access to the repositories, issues, merge requests, knowledge files, and wiki pages to be indexed.
4. The **Client ID** and **Client secret** have the `read_api` permission scope.
5. Users who access indexed GitLab data have corresponding **Microsoft Entra ID** identities for permission mapping.
6. Specify the following **redirect URLs** when configuring GitLab authentication:

   - **For Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`.  
   - **For Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`.

## Get started

### 1. Choose display name
Choose a display name that helps users recognize merge requests, issues, or documentation in a Copilot response.

### 2. Authenticate

- Enter your **Client ID** and **Client secret** from GitLab.
- Choose **Authorize** to sign in and grant access.
- Grant the required API scopes.

### 3. Roll out to limited audience
Before you deploy the connector, test the connection with a limited user base in Copilot and Microsoft Search.

## Custom setup
Custom setup is for admins who want to edit the default values for any settings. When you choose **Custom setup**, you see three other tabs: **Users**, **Content**, and **Sync**. 

### Users
#### Identity mapping
To ensure correct permission enforcement, map GitLab user identities to Microsoft Entra ID. The following are the options:
  - **Email:** Matches GitLab user emails with Microsoft Entra ID emails. (Default and recommended mapping)
  - **Username:** Matches GitLab user names to Microsoft Entra ID user principal name (UPN).
  - **Name:** Maps GitLab user names with Microsoft Entra ID display names.

If direct mapping fails, use **regular expressions (regex)** for transformation.

### Content
You can verify property mappings in the sample data for metadata such as **titles**, **descriptions**, **statuses**, and **timestamps** on the **Content** tab.

### Sync
You can configure **incremental** and **full** crawls. The following are the default values:

  - Incremental crawl runs **every 15 minutes** by default.
  - Full crawl runs **daily** to ensure up-to-date indexing.

## Next steps

- Review the connection status in the Microsoft 365 admin center. 
- For troubleshooting information, see the [GitLab troubleshooting guide](troubleshoot-gitlab-connector.md).
- If you have issues or need support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
