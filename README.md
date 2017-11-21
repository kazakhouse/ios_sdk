# ios_sdk
iOS integration SDK of https://www.admitad.com/

## Setting your project

Make sure that your project's deployment target is iOS 9.0 or higher.

Your project should be set up to make interaction with URL Schemes and Universal Links possible.

To add *AdmitadSDK* to your project you have two options:
1. Manual Installation
2. Installation via CocoaPods

### Manual Installation

*AdmitadSDK* makes use of *Alamofire* framework. In order to use AdmitadSDK please add Alamofire to your project.
The link below contains fully descriptive manual on Alamofire installation process:
[Alamofire GitHub Page](https://github.com/Alamofire/Alamofire)

To add *AdmitadSDK* itself please follow these steps: 
1. Clone this repository or download zip-file.
2. Locate *DeeplinkSDKTest.xcworkspace* and open it in Xcode.
3. Select *AdmitadSDK* target. Build the project.
4. In *Project navigator* locate *AdmitadSDK* project and unfold it if necessary. Go to *Products* folder, where you can find *AdmitadSDK.framework*. Right-click on it and select *Show in Finder*.
5. Drag *AdmitadSDK.framework* to your project's directory.
6. In your Xcode project go to *Project->Target->General->Embedded Binaries* and add *AdmitadSDK* by clicking on the "plus" button.
7. In *Project->Target->Build Settings->Framework Search Paths* add `$(PROJECT_DIR)`. You can place *AdmitadSDK* to another directory, but be sure that the directory is present in the *Framework Search Paths* list.

### Installation via CocoaPods

to be written...

## Objective-C interoperability

Just add `@import AdmitadSDK;` import statement to the source files that make use of *AdmitadSDK*.

## Setting AppDelegate

1. In `application(_:didFinishLaunchingWithOptions:)` method assign *AdmitadTracker* singleton's `postbackKey` property to your Admitad Postback Key.
2. In the same method call *AdmitadTracker*'s `trackAppLaunch()`, `trackReturnedEvent()` и `trackLoyaltyEvent()`.
3. To track Universal Links usage, in `application(_:continue:restorationHandler:)` call corresondingly named `continueUserActivity` method and pass `userActivity` to it as parameter.
4. To track URL Schemes usage, in `application(_:open:options:)` call `openUrl` method and pass `url` to it as parameter.

## Event Tracking

If you have setup your *AppDelegate* right, *Installed* event is triggered automatically, *Returned* and *Loyalty* event are triggered when `trackReturnedEvent()` and `trackLoyaltyEvent()` respectively are called. To track *Confirmed Purchase* and *Paid Order* an *AdmitadOrder* object must be instantiated and passed as parameter to `trackConfirmedPurchaseEvent` or `trackPaidOrderEvent` respectively.

Methods `trackRegisterEvent()`, `trackReturnedEvent()` and `trackLoyaltyEvent()` can take user ID as parameter. Optionally you can setup *AdmitadTracker* singleton's `userId` property. If you prefer not to provide user ID in any of these ways, user ID will be generated automatically.

## Delegation and Callbacks

When working with *AdmitadSDK* from Swift environment you are provided with two mechanisms of notification on event tracking success or failure. Every event triggering method takes a completion callback. In the callback you can check if an error has occurred. *AdmitadTracker* instance also notifies its *delegate* object conforming to *AdmitadDelegate* protocol. Both ways of notification are independent from each other and can be used simultaneously and interchangeably. In Objective-C environment only the former mechanism is available.
