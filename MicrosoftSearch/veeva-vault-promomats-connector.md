--- 

title: "Veeva Vault PromoMats Microsoft 365 Copilot connector" 
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
description: "Set up the Veeva Vault PromoMats Microsoft 365 Copilot connector." 
ms.date: 02/26/2025
---
# Veeva Vault PromoMats Microsoft 365 Copilot connector (preview)

The Veeva Vault PromoMats Microsoft 365 Copilot connector allows organizations to index promotional marketing materials from Veeva Vault into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot.

The connector integrates Vault PromoMats' built-in permission model, ensuring that users only access authorized content, and supports faster content generation and review through content analysis and preparation. By enhancing efficiency throughout the content lifecycle, it helps maintain brand consistency. This functionality is beneficial for marketing, medical affairs, and regulatory teams, enabling informed decision-making and reducing the time-to-market for promotional materials.

The following are the key benefits of the Veeva Vault PromoMats Copilot connector:

- **Enhanced content management and retrieval:** The connector suggests tags to organize and access relevant documents more easily.
- **AI-assisted content reuse and localization:** Facilitates content adaptation for various markets, saving time while ensuring relevance for different audiences.
- **Comprehensive document review and summarization:** AI tools help grammar, spelling, semantics, and regulatory compliance, ensuring accuracy and up-to-date promotional materials.

Additionally, the connector boosts productivity by minimizing time spent searching for information across multiple sources. By integrating Microsoft 365 Copilot and Microsoft Search with PromoMats data, it streamlines content preparation and field use. It also improves efficiency by referencing existing compliant documents and content to help generate new messaging and prepare materials effectively.

This guide is for Microsoft 365 administrators or anyone responsible for configuring, managing, and monitoring the Veeva Vault PromoMats Copilot connector.

## Capabilities

The Veeva Vault PromoMats Copilot connector enables the following capabilities:

- Generates summaries to understand and make decisions based on promotional materials and key documents.
- Improves the searchability of promotional documents by using advanced Microsoft 365 search capabilities.
- Gains insights and recommendations from indexed data to enhance workflow efficiency, including checking the usage of specific phrases in PromoMats documents.
- Indexes PromoMats content to create a unified search experience across Microsoft 365 environments.
- Maintains data privacy and compliance by supporting ACL permissions and document-level permissions, simplifying the permission model and reducing the risk of misconfiguration.
- Uses query string conditions to precisely control the synchronization of articles, ensuring efficient indexing.

The following table lists example prompts that show how Microsoft 365 Copilot, integrated with the Veeva PromoMats Copilot connector, can significantly enhance productivity and streamline processes by using PromoMats data.

|Scenario|Example prompt|
|:---|:---|
|Content generation|Generate personalized content for customer interactions based on the latest research documents stored in PromoMats.|
|Content tagging|Suggest tags that can be used with the selected promotional contents to make it easier to manage and retrieve going forward.|
| HTML email generation|Create HTML emails generated automatically from pre-provided HTML templates and documents stored in PromoMats.|
|Pre-call planning|Summarize relevant information and prepare materials for sales representatives before customer meetings.|
|AI-assisted content re-use|Identify appropriate tags, translation, and localization to improve the reuse of content. |
|Content consistency|Create new promotional materials, ensuring consistency with existing content.|
|Pre-MLR AI-assisted reviews|Review grammar, spelling, and semantics and cross-validate the following promotional documents.|
|Document summarization|Summarize key points from regulatory documents to ensure all team members are informed of the latest compliance requirements.|
|Meeting preparation|Prepare a script for an upcoming meeting based on recent customer email threads and PromoMats documents.|
|Support claim process|Find claims that can be reused made about the efficacy of drugs to ensure they are medically and legally validated and approved.|

## Limitations

- Indexes only the latest versions of documents.
- Supports file types including Microsoft Office documents, PDFs, and text-based files only; doesn't support PNG, JPG, or video files.
- Partially indexes files larger than 4 MB.

## Prerequisites

To configure Microsoft Entra ID OAuth 2.0/OpenID Connect for the Veeva Vault Copilot connector, follow these steps.

### Register an application in Microsoft Entra ID

1. Go to **Microsoft Entra admin center** > **Applications** > **App registrations** > **New registration**. 
1. In the creation form, fill out the name as your preference.
1. In the Supported account types, choose **Accounts in this organizational directory only**.
1. In the redirect URI, select **Web**, and add the following links to the **Redirect URI** field:

   - For **Microsoft 365 Enterprise**, copy and paste:
     `https://gcs.office.com/v1.0/admin/oauth/callback`
   - For **Microsoft 365 Government**, copy and paste:
     `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

1. Under **Certificates & Secrets**, generate a client secret and store it securely.

### Configure OAuth in Veeva Vault

1. Create a new profile.
   1. Go to **Admin** > **Settings** > **OAuth 2.0 / OpenID Connect Profiles**.
   2. Fill out the label, name, and description as your preference.
   3. Set **Status** as active.
   4. In **Authorization Server Provider**, select **Azure AD**.
   5. Click **Upload AS metadata** and select **Provide Authorization Server Metadata URL**.
   6. Use the link below, replace {tenant-id} with your tenant ID, and paste it into the field.
      `https://login.microsoftonline.com/{tenant-id}/v2.0/.well-known/openid-configuration`
   7. Select **Identity is in another claim** and enter the **upn** of the claim.
   8. In **User ID Type**, select **Federated ID**, and uncheck **Perform Strict Audience Restriction validation**.

   > [!NOTE]
   > Make sure your upn is the same as your federated ID.


2. In the newly created profile page, click **Client Applications** > **Add**. 
Use the **Client ID** from the newly created application in the Entra admin center.
   > [!NOTE]
   > If you would like to enable the flag **Perform strict Audience Restriction validation**, add the Client ID value in the **Audience** field.

4. Create security policies.
   1. Go to **Admin** > **Settings** > **Security Policies**.
   2. Click **Create** > **Single sign-on**.
   3. Fill out the name and description as your preference.
   4. In status, choose **active**.
   5. In authentication type, choose **Single Sign-on**
   6. In Single Sign-on Profile, choose a profile created based on single sign-on. For more information, see [Veeva Vault documentation](https://platform.veevavault.help/en/gr/13977/).
   7. In eSignature Profile, select **None**.
   8. In the OAuth 2.0 / OpenID Connect Profile, select the newly created OAuth 2.0 profile.

   For the rest of the settings, keep the default values.

5. Link user with the security policy.
   1. Go to **Admin** > **Users & Groups**.
   2. Select a user who is the vault owner.
   3. Click **Edit**.
   4. In **Details** > **Security Policy**, change the values to the newly created policy.
   5. In **Federated ID**, change it to the UPN claim of the admin identity, which is also used in the connector setup. 

## Get started

### Configure display name
Provide a meaningful display name for your connector in the Microsoft 365 Admin Center. This name helps identify the connection in your workspace.

### Add the Veeva Vault URL
Enter the URL of your Veeva Vault instance. For example: `https://<your-vault-domain>.veevavault.com`.

### Provide authentication details

To configure the Veeva Vault PromoMats Copilot connector, select **Azure Active Directory (OIDC)** and fill in the following information:

- **Vault session ID URL:** You can find the session ID URL on the Veeva Vault interface under the path: **Admin panel** > **Settings** > **OAuth 2.0/ OpenID Connect Profiles** > the profile that's created for the connection > **Vault Session ID URL**.
- **Client ID:** The application ID for your Entra application registered for Veeva Vault. 
- **Client secret:** The client secret associated with the Entra application. Make sure that it is securely stored and accessible only to authorized personnel. 
 
> [!Important]
> Configure both Microsoft Entra ID and Veeva Vault admin settings to enable Microsoft Entra ID authentication.

### Set up identity mapping

For customers who need the security settings of their Veeva PromoMats instance to be honored, click **Custom setup** > **User**. In **Map identities**, select **Non-ME-ID** as the identity type for your content source.

Enter the required information for identity mapping. For example, if you want to map identities based on email addresses, you can follow these steps.

1. Select **Mail** as the **Microsoft Entra user property**.
2. Select **Email** as the **non-Microsoft Entra user property**.
3. Use a regular expression such as `([^@]+)` to capture a sequence of one or more characters that are not the `@` symbol.
4. Create a formula to complete the mapping, such as `{0}@<your-domain>`.

This process ensures that user identity mappings are correctly established and security permissions are properly enforced.

### 5. Roll out to limited audience
Deploy this connection to a limited group of users to validate indexing and access control functionality before a full rollout. 


## Default settings

The following table lists the default settings for the Veeva Vault PromoMats Copilot connector. To modify these default values, choose **Custom setup** during the configuration.

| Section  | Setting               | Default value |
|----------|-----------------------|---------------|
| **Users**   | Access permissions   | Respects Veeva Vault permissions; only viewable documents are accessible. |
| **Content** | Index metadata       | Indexes key metadata, such as document name, owner, and lifecycle stage. |
| **Content** | Manage properties    | Enables metadata like title, created by, and last modified by. |
| **Sync**    | Full crawls          | Every day.|
| **Sync**  | Full crawl frequency|Every day.|

## Custom setup

### Users

#### Access permissions

The connector adheres to the ACLs defined in Veeva Vault. Only users with view permissions in Veeva Vault can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, although this isn't recommended.

### Sync

#### Adjust sync schedules

You can modify the frequency of full crawls to fit your organization's requirements. The following are the default crawls:

- Incremental crawl - 15 minutes.
- Full crawl - daily.

## Troubleshooting

For information about troubleshooting, see [Troubleshooting the Veeva Vault Copilot connector](troubleshoot-veeva-vault-connectors.md).

## Next steps

After you configure and publish the connector, monitor its status on **Data sources** in the [Admin Center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/graph/support). 
