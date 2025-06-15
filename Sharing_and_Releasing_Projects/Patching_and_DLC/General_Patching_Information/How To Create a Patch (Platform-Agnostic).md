# How To Create a Patch (Platform-Agnostic)

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-patch-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-patch-in-unreal-engine)  
**Processed:** 2025-06-14 16:28:52

---

![Banner Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91ce550e-c124-4904-a49f-8989585f7acf/create-patch-banner.png)

During patching, the **Unreal Engine** (UE) compares all the content post-cook to the originally released cooked content, and uses that to determine what is included in a patch. The smallest piece of content is a single package (like a `.ulevel` or `.uasset`), so if anything changes in a package then the entire package will be included in the patch. The method you use to get the patch's **PAK** (`.pak`) file to the users will depend on your distribution platforms, but this procedure will allow you to create a much smaller PAK file that just contains the updated content.

You can patch a project you have previously released using a versioned release. Some things to keep in mind are:

-   Lock down the serialization code paths at the time of release.
    
-   Keep the released cooked content, as the **UnrealPak** tool uses this to determine which content should be in the patch package file.
    
-   At runtime, mount both PAK files, with a higher priority for the patch file so any content within it is loaded first.
    

There are several methods for patching projects created in Unreal Engine. The method used here is **platform-agnostic**, meaning it technically can be used for any platform. However, the only two platforms that you would intentionally use this method with are **Windows** and **Xbox** One. Other platforms have specific patching methods. You can find documentation on these platform-specific methods in the section for the platform you are planning to develop for.

This method can eventually use a lot of data storage, because this method keeps all old files, and merely points the game to the newest files that exist. Platform-specific methods often use less space.

## How to Create a Patch Using the Project Launcher

This example provides information about creating a patch for the UE project.

### Create a Launch Profile for Testing the Patch

If you have base build of your project, you can create a **Launch Profile** for the patch in the **Project Launcher**. You might want to create one Launch Profile for creating a test version of your patch, and another Launch Profile for your actual patch release.

1.  Open the **Project Launcher**, by clicking **Platforms > Project Launcher**.
    
    ![Open the Project Launcher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af5f71db-4022-40c4-bb7f-2263c8b5aba1/ue5_1-01-open-project-launcher.png "Open the Project Launcher")
2.  Create a new **Custom Launch Profile** using the **+Add** button. This first Launch Profile is specifically for a test version of your patch. Type in a **Name** and **Description** that makes that clear.
    
    ![Add a new Custom Launch Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dd9f102-6593-4260-b45c-8bd6ccdb6a92/ue5_1-02-add-launch-profile.png "Add a new Custom Launch Profile")
3.  There are a number of settings in the Project Launcher that you can customize for a Launch Profile. You can further customize each setting by clicking the **Show Advanced** and set **Advance Settings** using dropdown menus. You can also click the top dropdown in the **Cook**, **Package** or **Deploy** sections, and your selection can change the available options.
    
    ![Show Advanced options in the Project Launcher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10d34d52-f8c5-4581-a6bd-5090172505d8/ue5_1-03-show-advanced-options.png "Show Advanced options in the Project Launcher")
    
    | Launch Profile Section Name | Description of Advanced Settings |
    | --- | --- |
    | **Project** | You can browse to the specific project to use, or use **Any Project** to patch the current project. |
    | **Build** | Options are **DebugGame**, **Development** and **Shipping**. Click the **Advanced Settings** dropdown to build the Unreal Automation Tool (UAT) as part of the patch process. |
    | **Cook** | Click the dropdown to select **Cook by the Book** or **Cook on the Fly**. You can also select **Do Not Cook**. You can click the **Advanced Settings** dropdown to select **Only Cook Modified Content**. Additional options display for **Advanced Settings**, and for **Release/DLC/Patching**, when you select **Cook by the Book**. |
    | **Package** | Options are **Package and Store Locally**, **Package and Store in Repository**, or **Do Not Package**. |
    | **Archive** | If you want to archive the build, check the box in this section. |
    | **Deploy** | Options are **Copy to Device**, **Copy Repository**, **File Server**, or **Do Not Deploy**. |
    | **Launch** | Options are **Using Default Role**, **Using Custom Roles**, and **Do Not Launch**. |
    

### Customize the Launch Profile

Follow these steps to customize your new Launch Profile.

1.  In the **Project** section, click the dropdown to browse to your project.
    
    ![Set Project section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10a5a381-b582-426f-9bb3-c59d7ef9a047/ue5_1-04-set-project-section.png "Set Project section")
2.  In the **Build** section, click the dropdown and select **Shipping**. Optionally, expand **Advanced Settings** if you need to build **Unreal Automation Tool (UAT)** as part of the patch process because you are creating the patch on a build machine.
    
    ![Set Build section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3de684b1-95bf-4932-aa07-d72abe40cea3/ue5_1-05-set-build-section.png "Set Build section")
3.  In the **Cook** section, click the dropdown and select **By the Book**. This gives you options for **Cooked Platforms**, **Cooked Cultures**, and **Cooked Maps**. Check the Cook settings for your project.
    
    ![Set Cook section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/170abe5b-a400-4828-b270-2f9985b31dc5/ue5_1-06-set-cook-section.png "Set Cook section")
    
    The Cook settings determine which content in your project is cooked for this patch, and that content is then compared to the original package file.
    
4.  Click the arrow to expand **Release/DLC/Patching Settings**.
    
    ![Open Release/DLC/Patching Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7f3a5c2-c3fe-449c-9941-8ec638dd5c1b/ue5_1-07-open-patching-settings.png "Open Release/DLC/Patching Settings")
5.  Under **Release Version This is Based On**, type the release version. Then check the box for **Generate Patch**.
    
    ![Set Release/DLC/Patching Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/122e4235-6b51-495a-901f-cc9f85511d45/ue5_1-08-set-patching-settings.png "Set Release/DLC/Patching Settings")
6.  Click the arrow to expand **Advanced Settings**. Make sure the following boxes are checked, as well as any others you need for your specific project's distribution method.
    
    -   **Compress Content**
        
    -   **Save Packages Without Versions**
        
    -   **Store All Content in a Single File (UnrealPak)**
        
    
    ![Set Advanced settings in the Cook section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ec47fa4-902c-41f9-b211-a0839b34bc64/ue5_1-09-set-adv-cook-settings.png "Set Advanced settings in the Cook section")
7.  Also in **Advanced Settings**, click the dropdown for **Cooker Build Configuration** and select **Shipping**.
    
    ![Set Build Configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3ce7373-d5b6-4662-be08-d70f477da81a/ue5_1-10-set-build-configuration.png "Set Build Configuration")
8.  In the **Package** section, click the dropdown and select **Package and Store Locally**. The local directory is entered by default; if you want to change it, click **Browse** and select the directory where you want to store the package.
    
    ![Set Package section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7cfc553-04de-4643-ab51-3e96b96f612a/ue5_1-11-set-package-section.png "Set Package section")
9.  In the **Deploy** section, click the dropdown and select **Do Not Deploy**.
    
    ![Set Deploy section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/886c95b4-ae1d-4cdb-82c5-896daf3566f7/ue5_1-12-set-deploy-section.png "Set Deploy section")
    
    Select **Do Not Deploy** to test the patch. When you have tested your patch and are ready to build a shipping version, follow the steps in this section and just choose a different Deploy method.
    

### Launch the Test Version of the Patch

1.  Navigate back to the main profile window using the **Back** button in the top right corner.
    
    ![Navigate to the Main Project Launcher window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/572a6b83-1caa-42aa-aa2c-899d3652b8a2/ue5_1-13-back-to-project-launcher-main.png "Navigate to the Main Project Launcher window")
2.  Click on the launch icon next to your **Patching** profile.
    
    ![Launch Patching process](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13283f18-1157-4d54-9d36-6ab2962f17f6/ue5_1-14-launch-patching.png "Launch Patching process")
3.  The project launcher will go through the building, cooking, and packaging process. This may take some time depending on the complexity of your project.
    
    ![Patching process in progress](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98514afd-6032-4306-b805-3b1271460f05/ue5_1-15-patching-in-progress.png "Patching process in progress")
4.  Once the operation is complete, close the window or click on **Done**.
    
    ![Patching process done](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a30e6733-8a64-4f46-9b71-044a4e3ebee0/ue5_1-16-patching-done.png "Patching process done")

### Create and Customize a Launch Profile for Shipping the Patch

1.  Create a new Custom Launch Profile using the **Plus** (**+**) button. This profile is for shipping your patch, so type a **Name** and **Description** to make that clear.
    
2.  Follow steps 1-11 in the [Customize the Launch Profile](/documentation/en-us/unreal-engine/how-to-create-a-patch-in-unreal-engine#customizethelaunchprofile) section. If needed, change the custom settings if your test version was significantly different from what you want to ship.
    
3.  In the **Deploy** section, click the dropdown and select the deployment option you want to use.
    
4.  When you've finished making the Shipping Launch Profile, follow the steps in the [Launch the Test Version of the Patch](/documentation/en-us/unreal-engine/how-to-create-a-patch-in-unreal-engine#launchthetestversionofthepatch) section.
    

## How to Create a Patch Using the Command Line

The Project Launcher is not the only option for creating a platform-agnostic patch for your project. You can also create a patch using command-line instructions with UAT.

First you need to create a base build. This is probably your shipping build. You need to use the command line parameter `-Createreleaseversion=<releasenumber>` when creating this build. This will create version 1.0 of your project.

Example:

```
	`BuildCookRun <normalbuildcookrunarguments> -build -cook -stage -pak -createreleaseversion=1.0`

Copy full snippet
```
BuildCookRun <normalbuildcookrunarguments> -build -cook -stage -pak -createreleaseversion=1.0

This will save a build in the `<ProjectPath>\Releases\1.0\` directory which will be required when generating the patch.

Once you have a numbered base build, you can create a patch that is based on that previous build. You need to use the command line parameter `-basedonreleaseversion=<releasenumber>` when creating this patch.

Example:

```
	`BuildCookRun <normalbuildcookrunarguments> -build -cook -stage -pak -generatepatch -basedonreleaseversion=1.0`

Copy full snippet
```
BuildCookRun <normalbuildcookrunarguments> -build -cook -stage -pak -generatepatch -basedonreleaseversion=1.0

## Installing a Patch

The platform-agnostic patching process creates a PAK file in following directory: `[ProjectName]\Saved\StagedBuilds[PlatformName][ProjectName]\Content\Paks`. Depending on the platform your project is created for, the PAK file contains the new or changed content that should be distributed to users. For example, on Windows, you would create an installer to copy that PAK file into the user's `[ProjectName]\Releases[VersionNumber][PlatformName]` folder, next to the original content PAK file.

The patch PAK file will automatically be mounted when it is located on the device in any of the PAK search directories set in `FPakPlatformFile::GetPakFolders`. To prioritize patches, the mounting system uses a `_p` at the end of the filename to determine that it gets priority over other PAK files. It can be renamed, but you need to include the `_p.pak` at the end of the file name.

If you build two patches from the same release version, they are both complete patches, so you should remove the first patch while installing the second patch.