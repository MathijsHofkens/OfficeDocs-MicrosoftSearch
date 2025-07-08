---
title: "Bitbucket Microsoft 365 Copilot connector (preview)"
ms.author: dannyyao
author: dannyyaou
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
description: "Set up the Bitbucket Microsoft 365 Copilot connector."
ms.date: 02/14/2025
---

# Bitbucket Microsoft 365 Copilot connector (preview)

The Bitbucket Microsoft 365 Copilot connector allows your organization to index pull requests and documentation (.txt and .md files) stored in Bitbucket. After you configure the connector and index Bitbucket content, users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot.

This article is intended for Microsoft 365 administrators or anyone who configures, runs, or monitors the Bitbucket Copilot connector.

## Capabilities
- Index Bitbucket repositories, pull requests, and documentation.
- Enable Microsoft Search and Microsoft 365 Copilot to retrieve Bitbucket data efficiently.
- Maintain Bitbucket ACLs and user permissions.
- Allow administrators to customize crawl frequency and indexing preferences.

## Limitations
- The connector does not support indexing Bitbucket CI/CD pipelines beyond status indexing.
- Only repositories, pull requests, .md, and .txt files are indexed.
- On-premises/self-hosted Bitbucket instances aren't currently supported.
- The connector may leave the LastModifiedBy field blank in cases where Git changes are not mapped to a Bitbucket account. This occurs when a manual configuration linking Git changes to Bitbucket user accounts is not completed before an incremental crawl.

## Prerequisites

1. Your Bitbucket instance is accessible via API.
2. The user account used for authentication has access to the repositories, pull requests, and knowledge files to be indexed.
3. Users who access indexed Bitbucket data have corresponding **Microsoft Entra ID** identities for permission mapping.
4. Set up an OAuth consumer on Bitbucket
    1. Go to your workspace page on Bitbucket. 
    2. Click the gear icon on the top right corner and select **Workspace settings**. 
    3. On the left navigation, select OAuth Consumers located under the Workflows section. 
    4. Click **Add consumer** and fill out according to the following redirect URLs: 
    - For Microsoft 365 Enterprise, use `https://gcs.office.com/v1.0/admin/oauth/callback`
    - For Microsoft 365 Government, use `https://gcsgcc.office.com/v1.0/admin/oauth/callback`  
    5. Enable the key to have the following permissions configured to read issues:
    - Account
    - Repositories
    - Pull requests
    6. Save the configuration and copy the key and secret values 

We recommend using separate user accounts for OAuth authentication with each connection, as Bitbucket's rate limit is calculated individually per user.

## Get started

### Choose display name
Choose a display name that helps users recognize merge requests or documentation in a Copilot response.

### Bitbucket instance URL
Enter the URL of your Bitbucket instance (for example, `https://bitbucket.org/testinstance`).

### Authentication type
1. Enter your Client ID using the key from your Bitbucket OAuth consumer, and your Client Secret using the corresponding OAuth consumer secret.
2. Choose **Authorize** to sign in and grant access.
3. Click **Authorize** to sign in and grant the required access permissions.

### Roll out to limited audience
Before you deploy the connector, test the connection with a limited user base in Copilot and Microsoft Search.

## Custom setup
In custom setup, you can edit any of the default values for users, content, and sync.

### Users
#### Identity mapping
By default, due to the limitation of the Bitbucket API, the connector maps emails in Microsoft Entra ID using public names from Bitbucket.
If this mapping does not align with your configuration, customize the identity mapping.

To ensure correct permission enforcement, map Bitbucket user identities to Microsoft Entra ID. The following are the options:
  - **Full name:** Matches Bitbucket full names to Microsoft Entra ID user properties.
  - **Public name:** Maps Bitbucket public names with Microsoft Entra ID user properties.

If direct mapping fails, use **regular expressions (regex)** for transformation. For example:

1. Select **Mail** as the **Microsoft Entra user property**.
2. Select **Full Name** as the **non-Microsoft Entra user property**.
3. Use a regular expression such as `([^@]+)` to capture a sequence of one or more characters that are before the `@` symbol.
4. Create a formula to complete the mapping, such as `{0}@<your-domain>`.

### Content
On the **Content** tab, you can verify property mappings in the sample data for metadata such as **content**, **labels**, **description**, and **timestamps**.

### Sync
You can configure **incremental** and **full** crawls. The following are the default values:

  - Incremental crawl runs **every 15 minutes** by default.
  - Full crawl runs **daily** to ensure up-to-date indexing.

## Next steps

- Review the connection status in the Microsoft 365 Admin Center.
  
If you have issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
