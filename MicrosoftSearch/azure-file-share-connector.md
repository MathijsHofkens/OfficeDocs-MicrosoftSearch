---
title: "Azure File Share Microsoft 365 Copilot connector (preview)"
ms.author: dannyyao
author: dannyyaou
manager: jecui
audience: Admin
ms.audience: Admin
ms.topic: get-started
ms.service: mssearch
ms.localizationpriority: Medium
search.appverid:
- BFB160
- MET150
- MOE150
description: "Set up the Azure File Share Microsoft 365 Copilot connector"
ms.date: 12/02/2024
---

# Azure File Share Microsoft 365 Copilot connector (preview)

The Azure File Share Microsoft 365 Copilot connector allows organizations to integrate Azure File Share data into Microsoft 365. It enables users to access indexed files via Microsoft Search and Copilot while ensuring security by adhering to NTFS permissions.

This guide is designed for Microsoft 365 administrators responsible for configuring, managing, and monitoring the Azure File Copilot connector.

## Capabilities
- Seamless access to Azure File Share data within Microsoft Search and Copilot.
- Ensures data security by integrating NTFS permissions with Azure Active Directory (AAD).
- Performs regular full crawls to update indexed content.
- Indexes file content, metadata, directory structures, and access control lists (ACLs).

## Limitations
- Files up to 100 MB in size are indexed, with a maximum of 4 MB of text content extracted per file.
- Supported file formats include:
  - Microsoft Office files
  - PDFs
  - Text files
  - JSON files
- Non-text files are excluded by default.

## Prerequisites

Ensure the following requirements are met before starting the setup process:

### Azure File Share Configuration
- Mount your Azure File Share on a device.
- Install and register the **Graph Connector Agent (GCA)** on the same device.

### User Credentials
Use the same credentials for:
- Mounting the Azure File Share.
- Running the Graph Connector Agent.
- Configuring the connector in the Microsoft 365 Admin Center.

##Get started

### Choose a display name
Provide a clear, descriptive name for the connector. For example:  
`Azure File Share - Marketing Team`

### Add the source folder paths
Enter the UNC path for the Azure File Share, such as:  
`\\testpath.file.core.windows.net\test_folder\test_folder2`

### Provide authentication type
- Select the registered **Graph Connector Agent (GCA)** for your tenant.
- Use Windows authentication with valid admin credentials.

### Roll out to a limited audience
Deploy the connection to a limited user base if you want to validate it in Copilot and other Search surfaces before you roll it out to a broader audience. For more information, see [Staged rollout for connectors](staged-rollout-for-graph-connectors.md).

For other settings, like Access Permissions, Data inclusion rules, Schema, Crawl frequency, etc., we set defaults based on what works best with AEM Assets data. You can see the default values below: 

|Page|Settings|Default values|
|----------|-----------------------|-------------------------------------------------------------------|
| Users | Access Permissions    | Respects NTFS permissions; only authorized files are accessible. |
| Content | Index Metadata       | Includes properties like file name, owner, last modified, and file path. |
| Sync* | Full Crawl Frequency  | Once daily.                                                      |

## Custom Setup
In custom setup,  you can edit any of the default values for users, content, and sync.

### Users
#### Access Permissions
The connector adheres to NTFS ACLs to control file access. Administrators can broaden access, but maintaining default permissions is recommended for security.

#### Enhancing Metadata
You can create custom properties to extend the metadata available for search.

1. Name the property as it will appear in search results.

2. Choose one of the following:
   - **Static Value**: A constant value applied to all search results.
   - **String/Regex Mapping**: A dynamic value based on specific rules.

3. **Configure the Value**  
   - For static values, enter the desired text.
   - For regex-based values:
     - In **Add Expressions**, choose a default property.
     - Provide a sample value for preview.
     - Add up to three regex expressions.  
       [Learn more about regex expressions](/dotnet/standard/base-types/regular-expression-language-quick-reference).
     - Combine extracted values using a formula in the **Create Formula** section.

#### Managing schema and labels
To manage schema and assign labels to properties, follow the [general setup instructions](./configure-connector.md).

## Troubleshooting
For more information, see [Troubleshooting Guide](troubleshoot-azure-file-share-connector.md).

## Next Steps
After publishing your connector, you can review the status under **Data sources** in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/graph/support).
