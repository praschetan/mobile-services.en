---
description: Release notes and known issues for iOS SDKs 4.x for Experience Cloud Solutions.
seo-description: Release notes and known issues for iOS SDKs 4.x for Experience Cloud Solutions.
seo-title: Release Notes
solution: Marketing Cloud,Analytics
title: Release Notes
topic: Developer and implementation
uuid: e1613dc5-02a4-43a7-997a-29b4de98b4d1
---

# Release notes {#release-notes}

Here is the release notes, known issues, and hot fix information for iOS SDKs 4.x for Experience Cloud Solutions:

**March 24, 2020: Version 4.19.2**

* General - Fixed some leaks in Target code.

**March 12, 2020: Version 4.19.1**

* General - Resolved a potential crash caused when Swift enums are included in context data for tracking calls.
* Target – Target Session Id will now be added as a context data parameter ‘a.target.sessionId’ in the internal Analytics for Target hit sent to Adobe Analytics.

**Feburary 4, 2020: Version 4.19.0**

* Lifecycle - Added a new API, pauseCollectingLifecycleData, to mitigate the abnormal session length data that was reported from some old iOS devices.

**November 8, 2019: Version 4.18.9**

* In App Messaging - Fixed a bug where cached or bundled images could not be loaded in the full screen messages.

**September 20, 2019: Version 4.18.8**

* In App Messaging:

  * On devices running iOS 10 or newer, the `UserNotifications` framework is now used to schedule local notifications for apps that are linked to the `UserNotifications.framework`.
  * Fullscreen messages now use WKWebViews from `WebKit.framework`, which must be linked in your Xcode project.
  * Fixed a bug where the Push click-through payload could not be used as traits for In-App Messaging.
  * Fixed a crash issue.

* General - Fixed a bug where SDK data was synchronized to the paired watchOS app on every Analytics call.

**August 2, 2019: Version 4.18.7**

* Reverted a change that was introduced in version 4.18.6 which, in some environments, caused a crash on devices that were running an iOS version older than 11.0.

* Adobe Target: Added the `requestLocationParameters` property in `ADBTargetRequestObject`, which enables the impressionId to be sent with Target requests.

**July 18, 2019: Version 4.18.6**

* Adobe Target: All requests now include the client and the `sessionId` in the URL query parameters.
* Adobe Target: Fixed a memory leak.
* Visitor ID Service: The `visitorAppendToURL` and `visitorGetUrlVariablesAsync` APIs no longer double-encode their return values. 

  The double-encoding was causing the return values from those APIs to be flagged by certain security reviews.

**June 5, 2019: Version 4.18.5**

* Analytics - Append push opt-in status to Lifecycle data when push notifications are enabled.

**May 24, 2019: Version 4.18.4**

* Visitor ID Service - Increased the return timeout for the 
`visitorGetUrlVariablesAsync` API to 30 seconds.

* Visitor ID Service - The `setPushIdentifier` API call now sends a sync call to the Visitor ID Service every time it is called. 

For more information about the current and past release notes for all solutions, see [Adobe Experience Cloud Release Notes](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html).
