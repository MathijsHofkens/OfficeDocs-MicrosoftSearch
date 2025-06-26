---
title: "Troubleshooting the GitLab Microsoft 365 Copilot connector"
ms.author: dannyyao
author: dannyyaou
manager: jecui
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: mssearch
ms.localizationpriority: Medium
search.appverid:
- BFB160
- MET150
- MOE150
description: "Find information to troubleshoot issues with the GitLab Microsoft 365 Copilot connector."
ms.date: 02/28/2025
---

# Troubleshooting the GitLab Microsoft 365 Copilot connector

The following table lists common errors that can occur with the GitLab Microsoft 365 Copilot connector and possible reasons for the errors. Errors can occur when you configure the connector or during crawls.

| Step | Error message | Possible reason |
|:------------ |:------------ |:------------|
| Authentication | Having trouble? Try signing in again. | The sign in attempt in the popup window was unsuccessful. Try again. |
| Authentication | The account doesn't have permission to access this data source. Make sure that the application has been granted the correct scopes and the account has access.| The authentication was successful, but the user lacks the necessary GitLab permissions. Make sure that the _read_api_ scope is granted, and that the user has access to the selected repositories, issues, and wikis. |
| Authentication | The Graph Connector Agent associated with the connection is not reachable. Either the agent is not running or app credentials have expired or been revoked. | The on-premises Microsoft Graph connector agent is offline, or the credentials expired. Verify that the agent is running and has internet access, and that the application credentials are active. |
| Authentication | An unknown error occurred. Try again after some time. If this error persists, contact support. | A transient issue or potential code bug. Try again later. If the problem continues, contact support. |
| Crawl Initialization | Failed to connect to GitLab with the provided credentials. Verify that the credentials are correct. | The authentication details were changed or revoked after setup. Update the credentials in the connector settings. |
| Crawl Initialization | Failed to connect to GitLab. Make sure your GitLab is up and running, and the Graph Connector Agent has network access to the GitLab server.| The GitLab server is unreachable due to network issues, incorrect GitLab URL, or firewall restrictions. Make sure that GitLab is accessible from the connector. |
| Item Fetching | The crawler account does not have permissions for the item. Verify that the crawler account was granted access to this item in GitLab. | The crawler lacks read access for the item. Make sure that the authentication account has the appropriate repository, issue, or wiki access. |

## Next steps

If the issue persists, verify your configuration settings, authentication credentials, and network connectivity.  

For more support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
