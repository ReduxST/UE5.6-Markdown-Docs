# Provisioning Profiles and Signing Certificates

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-ios-tvos-and-ipados-provisioning-profiles-and-signing-certificates-for-unreal-engine-projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-ios-tvos-and-ipados-provisioning-profiles-and-signing-certificates-for-unreal-engine-projects)  
**Processed:** 2025-06-14 16:49:40

---

To publish iOS, iPadOS, and tvOS games, you need a **Code Signing Certificate** identifying you as a valid Apple developer, as well as a **Provisioning Profile** identifying the services and permissions needed for your app. While **Xcode** automatically manages this process for building code, you need to provide these manually in your **Unreal Engine** project settings so that the Unreal Engine build system can cook and package a project. This guide will explain all the steps needed to set up valid Certificates and Provisioning Profiles.

This guide covers the full setup for building Unreal Engine C++ projects with MacOS and Xcode. While you need a MacOS machine with Xcode to build your project to ship on the app store, Unreal Engine provides several other paths for building iOS apps for development and testing purposes, including paths for working on Windows. Refer to [Appendix B: Additional Build Options](/documentation/en-us/unreal-engine/setting-up-ios-tvos-and-ipados-provisioning-profiles-and-signing-certificates-for-unreal-engine-projects#appendixb:additionalbuildoptions) for more information.

## 1\. Overview and Requirements

To build and distribute an **Unreal Engine** project for an iOS, tvOS, or iPadOS device, you need the following requirements:

-   A computer running MacOS.
-   An installation of Xcode that is compatible with your current version of Unreal Engine.
-   An Apple Developer Account.
-   An Unreal Engine Project.

Refer to the [iOS, iPadOS, and tvOS Development Requirements](/documentation/404) page for more information about the MacOS and Xcode versions required for use with the current version of Unreal Engine. Refer to the [iOS Quickstart Guide](/documentation/en-us/unreal-engine/setting-up-an-unreal-engine-project-for-ios) guide for instructions about how to set up Xcode to work with Unreal Engine.

You need an Apple Developer Account to create code signing certificates and provisioning profiles. If you do not already have one, visit [developer.apple.com](https://developer.apple.com/) and create an Apple ID and a Developer Account.

While Epic's software is available free of charge, Apple Developer accounts cost a fee of $99 per year. Keep this in mind when registering your account.

Finally, you need to do the following on your Apple Developer Account:

-   Connect Xcode with your Developer Account.
-   Create an **Identifier (App ID)** for your app.
-   Create a **Provisioning Profile** for a deployment of your app.
-   Create a **Signing Certificate** identifying yourself as the creator of your app.
-   Register your iOS device with your account.

Once you have each of these components, you need to download the Provisioning Profile and Signing Certificate and add them to your **Project Settings.** After that, you can package projects and push them to your device. The sections below will detail each of these steps.

## 2\. Connect Xcode With Your Apple Developer Account

To make sure your Certificates and Provisioning Profiles are recognized correctly, connect Xcode with the Apple ID for your Apple Developer Account.

1.  Open Xcode, then click **Xcode** > **Preferences**.
    
2.  Click the **Accounts** tab.
    
3.  Click **Add (+)** to add an account. Provide the information for your Apple Developer Account.
    

## 3\. Create Your Identifier (App ID)

All iOS apps require an Identifier with a Bundle ID. Your Provisioning Profile references this information in a later step. To create an Identifier, follow these steps:

1.  Login to your [Apple Developer Account](https://developer.apple.com).
    
    ![The sign-in screen for the Apple Developer page](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd91a0ee-7baa-4e28-8768-97477784f9d7/signin.png)
2.  Click **Certificates, Identifiers, and Profiles**.
    
    ![The Certificates, Identifiers, and Profiles option is where you configure most of the details in this guide](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db7f8cdd-3434-4531-8cd7-4b8f0e8f23d4/certsidsprofs.png)
3.  Click **Identifiers**, then click **Register an App ID**.
    
    ![Registering an Identifier in the Identifiers page](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92b676c4-a8bc-4607-8a56-9fc3de5fd6be/appid.png)
4.  Select **App IDs** and click **Continue**.
    
5.  Select **App** and click **Continue**.
    
6.  In the **Register an App ID** menu, fill in your **Description** and **Bundle ID**. The Bundle ID should be a reverse-domain string taking the format `com.(OrganizationDomainName).(AppName)`. In this example, the app is called `com.YourCompany.MobileTestGame`.
    
    Take note of the application name you provide for the App ID, as this information must match the name of your Unreal Engine project. Specifically, you need the name of the `.uproject`, without the extension. You also need the Bundle ID to match in both your Xcode project and the **Project Settings** in Unreal Editor.
    
7.  Select any permissions and services your app needs, then click **Continue**.
    
8.  Confirm that all your settings are correct, then click **Register**.
    

## 4A. Create a Code Signing Certificate from Xcode

If you have connected Xcode with your Apple Developer account, you can generate a Development Certificate automatically with these steps:

1.  Open your project's solution in **Xcode**, then select your project in the navigation panel. This will display the project's settings.
    
2.  In the **General** settings, provide your project's bundle identifier. This should be a reverse-domain style string reading com.(OrganizationName).(ProjectName). In this example, it reads `com.YourCompany.MobileTestGame`.
    
3.  Click **Signing and Capabilities**. Set the **Team** to the name given by your Apple Developer profile.
    
4.  Enable **Automatically Manage Signing**. Xcode will connect with the Apple Developer site and generate a Code Signing Certificate for Development.
    

This Certificate will only be available on the Mac you configured it on, and it will only be usable for development, not shipping.

## 4B. Generate a Signing Certificate Manually

Development Certificates generated by Xcode make it possible to deploy your project for testing, but to ship your project you may need to create a Signing Certificate that is configured for distribution on the app store. You may also need to create a Certificate that is usable by your team on other devices.

Follow these steps to manually create a Certificate with your Apple Developer account:

1.  Open the **Keychain Access** app. Click **Keychain Access** > **Certificate Assistant** > **Request a Certificate From a Certificate Authority.**
    
2.  In the **Certificate Information** dialog, provide your Apple Developer Email address and your name. Click **Continue**, then save the signing request to a convenient location, such as the desktop.
    
3.  Open the **Apple Developer Page**. In the Certificates, Identifiers, and Profiles menu, click **Certificates**, then click **Create a Certificate**.
    
4.  Select **iOS App Development**, then click **Continue**. If you are creating a certificate to ship your app, you need to use **iOS Distribution (App Store and Ad Hoc)** instead.
    
    ![Creating a Code Signing Certificate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ec2c943-2407-42d6-b5df-a54b7a17fdd4/appcert.png)
5.  Click **Choose File**, then select the **Certificate Signing Request file** you generated. Click **Continue** to generate your Certificate.
    
6.  Download the Certificate and open it to add it to your System Keychain.
    

## 6\. Create a Provisioning Profile

Your app's Provisioning Profile ties together your identity as an Apple Developer, information about your test devices, and information about the app's entitlements.To create a Provisioning Profile, follow these steps:

1.  In the **Certificates, Identifiers & Profiles** menu on the Apple Developer page, click **Profiles**, then click **Generate a Profile**.
    
2.  Select **iOS App Development,** then click **Continue**.
    
    ![Creating a Provisioning Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff52cefc-da67-49ea-bff9-3f4eebbdf9a3/appprov.png)
    
    This page uses an iOS app as an example, but you can select the provisioning profile type that is appropriate to your target device. For example, if you are creating a tvOS app, choose **tvOS App Development**.
    
3.  Click the **App ID** dropdown and select the App ID you generated in the previous section, then click **Continue**.
    
    ![Choosing the Identifier for your app for your Provisioning Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b3f1b9f-7e7e-43dd-a458-a51afb6237bb/appprovid.png)
4.  Choose the **Signing Certificate** for **Development** that you generated in the previous section, then click **Continue**.
    
    If you need to share your Signing Certificate and Provisioning Profile with your team, create a Certificate manually.
    
5.  Choose your registered device as a test device, then click **Continue**.
    
6.  Provide a **Provisioning Profile Name**. In this example, the profile is called **MobileTestGame\_Development**. Click **Generate**.
    
7.  Download the Provisioning Profile and place it in a convenient location. Click and drag it onto the Xcode app icon in your dock to install it.
    

## 7\. Add Your Provisioning Profile and Signing Certificate to Unreal Editor

Xcode does not need a Provisioning Profile to build code if you have it set to automatically manage code signing. However, Unreal Engine's build system and the iPhone Packager need to refer to your Provisioning Profile and Signing Certificate to cook and package your project's executable for iOS. Follow these steps to provide your Provisioning Profile and Signing Certificate in Unreal Engine's project settings:

1.  Open Unreal Editor, then open **Project Settings** > **Platforms** > **iOS**. Make sure your **Bundle Identifier** is set to the same name as in both Xcode and your Apple Developer Account.
    
2.  Wait for a moment for the editor to discover your Provisioning Profile and Signing Certificate. If the entries for your Provisioning Profile and your Certificate both turn green, they are recognized as valid profiles and will be used automatically. You can select the check box to manually set them as well.
    

You can perform the steps in this section on a Windows machine for Blueprint-only projects and remote builds.

The Signing Certificate you select in your Project Settings must match the one used to generate your Provisioning Profile, otherwise your project will fail to package.

## 8\. Package Your Project

1.  Click **Platforms** > **iOS** > **Package Project** to package for iOS. If all of your settings are correct and your Provisioning Profile and Signing Certificate are both valid, UE creates an iOS build.
    
2.  Click the **Platforms** dropdown again. If your iOS device appears in the **Quick Launch** options, select it to deploy a build directly to your device.
    

## Final Result

After following the steps in this guide, you have all the needed components to build and distribute iOS projects. When you need to create a Provisioning Profile for testing or shipping, refer to this guide again and configure your Identifier, Certificate, and Provisioning Profile accordingly.

## Appendix A: Obtaining an Apple Worldwide Developer Relations (WWDR) Certificate

Apple requires an [Apple Worldwide Developer Relations Certificate](https://developer.apple.com/support/expiration/) to build apps. This should be provided by Xcode automatically, but in some situations, you may need to manually install it on your Mac.

1.  Go to the Apple [Certificate Authority Page](https://www.apple.com/certificateauthority) and download the latest WWDR Intermediate Certificate.
    
2.  Open the **Keychain Access** app and drag the certificate into the **System keychain**.
    

## Appendix B: Additional Build Options

The steps in this guide are for the full Signing and Provisioning process needed to distribute an app. There are several other options available during development and testing:

-   Blueprint-only iOS projects do not need to go through the Signing and Provisioning process to package builds or push them to devices for testing – you can package them directly out of the box. This path will also work on Windows. Refer to [Building for iOS on Windows](/documentation/en-us/unreal-engine/creating-remote-builds-of-unreal-engine-projects-for-ios) for more information.
    
-   Because most teams using Unreal Engine use Windows machines for development, a remote build process is available. This will create a secure connection with a MacOS device and have it automate a build. Refer to the [Building for iOS on Windows guide](/documentation/en-us/unreal-engine/creating-remote-builds-of-unreal-engine-projects-for-ios) for more information.
    

## Appendix C: Sharing Your Signing Certificates With Your Team

In UE 5.3 and newer, automatic code signing is the preferred method for handling signing certificates in Development builds. Your team should have a shared Apple developer account that each team member can connect to in Xcode, which provides all of them shared access to signing and provisioning resources.

If you need to share manually-created signing certificates or provisioning profiles, create a folder in your UE project directory called Provisioning, then place them in that folder. They are not necessary for the build process, but you can add them to source control for your team and share them as needed.