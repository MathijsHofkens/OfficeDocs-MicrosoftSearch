---
title: "Microsoft 365 Copilot Connectors FAQ"
ms.author: gladysa
author: gladysaj
manager: brian.j
ms.audience: Admin
ms.topic: reference
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 07/15/2025
description: "Find answers to frequently asked questions about Copilot connectors."
---

# Microsoft 365 Copilot connectors FAQ

Microsoft 365 Copilot connectors increase the discoverability of and engagement with your enterprise data by integrating your data into the Microsoft 365 Copilot experience. With Copilot connectors, you can make the most of your external data for functions like enriched data analysis to allow Copilot to access and summarize diverse datasets from different sources and provide more comprehensive insights.
For more information, see [Microsoft 365 Copilot connectors overview](/graph/connecting-external-content-connectors-overview).

This article provides answers to frequently asked questions related to Copilot connectors.

## General questions

### How do I set up a Microsoft 365 Copilot connector?

To set up a Copilot connector:

1. Create a connection.
2. Register your schema.
3. Ingest your content into Microsoft Graph. Each item is sent with properties that match the schema you registered to power your content as discoverable in Microsoft 365 Copilot app.

For more information, see [Set up Microsoft 365 Copilot connectors in the Microsoft 365 admin center](/microsoftsearch/configure-connector).

### Can I edit the query string after the connection is published?

Currently, editing the query string after the connection is published isn't supported. You need to create a new connection. 

> [!NOTE]
> Query strings are available for ServiceNow Knowledge, ServiceNow Catalog, Confluence Cloud.

### How do Copilot connectors work Microsoft 365 Copilot?

Copilot connectors allow external content to be stored in Microsoft Graph, which provides a way to surface external content in various Microsoft 365 experiences. This integration allows for Microsoft 365 Copilot to access and summarize your diverse datasets from different sources, enhancing the ways your users are already searching for answers.

For more information, see [Build Copilot connectors for Microsoft Copilot for Microsoft 365](/microsoft-365-copilot/extensibility/overview-graph-connector).

### Is my data secure when I use connectors?

When you use connectors to bring your content into Microsoft 365, your security and data access controls are maintained. You map existing access control lists to objects in Microsoft 365 and Microsoft Entra ID to ensure that only individuals with the right permissions can access the content.

### Where is the data stored when it is ingested?

When data enters the Microsoft cloud through the Copilot connectors platform, it is stored in the region where your Microsoft 365 tenant is located. For more information, see [Where your Microsoft 365 customer data is stored](/microsoft-365/enterprise/o365-data-locations).

### Is the data ingested into Microsoft Graph encrypted? What encryption algorithm is used?

Data ingested via Copilot connectors encrypted as follows:

- **Data at rest (in customer's master store)** - Encrypted using DEK (Data Encryption Key) & KEK (Key Encryption Key) supplied to the partner. 
- **Data in transit** - Secure tunnel. 
- **Data at rest (in Microsoft 365)** - Encrypted using Microsoft 365 encryption key by default (you can provide your own encryption key). 

For more information, see [Encryption in the Microsoft cloud](/purview/office-365-encryption-in-the-microsoft-cloud-overview). 

### If data is encrypted, does Microsoft have access to the encryption keys?

Microsoft does not have (or need) access to partner encryption keys. Content in the Microsoft cloud is encrypted using Microsoft 365 encryption keys by default. You can provide your own encryption key. For more information, see [Service encryption with customer key](/purview/customer-key-overview).

### How long are copies of the data retained?

Content is retained in adherence to the general Microsoft 365 data retention period. For more information, see [Data retention, deletion, and destruction in Microsoft 365](/compliance/assurance/assurance-data-retention-deletion-and-destruction-overview).

### What are the best practices for testing a connection?

Apply the following best practices when you test a connection:

- Create users in the test environment for ACL testing.
- Make sure you're using the right credentials to test the tenant.
- Make sure that users are assigned to the test tenant for staged rollouts and test for only those users.
- Use the [Index browser](/microsoftsearch/configure-connector) to verify that an item is indexed.

## Prebuilt and custom Copilot connectors questions

### What are prebuilt Copilot connectors?

Prebuilt connectors are connectors that Microsoft and partner organizations provide that allow you to integrate third-party content sources like Salesforce, ServiceNow, Confluence, and more into Microsoft 365. These connectors help you bring external data into Microsoft 365. For more information, see [Copilot connectors gallery](/microsoftsearch/connectors-gallery).

### What are the benefits of using prebuilt Copilot connectors?

Prebuilt Copilot connectors provide the following benefits:

- **Simplified integration** - Prebuilt connectors reduce the time and effort required to integrate external data sources. 
- **Enhanced searchability** - By bringing external data into Microsoft 365, prebuilt Copilot connectors make it easier for users to search and access this information.
- **Improved productivity** - Users can access all relevant information from within Microsoft 365, reducing the need to switch between different applications and platforms.

### What are custom Copilot connectors?

Custom connectors allow you to integrate your own data sources into Microsoft Graph to bring external data into Microsoft 365 experiences. For more information, see [Microsoft 365 Copilot connectors overview](/graph/connecting-external-content-connectors-overview).

### How do I build a custom Copilot connector?

You can use the [Microsoft 365 Agents Toolkit](/microsoft-365-copilot/extensibility/build-your-first-connector) or the [Copilot connectors SDK](/graph/custom-connector-sdk-sample-overview) to build a custom Copilot connector.

### What are the prerequisites for creating a custom connector?

To create a custom connector, you need a Microsoft work or school account with the Global administrator role, and access to a Microsoft 365 tenant. If you don't have a Microsoft 365 tenant, you might qualify for one through the [Microsoft 365 Developer Program.](/office/developer-program/microsoft-365-developer-program).

### What is the difference between full crawl and an incremental crawl?

A full crawl:

- Crawls the entire data source.
- Updates the index with all items.
- Reflects any deletions from the data source in the index.
- Updates the permissions.  

An incremental crawl:

- Only updates items that changed since the last crawl.
- Doesn't handle deletions, so items removed from the data source remain in the index. 
- Incremental crawls do not currently support processing of updates to permissions. 

For more information about crawl schedules and refresh settings, see [Crawl scheduling](/microsoftsearch/configure-connector#crawl-scheduling).

### Why aren't results displayed in Microsoft Search?

Results might not be displayed in Microsoft Search after a Copilot connector is configured for several reasons:

- **Indexing delays** - Sometimes, it takes a while for the data to be indexed and displayed in search results. It can vary based on the volume of data and the complexity of the data source.
- **All vertical setting** - Make sure that **include results in All vertical** is enabled. This setting should be enabled by default for prebuilt Copilot connectors. For custom connectors, the setting must be enabled. 
- **Permissions issues** - Make sure that the correct permissions are set for the data source. If the permissions are not configured correctly, the data might not be accessible for indexing.
- **Configuration errors** - Double-check the configuration settings of the Copilot connector. Any misconfiguration can lead to issues with data indexing and search results.
- **Staged rollout** - If you're using a [staged rollout](/microsoftsearch/staged-rollout-for-graph-connectors), validate which users are in the staged rollout. 
- **Supported file types and sizes** - Verify that the file types and sizes are supported by the connector. Unsupported file types or sizes might not be indexed.
- **Custom verticals** - Create a custom vertical for each data source to help with troubleshooting and ensure that the data is indexed correctly.

## Copilot Search data source filter questions

### How are connector names and icons generated in the data source filter?

Prebuilt connectors display standard connector names and icons as data sources. For custom connectors built with the [Copilot connectors SDK](/graph/custom-connector-sdk-sample-overview), the connection name and icon that the developer supplies is displayed as the data source. For custom connectors built with the [Connectors API](/graph/connecting-external-content-connectors-api-overview), a default connection name and icon are displayed as the data source.

### How can I change the name of a custom connector built with the SDK?

To change the display name or description for a custom connector built with the [Connectors API](/graph/connecting-external-content-connectors-api-overview), see [Update externalConnection](/graph/api/externalconnectors-externalconnection-update).

If you're using the [Copilot connectors SDK](/graph/custom-connector-sdk-sample-overview) to build your custom connectors, be sure to set the name that you want when you [publish your connector](/graph/custom-connector-sdk-sample-publish).

## Copilot Search results page questions

### Why do Copilot Search and Workplace Search show different search result layouts?

Adaptive Card layouts aren't supported in Copilot Search; instead, semantic labels are used to generate the result layout. To make sure that key elements such as title and URL are represented accurately in the results, apply semantic label mappings to the fields.

### Which icons are shown as part of search results for connector data? 

When the search result shows connector data, the connector icon is displayed. If a connector icon isn't available, the data source icon is displayed.

### How is activity information updated in search results?

The activity information is determined by the most recent activity information associated with the **LastModifiedBy** label; for example, "Modified by Adam 4 hours ago."

> [!NOTE]
> Activity information isn't available for the Azure DevOps and ServiceNow connectors.

### How do I change the value of the LastModifiedBy label?

To update the **LastModifiedBy** label:

- Determine which property you can to use for **LastModifiedBy/DateTime**. 
- Update the logic to adjust the value that you want to show; for example: empty if not available, same as created, some static value, last crawl time, actual modified time.
- Use the [update schema API](/graph/api/externalconnectors-externalconnection-patch-schema) to map the label to the right property.
- Use the [update externalConnection API](/graph/api/externalconnectors-externalconnection-update) to update all items.

### How are type filter values generated?

The type filter is populated with default values for the most common Copilot connectors, such as Confluence, Google Drive, and Jira.

## Microsoft Graph Connector Agent questions

### How does the Microsoft Graph Connector agent interact with its system, and where is the indexed data stored?

The agent is installed on-premises and needs access to the data source. When the account is authorized, the agent crawls the data and communicates with the Microsoft 365 Copilot connector services to push data to the index. The data indexed through Microsoft 365 Copilot connectors is in the same location.

### Where should the Microsoft Graph Connector Agent be installed?

Install the agent on a computer on the same network as the data source. It doesn't have to be installed on the same computer that hosts the data source. The data source URL must be accessible to the Microsoft Graph Connector Agent.

### Why does the Microsoft Graph Connector Agent require the ExternalConnection.ReadWrite.OwnedBy permission?

The `ExternalConnection.ReadWrite.OwnedBy` permission allows the agent to read and write external connection settings on behalf of the admin, but it can't access or modify anything beyond its granted permissions.

### Can the Microsoft Graph Connector Agent be installed on multiple servers, and does the service run on both?

You can install the Microsoft Graph Connector Agent on multiple computers, for multiple connections. One agent can handle multiple connections. The crawl performance depends on the number of connections used, crawl frequency, and number of items. We recommend using no more than three connections per agent.

## Related content

- [Connectors overview](/microsoftsearch/connectors-overview)
- [Connectors gallery](/microsoftsearch/connectors-gallery)
- [Copilot Search overview](/microsoftsearch/overview-copilot-search)