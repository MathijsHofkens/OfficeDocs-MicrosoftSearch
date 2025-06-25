--- 
ms.date: 02/26/2025
title: "Troubleshooting the Veeva Vault Microsoft 365 Copilot connector" 
ms.author: dannyyao
author: dannyyaou
manager: jecui
audience: Admin 
ms.audience: Admin 
ms.topic: troubleshooting-general
ms.service: mssearch 
ms.localizationpriority: medium 
description: "Find troubleshooting information for the Veeva Vault Microsoft 365 Copilot connector." 
--- 

# Troubleshooting the Veeva Vault Microsoft 365 Copilot connector

The following table lists common errors that can occur when you configure the Veeva Vault Microsoft Graph connectors.

| Error | Description | Resolution|
|:---------|:-------------------------|:------------------------|
| `INVALID_SESSION_ID`    | Authentication session expired or invalid.| Reauthenticate with valid credentials.                             |
| `INSUFFICIENT_ACCESS`   | User lacks permissions to access files.   | Verify user roles and ACLs in Veeva Vault.                   |
| `API_LIMIT_EXCEEDED`    | Too many API requests made in a short period. | Adjust crawl frequency or retry after some time.                  |
| Missing Properties or Documents| Required metadata properties are not enabled. | Make sure that metadata properties are enabled in Veeva Vault and test retrieval.|

To view more error types, select the connection and choose **error details** > **error code**. For more information, see [Monitor your connections](./manage-connector.md).

## Share your feedback

We value your feedback on the performance of the Veeva Vault Microsoft Graph connectors. To help us improve, please take a moment to share your thoughts by using the thumbs-up/thumbs-down icons at the bottom of each response (it only takes a minute). Your feedback plays a key role in improving the service.

1. When the feedback form opens, add your comments about what worked well or what didn't in the text field. 
    > [!Important]
    > Include the hashtag **#VeevaGC** in your feedback.
3. If applicable, add a screenshot.
4. Select **YES** to share your data with Microsoft, and choose **Submit**.

## Help and support

For help and support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
