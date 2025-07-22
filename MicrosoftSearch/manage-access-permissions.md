---
ms.date: 07/18/2025
title: "Review and Manage Access Permissions"
ms.author: vivg
author: vivg
manager: harshkum
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
description: "Review and Manage Access Permissions in Microsoft Copilot Connectors."
---

# Review and manage access permissions in Microsoft Copilot connectors
 
Admins can review and validate access permissions for each Microsoft Copilot connector directly from the connection details pane. This guide walks you through how to verify whether the configured permissions align with your intended settings, and what to do if they don't.
 
## Why access permissions matter
 
Microsoft Copilot connectors index content from external data sources into Microsoft 365 Search and Copilot. To ensure secure and compliant access, it's critical that the access permissions configured during setup reflect your organization's intended visibility model.
 
Incorrect permission settings such as unintentionally granting access to "Everyone" can lead to oversharing of sensitive content.
 
## Step 1: Open the connection details pane
 
1. Go to the [Microsoft 365 Admin Center](https://admin.microsoft.com).
2. Navigate to Copilot > Connectors > Your Connections.
3. Select the connector you want to review.
4. In the connection overview, click on the connection name to open the **details pane**.

   [![Screenshot that shows the connectors list with a connector selected and details pane showing information about this connector.](media/datasourcestab.png)](media/datasourcestab.png#lightbox)
 
## Step 2: Review the access permissions
 
In the connection details pane, locate the **Permissions** section. This section shows one of the following settings:
 
- **Only people with access to this data source**: The connector respects source system ACLs (Access Control Lists).
- **Visible to everyone**: The connector grants access to all users in the organization.
 
## Step 3: What if the permissions don't look right?
 
If the access permissions don't match your intended configuration, you must:
1. **Delete** the existing connection.
2. **Recreate** the connection using the **Custom setup** flow to explicitly configure access permissions.
 
> [!Note]
> Editing access permissions after creation isn't supported currently. Deletion and recreation is the only reliable way to correct misconfigured access.
