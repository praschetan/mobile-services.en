---
description: Acquisition links with unique tracking codes can be generated in Adobe Mobile services. When a user downloads and runs an app from the App store after clicking on the generated link, the SDK automatically collects and sends the acquisition data to Adobe Mobile services.
keywords: android;library;mobile;sdk
seo-description: Acquisition links with unique tracking codes can be generated in Adobe Mobile services. When a user downloads and runs an app from the App store after clicking on the generated link, the SDK automatically collects and sends the acquisition data to Adobe Mobile services.
seo-title: Mobile App Acquisition
solution: Marketing Cloud,Analytics
title: Mobile App Acquisition
topic: Developer and implementation
uuid: 4d32eae9-e856-4e40-8a29-2b5bccd106e0
---

# Mobile app acquisition {#mobile-app-acquisition}

Acquisition links with unique tracking codes can be generated in Adobe Mobile services. When a user downloads and runs an app from the App store after clicking on the generated link, the SDK automatically collects and sends the acquisition data to Adobe Mobile services.

## New Adobe Experience Platform Mobile SDK Release

Looking for information and documentation related to the Adobe Experience Platform Mobile SDK? Click [here](https://aep-sdks.gitbook.io/docs/) for our latest documentation.

As of September 2018, we released a new, major version of the SDK. These new Adobe Experience Platform Mobile SDKs are configurable through [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* To get started, go to Adobe Experience Platform Launch.
* To see what is in the Experience Platform SDK repositories, go to [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
>To use Acquisition, you **must** have SDK version 4.1 or later.

Acquisition links must be created in Adobe Mobile services. For more information, see [Acquisition](/help/using/acquisition-main/acquisition-main.md).

**In SDK versions 4.13.1 and later**:

If you cannot use the acquisition links that are created in Adobe Mobile Services, the acquisition data can still be collected and sent by the SDK by using Google Play Acquisition.

To collect acquisition data from a standard Google Play Acquisition campaign:

* Use the standard Google Play Store acquisition method.

  Custom acquisition data can be used with the standard Google Play Acquisition key value pairs. 

* When the user downloads and runs an app as the result of a Google Play store acquisition, the data from the referrer will be collected and sent to Adobe Mobile Services.

  * The data is stored and available in the `AdobeDataCallback` instance that was registered earlier with the SDK.

      For more information, see [Configuration Methods](/help/android/configuration/methods.md). 

  * The `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` or the `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` event type are used.
  
  * Custom keys that were part of the acquisition data from Google Play will be name-spaced with " `a.acquisition.custom.`"

If you are using the Acquisition links that were created on Adobe Mobile Services, add custom data to the acquisition link by completing the following tasks:

1. Prefix an acquisition variable with " `adb`".

   When the SDK receives the acquisition data from Adobe Mobile Services (on first launch), that data will be stored and also available in the `AdobeDataCallback` instance registered earlier with the SDK, as mentioned in [Configuration Methods](/help/android/configuration/methods.md). 

1. The `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` or the `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` event type will be used. 

1. The custom data keys are prefixed with "`a.acquisition.custom.`"

>[!TIP]
>
>If you are sending data to multiple report suites, use the acquisition data from the app that is associated with the first report suite in your list of report suite IDs.

The updates in this section enable the SDK to send acquisition data from an acquisition link.

## Tracking mobile acquisition {#section_CEA30C652AC8470784B8054E299B80FA}

1. Add the library [to your project and implement lifecycle.

   For more information, see *Add the SDK and Config File to your IntelliJ IDEA or Eclipse Project* in [Core implementation and lifecycle](/help/android/getting-started/dev-qs.md). 

1. Import the library: 

   ```java
   import com.adobe.mobile.*;
   ```

1. Implement the `BroadcastReceiver` for the referrer: 

   ```java
   package com.your.package.name;  // replace with your app package name 
  
   import android.content.BroadcastReceiver; 
   import android.content.Context; 
   import android.content.Intent; 
  
   public class GPBroadcastReceiver extends BroadcastReceiver { 
     @Override 
     public void onReceive(Context c, Intent i) { 
      com.adobe.mobile.Analytics.processReferrer(c, i); 
     } 
   }
   ```

1. Update `AndroidManifest.xml` to enable the `BroadcastReceiver` that was created in the previous step: 

   ```xml
   <receiver android:name="com.your.package.name.GPBroadcastReceiver" android:exported="true"> 
    <intent-filter> 
     <action android:name="com.android.vending.INSTALL_REFERRER" /> 
    </intent-filter> 
   </receiver>
   ```

1. Verify that the `ADBMobileConfig.json` file contains the required acquisition settings: 

   ```xml
   "acquisition": { 
      "server": "c00.adobe.com", 
      "appid": "0652024f-adcd-49f9-9bd7-2552a4565d2f" 
   }, 
   "analytics": { 
     "referrerTimeout": 5, 
     ...
   ```

   >[!IMPORTANT]
   >
   >If you are sending data to multiple report suites, use the acquisition settings (acquisition server and appid) from the app that is associated with the first report suite in your list of report suite IDs.

   The `acquisition` settings are generated by Adobe Mobile services and should not be changed. For more information about how to download a customized `ADBMobileConfig.json` file with the `acquisition` settings pre-configured, see [Before You Start](/help/android/getting-started/requirements.md).

After these settings are enabled, after the initial launch of the app, acquisition data is sent automatically with the initial lifecycle call.

>[!CAUTION]
>
>`referrerTimeout` must be set to a value higher than 0 to enable app acquisition.
