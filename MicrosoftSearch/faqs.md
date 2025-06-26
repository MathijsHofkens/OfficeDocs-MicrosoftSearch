---
title: "Microsoft Search FAQs"
ms.author: bstucker
author: bstuck
manager: bstucker
ms.audience: Admin
ms.topic: reference
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 03/15/2022
search.appverid:
- BFB160
- MET150
- MOE150
description: "Get answers to commonly asked questions about Microsoft 365 enterprise and Microsoft Search"
---
# Microsoft Search FAQs

Here's a list of the most common questions.

> [!TIP]
> Don't see your question answered here? Ask your question in this article's feedback.

> [!IMPORTANT]
> As of March 31, 2025, M365.cloud.microsoft (formerly Office.com and Microsoft365.com) and SharePoint Online are the new homes for Microsoft Search. Microsoft Search in Bing is no longer available. We encourage Microsoft Search in Bing users to update your bookmarks. [Learn more](/microsoftsearch/retirement-microsoft-search-bing). 

## Is advanced query understanding supported?

Yes, Microsoft Search parses query intent from larger phrases. This feature uses AI to learn common superfluous phrases users add to their queries that don't affect their search intent. For example, when a user searches for *tell me more about how to change my password*, we extract the less important words from the query and trigger based on the relevant ones like *change password*.
  
This feature won't override keywords set in the [Microsoft 365 admin center](https://admin.microsoft.com).
  
## Can you search for files on-premises?

Yes. You can search on-premises [SharePoint](https://sharepoint.com/) files if you have a hybrid deployment of SharePoint.
  
## How do I make Bing the default search engine for people in my org?

These are the instructions for setting the default search engine, default homepage, and default browser to give your users the best experience with Microsoft Search in [Bing](https://Bing.com):

- [Set Microsoft Edge as your default browser](/deployedge/edge-default-browser)
- [Make Bing your default search engine](set-default-search-engine.md)
- [Set Bing.com as your enterprise homepage](set-default-homepage.md)
 

## How are my search results protected?

We require [Microsoft Entra ID](/azure/active-directory/) authentication to access results from the Trusted Cloud. Authenticated users only see content they have access to.

## Filename vs. Title in search results

Unlike the classic search experience in SharePoint which prefers the `Title` property of a file, search results in Microsoft Search display the filename for files, similar to the default view in SharePoint or OneDrive libraries. This approach avoids showing the `Title` property, which can often be misleading when it carries over from copied documents or from document templates. However, for sites, pages and list items, the `Title` property is shown.

Text in the `Title` property is still indexed and searchable, and can be used in the hit highlighting of a search results if decided by the search engine.

## Can I search across federated organizations?

No.

## Where can I get info about Office 365 security, compliance, and privacy?

Details can be found on the [Trust Center pages for Office 365](https://www.microsoft.com/TrustCenter/CloudServices/office365/default.aspx).

## Can guests access Microsoft Search in my organization?

Microsoft 365 enables rich collaboration with people outside of your organization through [guest access.](/microsoft-365/solutions/collaborate-with-people-outside-your-organization) These users can search for documents, sites, groups, lists, and libraries. However, guests won't get the full, personalized Microsoft Search experience and may need to use the on-page search box instead of the unified Microsoft Search box in the header.

## What does Microsoft Search cost?

Microsoft Search is the search for your Microsoft 365 experience; there is no additional cost to search your data. Some features like [Microsoft 365 Copilot connectors](connectors-overview.md) come with quotas that are included on certain [licenses and have extra quota available for purchase](licensing.md).
