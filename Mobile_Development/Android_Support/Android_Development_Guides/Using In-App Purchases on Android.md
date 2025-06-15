# Using In-App Purchases on Android

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-in-app-purchases-in-unreal-engine-projects-on-android](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-in-app-purchases-in-unreal-engine-projects-on-android)  
**Processed:** 2025-06-14 16:29:29

---

## Configuration

1.  Set up your in-app purchase in Google Play:
    
    Google Play requires the id to be all lowercase, and it's best to have the ID for iOS and Android match for ease of Blueprint setup.
    
    ![Example of the app id](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db7298c2-8fb5-489b-be76-7b719a2728ce/01-example-app-id.png "Example of the app id")
2.  Make a note of the ID you use, as well as if the item is consumable or non-consumable.
    
3.  If you have a Blueprint project, you're set to go. If you have a code project and have not already set up your project to use online subsystems, add the following block to your project's `Build.cs` file:
    
    ```
             `if (Target.Platform == UnrealTargetPlatform.Android)          {              PrivateDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "OnlineSubsystem" });              DynamicallyLoadedModuleNames.Add("OnlineSubsystemGooglePlay");          }`
    		
    Copy full snippet
    ```
    if (Target.Platform == UnrealTargetPlatform.Android) { PrivateDependencyModuleNames.AddRange(new string\[\] { "Core", "CoreUObject", "Engine", "OnlineSubsystem" }); DynamicallyLoadedModuleNames.Add("OnlineSubsystemGooglePlay"); }
4.  In **Project Settings > Platforms > Android**, find the **Advanced APKPackaging** section.
    
5.  Add an element to **Extra Permissions** called **com.android.vending.BILLING**.
    
    ![Add an element to the Extra Permissions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/702a6fe1-1d04-4a86-b9e7-1196a5d08232/ue5_1-02-add-extra-permission.png "Add an element to the Extra Permissions")
6.  Edit `[ProjectName]/Config/Android/AndroidEngine.ini`:
    
    ```
             `[OnlineSubsystem]          DefaultPlatformService=GooglePlay 		          [OnlineSubsystemGooglePlay.Store]          bSupportsInAppPurchasing=True`
    		
    Copy full snippet
    ```
    \[OnlineSubsystem\] DefaultPlatformService=GooglePlay \[OnlineSubsystemGooglePlay.Store\] bSupportsInAppPurchasing=True

## Reading Purchase Information

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5a9e2f0-87fa-4f22-9c57-bc28ffc81abd/image_3.png)

You can read the in-app purchase information using the **Read In-App Purchase Information** Blueprint node (or associated C++ function call). Like most other online subsystems functions, it takes a Player Controller as input, as well as an array of your product identifiers. Note that Make In-App Purchase below takes a single identifier, while Read can process an array of information. The function returns an array of In App Purchase structs, and each element of the array can be broken out to get the name, description, price, and other data to display in your UI or use in your gameplay logic.

## Completing a Purchase

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ef98ff4-6261-4f11-ba1c-e6f8cd0b9505/image_4.png)

To make an in-app purchase, use the **Make an In-App Purchase** Blueprint node (or associated C++ function call). It takes the Player Controller as input, as well as a Product Request struct. A Product Request is just the product identifier from iTunes Connect or the Google Play Developer console (in this case, match3theme\_night), as well as whether or not the product is consumable.

The **Make an In-App Purchase** node is latent, so any gameplay behavior you want to have rely on whether the purchase succeeds or fails should use those two execution pins. They will only execute after a response has come back from the online service. The node also returns the completion status of the purchase (such as Success, Failed, Restored) and the detailed In App Purchase Information struct.

There is a non-latent version of this function (the Blueprint node will display without the clock). The exit execution pin here does not wait for a response from the online service, and you will generally want to use the latent version.

## Testing

To test on Android, you need to upload the packaged APK to Google Play, as well as set up the correct testing profiles. You'll also need your custom key store.

## Helpful Links

-   [Administering In-app Billing (Creating products)](http://developer.android.com/google/play/billing/billing_admin.html)
-   [Testing Android](http://developer.android.com/google/play/billing/billing_testing.html)