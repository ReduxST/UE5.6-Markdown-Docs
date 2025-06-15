# Build Operations: Cook, Package, Deploy, and Run

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:17

---

As part of the packaging process, the [Automation Tool](/documentation/en-us/unreal-engine/unreal-automation-tool-for-unreal-engine) (sometimes abbreviated as **UAT** for **Unreal Automation Tool**) is used to work through a set of utility scripts for manipulating **Unreal Engine (UE)** projects. For the packaging process, the Automation Tool uses a particular command called **BuildCookRun**. This command can cook content for a platform, package it up into a platform's native format for distribution, deploys it to the device, and automatically runs the project (where applicable). Packaging your project does not solely require the direct use of UAT, though. Use the **Platforms** button of the UE **Toolbar** to select from available platforms or Command Line to cook and package content for a platform.

As part of the **BuildCookRun** command in UAT, the following stages outline the different stages of the packaging pipeline:

-   **Build:** This stage compiles the executeables for the selected platform.
-   **Cook:** This stage cooks content by executing the UE in a special mode.
-   **Stage:** This stage copies the executables and content to a staging area; a standalone directory outside of the development directory.
-   **Package:** This stage packages the project into a platform's native distribution format.
-   **Deploy:** This stage deploys the build to a target device.
-   **Run:** This stage starts the packaged project on the target platform.

For a list of predefined tasks, read the [BuildGraph Script Tasks](/documentation/en-us/unreal-engine/buildgraph-script-tasks-reference-for-unreal-engine) reference page.

## Packaging Methods

Because you can deploy content in several different ways to a target platform for testing, debugging, or in preparation for release, you can test your packages in multiple different ways:

-   Use [UE Toolbar](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#launchon) to quickly test a part of your currently loaded **Level** for testing and debugging.
-   Use the [Project Launcher](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#projectlauncher) to use a default profile or create a custom one to perform actions like profiling or debugging for your project's latest build.
-   Take an already packaged game and deploy it to a platform, such as a console or mobile device.

Follow sections below to learn more about these packaging methods and how you can package your games using them.

### UE Toolbar

Use **Platforms** button of the UE **Toolbar** to select a platform to package your project for. When you package a project using this option, it will save the packaged project to a folder that you select but will not deploy it to the device.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04d434bd-ca05-4343-99a1-d5b7ac02b92a/01_platformstoolbarbutton.png)

From drop-down menu under **Platforms**, you can perform the following actions:

-   Build and launch a project on the available device you need. When clicked, the launch process automatically Cooks the necessary content, build code, and launch on the selected platform. The build is a quick way to test functionality during active development without the need to compile and run the entirety of the project every time you need to test something.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb4146d6-eb95-4d40-b440-cd895423558e/02_platformstoolbardevices.png)
-   Choose the target platform and adjust the **Build Configuration** for it (**Development**, **Shipping**, and so on).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90bba8b1-c844-40ef-bdba-8de508fa493c/03_platformstoolbar_buildconfig.png)
    
    In UE 5.4.0, there is a known issue where, if you try to package with the "Use Project Setting" option it will use the configuration set in **Project Settings** > **Packaging** at the time the editor started even if you change it. To remedy this, restart the editor to ensure the new build configuration takes effect, or choose one of the binary configurations from the Platforms menu instead of Use Project Setting. This issue is resolved in UE 5.4.1."
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23dad69e-c06b-4efe-ac9f-56e1fa7bf036/buildconfigissue.png)
-   Access to the **Project Launcher**, **Device Manager**, **Packaging Settings**, and **Supported Platforms**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47d363c6-e445-44d6-9f51-ef18f16ef893/04_platformstoolbaroptandset.png)

If you do not see the platform you want to deploy to or it is grayed out in this menu, here are some things you can check:

-   Make sure that you have the correct SDK installed for that platform (if required) and that it is supported by the Engine version you are currently using. Often, this can be checked in the platform's **UEBuild.cs** file located in **Engine/Source/Programmings/UnrealBuiltTools/Platforms**. For example, if you needed to see which SDK is supported for Android, you could look in the **UEBuildAndroid.cs** file.
-   Be sure that any Visual Studio extensions or necessary files are installed.
-   Some platforms (like console) require external tools to connect the device. Make sure this is working properly, and the device is detected.
-   Use the **Device Manager** in the Engine to "claim" any devices as needed, which ensures it can only be used for your local machine.

### Project Launcher

The [Project Launcher](/documentation/en-us/unreal-engine/preparing-unreal-engine-projects-for-release) affords you the ability to deploy for different platforms all from one location and even from a single launch profile. For open Project Launcher click **Platforms > Project Launcher**.

Each platform that is deployed to has its own default launch profile (listed in the main window). You can also choose to create a custom one that enables you to build a project in a specific way with many advanced settings. These include being able to apply command line arguments, test downloadable content (DLC) and patching releases, and much more.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dacaa40-81ca-428f-9c4e-ce392383550c/05_projectlauncher.png)

For additional information, see the [Project Launcher](/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine) reference page.

#### Custom Launch Profile

From the Project Launcher, you can create a **Custom Launch Profile** that can be used on all platforms or even just the ones you specify. These profiles enable you to build your content in specific ways by setting how it is cooked, packaged, and deployed using the available build operations.

To add your own Custom Launch Profile, click the **Add** button on the right side of the window.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ca2394c-8a2a-4426-8fa9-f7b9fa777edd/06_addcustomprofile.png)

After doing so, the Custom Launch Profile is immediately open. Be sure to give it a **Name** and **Description** so that you can quickly identify it later.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98df936d-7915-42f4-9e8f-5dbb664e8a36/07_setcustomlaunchprofile.png)

### Command Line

The [Automation Tool](/documentation/en-us/unreal-engine/automation-test-framework-in-unreal-engine) enables you to cook and package your game using Command Line, and since all build operations are performed by UAT, it can be run directly on the Command Line with **RunUAT.bat** file when provided with valid arguments.

The RunUAT files can be found in `Engine/Build/BatchFiles`. For Windows, use the **RunUAT.bat** file and for Mac/Linux use the **RunUAT.sh**.

A basic cook can be performed using the following command line arguments following either the **UnrealEditor.exe** or **UnrealEditor-cmd.exe** files:

```
	`UnrealEditor.exe [GameName or .uproject] -run=cook -targetplatform=[Platform] -cookonthefly -map=[Map Name]`
Copy full snippet
```
UnrealEditor.exe \[GameName or .uproject\] -run=cook -targetplatform=\[Platform\] -cookonthefly -map=\[Map Name\]

The commandlet must be specified via **\-run=cook** and a platform to cook for must be specified. It will generate the cooked data for the platform that is specified and saves it to the following location:

```
	`[UnrealEditor Project]/Saved/Sandboxes/Cooked-[Platform]`

Copy full snippet
```
\[UnrealEditor Project\]/Saved/Sandboxes/Cooked-\[Platform\]

Authoring your command line arguments by hand can be quite involved and has more potential to create accidental errors. Because of this, it is recommended to use a [Custom Launch Profile](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#customlaunchprofile) to accurately generate a Command Line for your build. Any parameters entered in the custom launch profile will automatically generate the Command Line and display it in the **Output Log** window when it is used to cook and build the project. Any text that follows **BuildCookRun** onward can be directly passed as your command line arguments using **RunUAT.bat**.

The following is an example of the generated output from the Project Launcher and the equivalent Command Line that would need to be manually authored to use for **RunUAT.bat**:

-   **Project Launcher Log Window**
    
    ```
              `Automation.ParseCommandLine: Parsing Command Line: -ScriptsForProject=MyProject.uproject BuildCookRun -project=MyProject.uproject -clientconfig=Development`
    		
    Copy full snippet
    ```
    Automation.ParseCommandLine: Parsing Command Line: -ScriptsForProject=MyProject.uproject BuildCookRun -project=MyProject.uproject -clientconfig=Development
-   **Manually Authored**
    
    ```
              `[UnrealEngineRoot]/Engine/Build/BatchFiles/RunUAT.bat BuildCookRun -project=MyProject.uproject -clientconfig=Development`
    		
    Copy full snippet
    ```
    \[UnrealEngineRoot\]/Engine/Build/BatchFiles/RunUAT.bat BuildCookRun -project=MyProject.uproject -clientconfig=Development

For additional information, see the [Content Cooking](/documentation/en-us/unreal-engine/cooking-content-in-unreal-engine) page.

## Content Cooking

In UE, content is stored in particular formats that are supported (PNG for textures data or WAV for audio) for a platform. However, this content may not be in a format that can be used by the platform you are developing for. The process of **Cooking** converts **Assets** used by the UE into ones that can be read on the platforms being deployed to. In some cases, the cooked content is converted to a proprietary format (like with console) that can only be read by by that platform.

Cooking content for different platforms can be done by using [Command Line](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#commandline) or by using the [Project Launcher](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#projectlauncher), and its UE interface. For some platforms, all content must be cooked before it can be used on the device for it to work correctly. You may need to check with the platform you are developing for if this is the case.

There are two ways to cook content for your projects; **By the book** and **On the fly**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/516f1cf3-e9d8-442e-99b3-5829069f7230/08_contentcooking.png)

### Cook By the Book

Cook **By the book (CBTB)** performs the entirety of the cook process ahead of time allowing for the build to deploy the cooked Assets all at once rather than as needed while playing the Level (if you were using a cook server). This option is useful for developers who are not iterating on individual Assets or for those who want the game to perform at full-speed without waiting for a server to deliver the necessary cooked content. Typically, performance testing and playtests will want to use this method.

When performing a CBTB, there is no extra setup required for the build. Use the Project Launcher to [create a Custom Launch Profile](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#customlaunchprofile) and in the **Cook** section, use the drop-down selection to choose **By the book**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76f6b1b2-16d3-4ad0-ad79-304750038347/09_cookbythebooksettings.png)

If you have any game-specific command lines to add, you can expand the **Advanced Settings** and add the arguments to the **Additional Cooker Options**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb39199d-1d81-4bed-a15d-8a4fc7ff6cae/10_additionalcookeroptions.png)

An example would be:

```
	`-nomcp`
Copy full snippet
```
\-nomcp

For additional information about this cook method and its available settings, refer to the [Project Launcher](/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine#bythebook) reference page.

### Cook On the Fly

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8225ffde-5077-470a-a902-3cfe44d65a99/11_cookontheflysettings.png)

When you choose to cook content **On the fly (COTF)**, it will delay cooking it until after the game has been deployed to the platform. Only the executable and some other basic files are installed, which use network communication with a **Cook Server** to make requests on-demand as the content is needed. COTF allows for faster iteration for developers who will be making changes to content regularly or those who will only be exploring sections of the game.

To cook on the fly, you will first need to start a Cook Server on a machine which has the full project available to it. This can be either your local machine or a remote server which performs the cook. The Cook Server can be run by starting the UE in Command Line mode using the following arguments with the **UnrealEditor-cmd.exe**:

```
		`UnrealEditor-cmd.exe [FullAbsolutePathToProject.uproject]-run=cook -targetplatform=Windows -cookonthefly`

Copy full snippet
```
UnrealEditor-cmd.exe \[FullAbsolutePathToProject.uproject\]-run=cook -targetplatform=Windows -cookonthefly

On the developer's local machine, access a [Custom Launch Profile](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#customlaunchprofile) from the Project Launcher and in the **Deploy** Section, set the method to **File Server**. Optionally, you can use the **Default Deploy Platform** to select a single platform or use the toggles to enable multiple platforms to build and deploy to.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c3ce5e7-2aed-4a17-8421-a2ef3da10d31/12_deployfileserver.png)

For the executable to know where to load content from, it needs to be made aware of the IP address of the machine that is running the Cook Server. To do this, you will need to pass the following command line argument on the client's Command Line (where x.x.x.x represents your host's IPs):

```
	`-filehostip=123.456.78.90`

Copy full snippet
```
\-filehostip=123.456.78.90

The argument can be specified in your custom launch profile under the **Launch** section in the **Additional Command Line Parameters** text box. If the IP address is left unspecified, the build will load from existing local files and not attempt to connect to the Cook Server.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/984de0f9-61ab-41ee-8e0f-aafffd1452a5/13_filehostip.png)

For additional information about this cook method and its available settings, refer to the [Project Launcher](/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine#onthefly) reference page.

## Deploying a Build

To deploy a build from the Project Launcher, you must have a project that cooked and packaged. There are a couple of ways you can deploy this type of build to a platform. In your [Custom Launch Profile](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine#customlaunchprofile) under the **Deploy** section, set the way you want to deploy the build.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62509ccf-d859-4111-a7d8-a994890175d9/14_deploybuildtypes.png)

-   **File Server** will cook and deploy the content at runtime as it is needed to the device.
-   **Copy to Device** will copy the entire cooked build to the device.
-   **Do Not Deploy** will not deploy the build to any device once the cook and package complete.
-   **Copy Repository** will copy a build from a specified file location to deploy to any device.

For additional information about this deployment methods and their available settings, refer to the [Project Launcher](/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine#deploy) reference page.