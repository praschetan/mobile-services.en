---
description: This plug-in lets you send iOS AppMeasurement calls from your PhoneGap project.
keywords: phonegap
seo-description: This plug-in lets you send iOS AppMeasurement calls from your PhoneGap project.
seo-title: PhoneGap Plug-in
solution: Marketing Cloud,Analytics
title: PhoneGap Plug-in
topic: Developer and implementation
uuid: f88bcf10-1f9e-4c97-b348-40db797c9923
---

# PhoneGap plug-in{#phonegap-plug-in}

This plug-in lets you send iOS AppMeasurement calls from your PhoneGap project.

## New Adobe Experience Platform Mobile SDK Release

Looking for information and documentation related to the Adobe Experience Platform Mobile SDK? Click [here](https://aep-sdks.gitbook.io/docs/) for our latest documentation.

As of September 2018, we released a new, major version of the SDK. These new Adobe Experience Platform Mobile SDKs are configurable through [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* To get started, go to Adobe Experience Platform Launch.
* To see what is in the Experience Platform SDK repositories, go to [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).


## Create a PhoneGap project

To create a PhoneGap project, see [PhoneGap](https://helpx.adobe.com/experience-manager/6-4/mobile/using/phonegap.html).

## Install the plug-in using npm: {#section_43229E57C16944C0B51531CB92089189}

1. Run the following command: 

   ```
   cordova plugin add adobe-mobile-services
   ```

## Manually install the plug-in {#section_D53BA60D488C4DB8AD2BDF90439C180A}

### Include the AppMeasurement library

To include the AppMeasurement:

1. Drag `ADBMobile_PhoneGap.h` and  `ADBMobile_PhoneGap.m` into the **[!UICONTROL Plugins]** folder in your Xcode project. 
1. Complete the following settings:

    1. Select **[!UICONTROL Copy items into destination group's folder (if needed)]**. 
    1. Select the targets where you want to use AppMeasurement code.

1. Drag `ADB_Helper.js` into the `www` folder in your project. 
1. In the `res/xml` folder, open `config.xml` and register an new plugin by adding the following: 

   ```
   <feature name="ADBMobile_PhoneGap"> 
     <param name="ios-package" value="ADBMobile_PhoneGap" /> 
   </feature>
   ```

### Add app permissions

The AppMeasurement library requires the following:

1. Launch the Xcode IDE and open your app. 
1. Drag the **[!UICONTROL AdobeMobile]** folder into your Xcode project and complete the following settings:

    1. Select **[!UICONTROL Copy items into destination group's folder (if needed)]**. 
    1. Select **[!UICONTROL Create groups for any added folders]**. 
    1. Select the targets where you want to use AppMeasurement code and click **[!UICONTROL Finish]**.

   ![](assets/xcode-settings.png){width="672"}

1. In the **[!UICONTROL Build Phases]** tab of your project’s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

    * `libsqlite3.dylib`
    * `SystemConfiguration.framework`

1. Confirm that your app builds without unexpected errors.

## Implement custom tracking {#section_FD102B3CDAA4492FB04E56BF17E28663}

In `html` files where you want to use tracking, add the following to the `<head>` tag:

```html
<script type="text/javascript" charset="utf-8" src="ADB_Helper.js"></script>
```

