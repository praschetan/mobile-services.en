---
description: This information helps you implement the iOS library and collect lifecycle metrics, such as launches, upgrades, sessions, engaged users, and so on.
seo-description: This information helps you implement the iOS library and collect lifecycle metrics, such as launches, upgrades, sessions, engaged users, and so on.
seo-title: Core Implementation and Lifecycle
solution: Marketing Cloud,Analytics
title: Core Implementation and Lifecycle
topic: Developer and implementation
uuid: 96d06325-e424-4770-8659-4b5431318ee3
---

# Core implementation and lifecycle {#core-implementation-and-lifecycle}

This information helps you implement the iOS library and collect lifecycle metrics, such as launches, upgrades, sessions, engaged users, and so on.

## Download the SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

>[!IMPORTANT]
>
>To download the SDKs, you **must** use iOS 6 or later.

**Prerequisite**

Before you download the SDK, complete the steps in *Create a Report Suite* in [Core implementation and lifecycle](/help/ios/getting-started/requirements.md) to set up a development report suite and download a pre-populated version of the configuration file. 

To download the SDK:

1. Download, unzip the `[Your_App_Name_]AdobeMobileLibrary-4.*-iOS.zip` file and verify that you have the following software components:

    * `ADBMobile.h`, the Objective-C header file that is used for iOS AppMeasurement. 
    * `ADBMobileConfig.json`, which is the SDK configuration file that is customized for your app. 
    * `AdobeMobileLibrary.a`, a bitcode-enabled fat binary that contains the library builds for iOS devices (armv7, armv7s, arm64), and simulators (i386, x86_64).

      This fat binary should be linked when the target is intended for an iOS app. 

    * `AdobeMobileLibrary_Extension.a`, a bitcode-enabled fat binary that contains the library builds for iOS devices (armv7, armv7s, arm64) and simulators (i386, x86_64).

      This fat binary should be linked when the target is intended for an iOS extension. 

    * `AdobeMobileLibrary_Watch.a`, a bitcode-enabled fat binary that contains the library builds for Apple Watch devices (armv7k) and simulators (i386, x86_64).

      This fat binary should be linked when the target is intended for an Apple Watch (watchOS 2) extension app. 

    * `AdobeMobileLibrary_TV.a`, a bitcode-enabled fat binary that contains the library builds for new Apple TV devices (arm64) and simulator (x86_64).

      This fat binary should be linked when target is intended for an Apple TV (tvOS) app.

>[!IMPORTANT]
>
>If you download the SDK outside the Adobe Mobile services UI, the `ADBMobileConfig.json` file must be manually configured. If you are new to Analytics and the Mobile SDK, see [Before You Start](/help/ios/getting-started/requirements.md) to set up a development report suite and download a pre-populated version of the configuration file.

## Add the SDK and config file to your project {#section_93C25D893B4A4CD3B996CF3C5590C8DC}

1. Launch the Xcode IDE and open your app. 
1. In Project Navigator, drag the `AdobeMobileLibrary` folder and drop it under your project. 
1. Verify the following:

    * The **[!UICONTROL Copy Items if needed]** checkbox is selected. 
    * **[!UICONTROL Create groups]** is selected. 
    * None of the checkboxes in the **[!UICONTROL Add to targets]** section is selected.

     ![](assets/step_3.png)

1. Click **[!UICONTROL Finish]**. 
1. In **[!UICONTROL Project Navigator]**, select **`ADBMobileConfig.json`**. 
1. In **[!UICONTROL File Inspector]**, add the JSON file to any targets in your project that will use the Adobe SDK.

   ![](assets/step_4.png)

1. In **[!UICONTROL Project Navigator]**, complete the following steps:

    1. Click on your app. 
    1. On the **[!UICONTROL General]** tab, select your targets and link the required frameworks and libraries in the **[!UICONTROL Linked Frameworks]** and **[!UICONTROL Libraries]** sections.

      * **iOS App Targets**
        * `SystemConfiguration.framework`
        * `WebKit.framework`
        * `libsqlite3.0.tbd`
        * `AdobeMobileLibrary.a`
        * `CoreLocation.framework` (optional, but required for geo-tracking capabilities)

      * **iOS Extension Target**

        * `SystemConfiguration.framework`
        * `libsqlite3.0.tbd`
        * `AdobeMobileLibrary\_Extension.a`

      * **Apple Watch (watchOS 2) Target**

        * `libsqlite3.0.tbd`
        * `AdobeMobileLibrary\_Watch.a`

      * **Apple TV (tvOS) Target**

          * `SystemConfiguration.framework`
          * `libsqlite3.0.tbd`
          * `AdobeMobileLibrary\_TV.a`


    >[!CAUTION]
    >
    > Linking more than one `AdobeMobileLibrary*.a` file in the same target will result in unexpected behavior or the inability to build.

1. Confirm that your app builds without errors.

## Implement lifecycle metrics {#section_532702562A7A43809407C9A2CBA80E1E}

>[!IMPORTANT]
>
>iOS will send lifecycle information with or without calling `collectlifecycledata`, and `collectlifecycledata` is only a way to initiate lifecycle earlier in the application's launch sequence.

After you enable lifecycle, each time your app is launched, one hit is sent to measure launches, upgrades, sessions, engaged users, and other [Lifecycle Metrics](/help/ios/metrics.md).

Add a `collectLifecycleData`/ `collectLifecycleDataWithAdditionalData` call in `application:didFinishLaunchingWithOptions`:

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
 [ADBMobile collectLifecycleData]; 
    return YES; 
}
```

### Include additional data with lifecycle calls

To include additional data with lifecycle metric calls, use `collectLifecycleDataWithAdditionalData`:

>[!IMPORTANT]
>
>Any data that is passed to the SDK through `collectLifecycleDataWithAdditionalData:` is persisted in `NSUserDefaults` by the SDK. The SDK strips the values in the `NSDictionary` parameter that are not of the `NSString` or `NSNumber` types.

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
    NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
    [contextData setObject:@"Game" forKey:@"myapp.category"]; 
    [ADBMobile collectLifecycleDataWithAdditionalData:contextData]; 
    return YES; 
}
```

Additional context data values that are sent with `collectLifecycleDataWithAdditionalData` must be mapped to custom variables in Adobe Mobile services: 

![](assets/map-variable-lifecycle.png)

Other lifecycle metrics are collected automatically. For more information, see [Lifecycle Metrics](/help/ios/metrics.md).

## What to do next {#section_A24DC703359D4B5C8F493D6421306FD3}

Complete the following tasks:

* [Track App States](/help/ios/analytics-main/states.md) 
* [Track App Actions](/help/ios/analytics-main/actions.md)
