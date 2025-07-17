---
ms.date: 10/02/2019
title: "Microsoft 365 Copilot connectors overview for Microsoft Search and Microsoft 365 Copilot"
ms.author: mecampos
author: mecampos
manager: lsheppard
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: "Learn how your organization can use Microsoft 365 Copilot connectors to index third-party data so that it appears in Microsoft Search and Microsoft 365 Copilot results."
---

# Microsoft 365 Copilot connectors overview for Microsoft Search

Microsoft Search indexes all your [Microsoft 365](https://www.microsoft.com/microsoft-365) data to make it searchable for users. With Microsoft 365 Copilot connectors, your organization can index third-party data, ensuring it appears in Microsoft Search and Microsoft 365 Copilot results. This feature enhances the range of content sources searchable within your Microsoft 365 productivity apps and the broader Microsoft ecosystem. The third-party data can be hosted on-premises or in the public or private clouds. Microsoft 365 Copilot connectors respect the source permissions configured in your content source. As a result, users can only access content for which they have appropriate permissions

> [!NOTE]
> For details about how to build a Microsoft 365 Copilot connector that is integrated with Microsoft 365 Copilot, see [Microsoft 365 Copilot for Microsoft 365 Copilot connectors](/microsoft-365-copilot/extensibility/overview-graph-connector).

The following video provides an overview of the Microsoft 365 Copilot connectors setup process for the Microsoft Search experience.

> [!VIDEO 4f4668c6-445a-4895-8627-92880eafad68]

## Connector architecture

The following architectural diagram of the Microsoft Graph platform shows how Microsoft 365 Copilot connector content flows through content indexing to user results in [Microsoft Search](./overview-microsoft-search.md) clients. The rest of this section explains each of the key building blocks in the diagram.

![Diagram: on-premises and cloud-based data is pulled by connectors and indexed by the Microsoft Search API, and then the Microsoft Search service delivers the results to users.](media/connectors-overview/highlevel-connectors.png)
Microsoft 365 Copilot connectors can pull data from cloud-based (SaaS) data sources and on-premises data stores. The above diagram shows connections to only two data sources, but you can add connections to up to ten sources per tenant.

The Microsoft 365 Copilot connectors API instantiates one connection per data source. Then, the API indexes and stores the data. Established connections interact with Microsoft Search and Microsoft 365 Copilot so that users can get search results.

You can use the Microsoft 365 [admin center](https://admin.microsoft.com) to set up and manage any of the Microsoft 365 Copilot connectors. The admin center has a simple user interface that makes it easy to establish a connection to your data source and monitor connection status and utilization.

To create a **connection** to a data source, admins need authenticated access to the data and the entire content repository. The data is fed to the Microsoft 365 Copilot connector service for indexing.

## Data sources

Microsoft provides more than 30 Microsoft 365 Copilot connectors, and our ecosystem partners have created over 100 more connectors. You can also build your own connector.

### Microsoft-built Copilot connectors

You can connect to the many popular data sources using connectors created by Microsoft.

The [Microsoft 365 Copilot connectors gallery](connectors-gallery.md) contains a brief description of each of these connectors. If you're ready to connect one of these data sources to your tenant, be sure to read the [Setup overview](configure-connector.md) and any other articles in the setup connectors by Microsoft section that apply to your data source.

### Copilot connectors for people data

[Microsoft 365 Copilot connectors for people data](/graph/peopleconnectors) integrate third-party people data into Microsoft 365 applications to enhance and unify individual profiles. They provide a synchronized view of people data while keeping the original data authoritative in its source system. These connectors improve identity cohesion, Copilot’s response relevance, and data discoverability within M365, including updated profile cards and search capabilities. For more information, see [Microsoft 365 Copilot connectors for people data](/graph/peopleconnectors). 

### Partner-built Copilot connectors

The [Microsoft 365 Copilot connectors gallery](connectors-gallery.md) includes a brief description of each of the connectors created by our partners and a link to each partner's website. To learn more, contact each partner directly.

### Custom Copilot connectors

You can build your own custom connectors to ingest your business data. For more information, see [Microsoft 365 Copilot connectors overview](/graph/connecting-external-content-connectors-overview). See also the following get started topics:

- [Microsoft 365 Agents Toolkit](/microsoft-365-copilot/extensibility/build-your-first-connector)
- [Copilot connectors SDK](/graph/custom-connector-sdk-sample-overview)

## Connection management

You can manage your connections on the [connectors tab](https://admin.microsoft.com/#/copilot/connectors) in the [Microsoft 365 admin center](https://admin.microsoft.com/). For more information about managing connections, see [Monitor your connections](manage-connector.md).

## Limitations

The following limitations apply to Copilot connectors:

* When you publish a Copilot connector, it can take a few minutes for the connection to be created. During that time, the connection shows its status as `Publishing`.

* Limited editing capabilities are supported after a connection is published. If you need to change any details that aren't editable, you have to delete and recreate the connection.

## License requirements

For users in your organization to view data from connectors in their search results, you need a valid Microsoft 365 or Office 365 license.

To learn more, see [License requirements and pricing](licensing.md) and [Terms of use](terms-of-use.md).

## Search result configuration and customization

You can customize and configure search results in several ways. To learn more, see the following articles:

* [Manage search verticals](manage-verticals.md) and [result types](manage-result-types.md)
* [Manage connector results in All vertical](connectors-in-all-vertical.md)
* [Manage search result layouts](customize-results-layout.md)
* [Manage result cluster](result-cluster.md)
* [Manage custom filters](custom-filters.md)

## Custom applications

After custom data is indexed, developers can [query this data](/graph/search-concept-custom-types). You can view your data in any application. For more information, see the [Overview of the Microsoft Search API in Microsoft Graph](/graph/search-concept-overview).

## Copilot connectors for Copilot Search

Microsoft 365 Copilot Search is a powerful, AI-powered enterprise search experience that acts as a universal search layer that integrates into the Microsoft 365 Copilot app. Copilot connectors enhance the Copilot Search experience by enabling seamless integration of data from external services into Microsoft Graph to make it available in the search experience. For more information, see [Copilot Search overview](./overview-microsoft-search.md).

## Related content

- [Microsoft Search overview](overview-microsoft-search.md)
- [Microsoft 365 Copilot connectors gallery](connectors-gallery.md)
