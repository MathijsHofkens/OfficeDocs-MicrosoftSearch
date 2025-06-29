---
title: "Guidance for retiring Microsoft Search in Bing for your organization"
ms.author: davidedwards
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: "Guidance for retirement of Microsoft Search in Bing."
ms.date: 01/17/2025
---

# Guidance for retiring Microsoft Search in Bing for your organization

As of March 31, 2025, work and school search through Bing.com is retired. This change is being made as Microsoft streamlines search experiences to focus on enhancing core productivity tools.

While Microsoft Search is no longer available on Bing, the core Microsoft Search experience remains accessible through M365.cloud.microsoft (formerly Office.com and Microsoft365.com) and SharePoint Online. Users can also still find people in their organization, files, and SharePoint sites using the Edge for Business address bar and Windows search box. Each of these entry points routes them to a Microsoft Search experience.

These changes also apply to users in organizations with education service plans that use Bing's experience designed for searching school. Some school search features, including answers about classes and upcoming assignments, are discontinued.

## What's changing? 

Users can find work and school search results on M365.cloud.microsoft and SharePoint Online rather than on Bing.com. Likewise, the Microsoft Edge for Business address bar and the Microsoft search box send users to work and school results on M365.cloud.microsoft rather than Bing.com. Bing's dedicated pages for work results (the "Work" tab) and school results (the "School" tab) are retired, so M365.cloud.microsoft and SharePoint Online are the new homes for Microsoft Search. Search boxes that IT admins configured to point to Microsoft Search in Bing no longer provide work results. People who go directly to or have bookmarks for www.bing.com/work are sent to M365.cloud.microsoft through June 30, 2025.

Some Microsoft Search answers are no longer available, including floor plans, Q&As and location answers. Recommended bookmarks are also retired—you can keep them by manually publishing or exporting them by April 30, 2025.

> [!NOTE]
> The Google Chrome browser extension that sets Bing as the default search engine is also retired as of March 31, 2025. Users of Google Chrome, Microsoft Edge, and other browsers can still select their default search engine in the browser settings. [Learn how to change your default search engine](https://support.microsoft.com/en-us/microsoft-edge/change-your-default-search-engine-f863c519-5994-a8ed-6859-00fbc123b782).

## When and where did these changes take place? 

Microsoft Search in Bing is retired in all regions worldwide as of March 31, 2025. It's retired on all devices, including mobile.

## Where can users search for work and school answers? 

M365.cloud.microsoft (formerly Office.com and Microsoft365.com) and SharePoint Online are the new homes for Microsoft Search. Users of Bing.com in Edge may see a banner redirecting them to M365.cloud.microsoft if their search terms indicate a high likelihood of being work-related. The address bar in Edge for Business and the Windows search box also continue to deliver work and school search results, with some adjustments detailed here: 

## Edge address bar

> [!NOTE]
> Microsoft Edge version 134.0.3124.51+ is required for the work search functionality described on this page.

After March 31, 2025, the Microsoft Edge for Business address bar sends users to work results on M365.cloud.microsoft rather than Bing.com. Users of the address bar can continue to find work-related documents, bookmarks, and people in suggested results—clicking on these suggestions takes users to work results on M365.cloud.microsoft. Users can also type "work" in the address bar, hit the tab key, then type in their work-related query to get work results on a M365.cloud.microsoft page. Work search results continue to include documents, people, and bookmarks.

See how it works:
 > [!VIDEO fc86ae5a-1aa7-4b5a-8710-0e1d264cbbbd]

## Changes to the Edge address bar policy

The *AddressBarMicrosoftSearchInBingProviderEnabled* policy, used to configure Microsoft Search in Bing results in the Edge for Business address bar, is being retired in May 2025. The new policy to replace it is *AddressBarWorkSearchResultsEnabled*. This policy is now available, allowing admins to configure the display of work suggestions in the address bar. 

## Windows search box

The "Work" scope is being retired in the Windows search box, and there's no longer company-specific branding (the "Commercial Gleam"). However, users can still find work files from both the "All" scope and the "Documents" scope. Additionally, users can find people through the "All" and "People" scopes.

## What actions are required for customers? 

- Help users transition to the Edge for Business address bar, the Windows search box, M365.cloud.microsoft, or SharePoint Online as entry points to Microsoft Search. Customers can add these entry points to favorites or the favorites bar in Edge for Business as a helpful alternative pathway. Admins can easily set favorites in Edge for Business for their organization—[see details here](/deployedge/edge-learnmore-provision-favorites).
- Inform your users how to use the Edge address bar to perform work searches. [Get details here](/MicrosoftSearch/retirement-microsoft-search-bing#edge-address-bar)

## What's happening to the "Work" or "School" tab? 

Users who go to Bing after March 31, and were previously logged in to Bing with their Entra ID account, may continue to see the "Work" or "School" tab. If they click on either of these tabs, they're redirected to m365.cloud.microsoft to complete their search. This experience is based on the user's cookies. So, if a user clears their cookies or gets a new browser or machine, they may no longer see these tabs. Visiting bing.com/work restores the "Work" or "School" tab.

## How do these changes affect users in educational organizations?

Users in organizations with education service plans can search for school resources through m365.cloud.microsoft (formerly Office.com and Microsoft365.com) and SharePoint Online. They can also still find people in their educational institution, files, and SharePoint sites using the Edge for Business address bar and Windows search box. Each of these entry points routes them to a Microsoft Search experience. Some education search features, including answers about classes and upcoming assignments, are discontinued.

## What's happening to SafeSearch? 

If you set the search experience for your organization to "School search," SafeSearch was set to Strict by default. You can ensure that your users continue to have SafeSearch set to Strict after the Microsoft Search in Bing retirement—just map www.bing.com to strict.bing.com at a network level. For more information, see [Blocking adult content with SafeSearch or blocking Chat](https://support.microsoft.com/en-us/topic/blocking-adult-content-with-safesearch-or-blocking-chat-946059ed-992b-46a0-944a-28e8fb8f1814).

## Why is this announcement important?  

Daily productivity can depend on the ability to search for files, people, intranet sites, and more. We understand that the retirement of Microsoft Search in Bing may create some disruption in efficiency. However, users can continue to access Microsoft Search through m365.cloud.microsoft (formerly Office.com and Microsoft365.com) and SharePoint Online., as well as the Edge for Business address bar and Windows search box. 

## Why is this happening?

Customer productivity is our mission and making work search a better experience remains a priority for Microsoft. We hope to better serve you through Microsoft Search in the core productivity experiences of M365.cloud.microsoft and SharePoint Online. We’re also continuing to explore new ways to improve the experience and make work search more discoverable.

## What happens if I linked my Entra ID and Managed Service Account (MSA)?

You may have linked your Entra ID account (work or school account) and your MSA account (personal account) to earn points when you search on Bing, Edge, and MSN. If you linked your accounts, they remain linked. You continue to earn points on Bing, Edge, and MSN if your accounts are linked. When you're on Bing, you need to log in with your MSA account to continue to earn.

If you no longer wish to have your accounts linked, see these [instructions for unlinking your accounts](https://answers.microsoft.com/en-us/microsoftedge/forum/all/how-can-i-unlink-account-linked-to-microsoft-edge/664ab279-8c73-4f68-88ba-cc361d8274ee). 

If you want to redeem your Rewards points, you can do that via the [Rewards dashboard](https://rewards.bing.com/).

Find answers to other questions about [Microsoft Rewards](https://support.microsoft.com/account-billing/getting-personal-rewards-points-for-work-searches-c66effb9-02e6-49c0-89e1-ae4d8644e6f7). 

## Can customers try to opt out of this change? 

No, customers can't opt out of the change. Microsoft Search in Bing is retired in all regions worldwide as of March 31, 2025. It's retired on all devices, including mobile.

## What's happening to bookmarks? 

Editorial bookmarks (bookmarks that an IT admin has curated) continue to work on the other Microsoft Search entry points. These entry points include M365.cloud.microsoft, SharePoint Online, and the Edge for Business address bar.

Microsoft Search no longer recommends bookmarks based on an organization's SharePoint links.

Some organizations set their recommended bookmarks to automatically publish. Automatically published bookmarks, which currently only appear in Microsoft Search in Bing, are no longer visible after March 31. If your organization automatically publishes recommended bookmarks, and you'd like those bookmarks to be visible on other Microsoft Search entry points, you must manually publish them before April 30, 2025. This date is intended to give you a little extra time after the March 31 retirement of Microsoft Search in Bing. You can also export your recommended bookmarks by April 30 if you want to keep them, but don't want to publish them.

Learn more about [managing bookmarks](/microsoftsearch/manage-bookmarks). 

## What's happening to search query history? 

Work or school search history on Bing.com is no longer available as of March 31, 2025. There's no control available for IT admins to download search terms on behalf of users.

## Does this impact all tenants? 

Yes, all tenants who have access to Microsoft Search in Bing are affected.