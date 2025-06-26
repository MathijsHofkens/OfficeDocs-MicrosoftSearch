---
ms.date: 10/08/2019
title: "Troubleshooting guide for ServiceNow Tickets Microsoft 365 Copilot connector"
ms.author: souravpoddar
author: souravpoddar001
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: "Troubleshoot issues with the ServiceNow Tickets Microsoft 365 Copilot connector."
---
# Troubleshooting guide for ServiceNow Tickets Microsoft 365 Copilot connector

## Unable to log in due to single sign-on enabled ServiceNow instance

If your organization has enabled single sign-on (SSO) to ServiceNow, you may have trouble logging in with the service account. You can bring up a username and password-based login by adding <em> `login.do`</em> to the ServiceNow instance URL. Example. `https://<your-organization-domain>.service-now.com./login.do`

## Unauthorized or forbidden response to API request

### Check table access permissions
If you see a forbidden or unauthorized response in connection status, check if the service account has required access to the tables mentioned in [step 3: connection settings](./servicenow-tickets-connector.md#step-3-connection-settings). Check whether all the columns in the tables have read access.

### Change in account password
The ServiceNow Tickets Copilot connector uses an access token fetched on behalf of a service account for crawling. The access token refreshes every 12 hours. Ensure that the service account password isn't changed after publishing the connection. You may need to reauthenticate the connection if there's a change in password.

### Check if the ServiceNow instance behind a firewall
The ServiceNow Tickets  Copilot connector may not be able to reach your ServiceNow instance if it is behind a network firewall. You'll need to explicitly allow access to the connector service. You can find the public IP address range of the connector service in the table below. Based on your tenant region, add it to your ServiceNow instance network allowlist.

**Environment** | **Region** | **Range**
--- | --- | ---
PROD | North America | 52.250.92.252/30, 52.224.250.216/30
PROD | Europe | 20.54.41.208/30, 51.105.159.88/30
PROD | Asia Pacific | 52.139.188.212/30, 20.43.146.44/30

## Access permissions not working as expected

If you observe discrepancies in access permissions applied to search results, verify whether the search user is part of `assigned_to` and `opened_by` fields.

## 4. Issues with *Only people with access to this data source* permission

### User mapping failures

 ServiceNow user accounts that don't have a Microsoft 365 user in Microsoft Entra ID won't map. Non-user, service accounts are expected to fail user mapping. Number of user mapping failures can be accessed in identity stats area in connection detail window. Log of failed user mappings can be downloaded from Error tab.

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
