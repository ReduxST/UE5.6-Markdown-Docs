# Releasing Your Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/preparing-unreal-engine-projects-for-release](https://dev.epicgames.com/documentation/en-us/unreal-engine/preparing-unreal-engine-projects-for-release)  
**Processed:** 2025-06-14 16:44:12

---

Use **Unreal Editor** for packaging a release version of you project for distribution. This page shows you how to package a release-versioned project on the example of packaging project for Windows Platform. Follow the steps below to package your project via the **Project Launcher**. Packaging process details depend on the platform for which you make a project: a Windows game, shipping a mobile project, or targeting another platform. The steps you take with the finished packaged content will be different.

This is an example of packaging a 1.0 release of ThirdPersonGame, aimed at Windows 64-bit, localized in English.

## Open Project Launcher

1.  Click **Platforms** button of the Unreal Editor **Toolbar** and select **Project Launcher**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab96a78d-6a09-44e7-8385-cc11b28329e9/01_projectlauncher.png)
2.  Create a new Custom Launch Profile by clicking the **Add** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/058ad76f-c6d7-402e-b3c7-77a30c6f6d1e/02_addcustomprofile.png)
3.  Set a name and description for your profile.
    

## Adjustment of Custom Project

There are a number of settings for the release process.

#### Project

Under **Project** section you can set the specific project, or use **Any Project**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea8bf738-3209-4e82-89b3-87dfe72fe3be/03_adjcustproj_project.png)

#### Build

1.  Set the **Build** configuration to **Shipping**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66e1c422-2918-4950-910b-8683b632cbb9/04_adjcustproj_buildshipping.png)
2.  Optionally, expand **Advanced Settings** if you need to build **Unreal Automation Tool (UAT)** as a part of the release.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/702d6751-a922-4ff3-a24e-817be8b55ea0/05_adjcustproj_builduat.png)

#### Cook

1.  Select **By the Book** as the cooking method in the dropdown menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdc4a449-fac7-4443-903d-ba9b2ef0023b/06_adjcustproj_cookbybook.png)
2.  Check the boxes for all platforms you would like to cook content for. In this example for Windows testing, **WindowsNoEditor** is selected.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb4991b8-a868-43fd-b194-ba7c84e0b24c/07_adjcustproj_cookwindows.png)
3.  Check the boxes for all cultures to cook localizations for.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffff80bd-ccae-4837-a7a7-658f99d915cf/08_adjcustproj_cookcultures.png)
4.  Check the boxes for which maps to cook.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e24f61d0-289c-43ad-a742-32f96a8d5524/09_adjcustproj_cookmaps.png)
5.  In **Release/DLC/Patching Settings**:
    
    -   Check the **Create a release version of the game for distribution.** checkbox.
    -   Enter a version number for this release.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f2a380e-3d53-45f9-9906-9dc3517e23bd/10_adjcustproj_cookrealisesettings.png)
6.  Expand **Advanced Settings** and make sure the following options are enabled, as well as any others you need for your specific project's distribution method:
    
    -   **Compress content**.
    -   **Save packages without versions**.
    -   **Store all content in a single file (UnrealPak)**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9dbc4df-9a21-495a-885f-01c9d8484be4/11_adjcustproj_cookadvancesettings.png)
7.  Also under **Advanced Settings**, set the **Cooker build configuration** to **Shipping**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee844ead-1a1b-4e81-8e1f-ea4641b89a84/12_adjcustproj_cookadvanceshipping.png)

#### Package

Set the build to **Package & store locally**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/355844ce-b5ba-4b89-aba0-433ad1b343be/13_adjcustproj_package.png)

#### Deploy

1.  Set the **Deploy** to **Do not Deploy**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/438ae1d7-ce73-4ea0-aa7e-775adeb04838/14_adjcustproj_deploy.png)
2.  Once you have set all the above settings, navigate back to the main profile window using the **Back** button in the top right corner.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b9ee06b-2992-4c53-bfeb-209c03ce5856/15_backbutton.png)
3.  Click on the launch icon next to your **Release** profile.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a12881bb-566a-4d6c-9a31-87b324c2f7d5/16_launchicon.png)
4.  The project launcher will go through the building, cooking, and packaging process. This may take some time depending on the complexity of your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26845a47-a1d6-40a8-ad45-70ef9e4c0eec/17_packagingprocess.png)
5.  Once the operation is complete, close the window or click on **Done**. You can test the patch now with the steps below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37d70265-4259-4d7e-a910-37ae1fd86657/18_packagingprocessdone.png)
6.  Save the asset registry and pak file from `[ProjectName]\Releases[ReleaseVersion][Platform]`. In this example, this is `ThirdPersonGame\Releases\1.0\WindowsNoEditor`.
    
    The asset registry and pak file will be needed for any future patches or DLC to check against.
    
7.  On Windows, you can test running the project from `[ProjectName]\Saved\StagedBuilds\WindowsNoEditor`.
    

While Steam will allow you to upload full packages of your game and do the updating process for you, using release versions as outlined here is still the recommended practice when distributing through Steam. This will make the process smoother if you decide to add additional supported platforms or distribution methods later on.