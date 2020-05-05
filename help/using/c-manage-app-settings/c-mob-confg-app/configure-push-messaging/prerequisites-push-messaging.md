---
description: You must complete these tasks before configuring Push Messaging in applications.
keywords: mobile
seo-description: You must complete these tasks before configuring Push Messaging in applications.
seo-title: Prerequisites to Enable Push Messaging
solution: Marketing Cloud,Analytics
title: Prerequisites to Enable Push Messaging
topic: Metrics
uuid: 194e6e07-b794-4152-a838-a4125c3292d4
---

# Prerequisites to enable push messaging {#prerequisites-to-enable-push-messaging}

You must complete these tasks before configuring push messaging in your applications.

## Enable the Experience Cloud for your company

Your Adobe Analytics Company must be Experience Cloud enabled. You can verify the status your Adobe account executive.

## Install and configure the Mobile SDK

* **Install the Mobile SDK**

    To configure push messaging, you must download and install at least version 4.6 or later of the Mobile SDK. For more information, see [Download the SDKs](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-analytics/download-sdk.md).

* **Configure push services**

    You must configure push services in the Mobile SDK.
    For more information, see the following content:

    * [Push Messaging in Android](/help/android/messaging-main/push-messaging/push-messaging.md)
    * [Push Messaging in iOS](/help/ios/messaging-main/push-messaging/push-messaging.md)

## Log in to the Mobile Core Service using your Adobe ID

>[!IMPORTANT]
>
>To use the Push Services functionality users must log in to the Mobile Core Service by using their Adobe ID and their Analytics account must be linked to their Adobe IDs. Push Services functionality is not available if users log in using their existing Adobe Analytics accounts.

If users do not have Adobe IDs, complete the following steps:

1. (**Experience Cloud Administrator**) Invite users to the Experience Cloud.

1. (**User**) Create a personal Adobe ID using the instructions that you received from the Experience Cloud administrator.

    An email message is automatically sent to each user after the administrator completes the previous step.

1. (**Users**) Log in to Mobile using their Adobe ID.

## Link users' accounts in the Experience Cloud

Each user must link the Analytics solution account from the Experience Cloud organization.

1. To sign in to the Experience Cloud with an Adobe ID, type [https://marketing.adobe.com](https://marketing.adobe.com) in a browser.

1. In the upper right corner, select the Analytics company name.

1. Click **[!UICONTROL Add Organization]** and select **[!UICONTROL Adobe SiteCatalyst/Adobe Social]** from the drop-down list.

1. Type the company name, your legacy credentials for the specified company, and click **[!UICONTROL Link Account]**.

    The Adobe ID is now linked to your Analytics account, company, and log-in credentials.

For more information, see [Troubleshooting Account Linking](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html).

## Configure push services and the SDK ID service in the Mobile User Interface

Before you enable the ID service for your app, the **[!UICONTROL Push Services]** section is disabled. But, after you enable the ID service, the Push Services section is enabled. For more information about enabling push services, see [Configure SDK ID service options](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-visitor.md).

>[!IMPORTANT]: You must click **[!UICONTROL Save]** to save your changes and refresh the Push Services.
>
>You can configure one app store app for Apple and one for Google in each report suite. If you need additional apps, for example, one for a production environment and one for a dev environment, set up a new app store app and a new report suite for each environment.

* For **Apple**, drag and drop your private key and/or certificate. If your private key is password-encrypted, type its password.

  * For the **Private Key**, drag and drop your private-key file into the box. 
  
    You can also click **[!UICONTROL Browse]** to select the file. This file contains the private key. The certificate might also be included in this file (`.p12`, `pkcs12`, `.pfx`, `.key`, `.pem`).

  * For the **Private Key Password**, if your private-key file is encrypted, type the password.

    (Conditional) For the **Certificate**, drag and drop your certificate file into the box. You can also click **[!UICONTROL Browse]** to select the file. This field is not required if the private-key file also contains the certificate ( `.cert`, `.cer`, `.crt`, `.pem`).

* For **Google**, specify the API key for the app.

    Click **[!UICONTROL Test]** to validate that the app and Mobile Services are configured correctly. This option is useful for debugging and troubleshooting.

    Type the device's push tokens that you want to send the message. You can send the message to multiple devices by specifying tokens in a comma-separated list.

    ![push test message](assets/push_test_list.png)
