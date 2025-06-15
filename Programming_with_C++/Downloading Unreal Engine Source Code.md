# Downloading Unreal Engine Source Code

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:14

---

Operating System

×Windows

Select an option from the dropdown to see content relevant to it.

This page provides detailed instructions for subscribers to download the source code for **Unreal Engine (UE)** from the Unreal Engine GitHub repository, and to get started working with the code.

Before you can access the repository at [https://github.com/EpicGames/UnrealEngine](https://github.com/EpicGames/UnrealEngine), you must:

-   have an Epic Games account,
    
-   have a GitHub account, and
    
-   have associated your GitHub account with your Epic Games account as described on the [UE on GitHub](https://www.unrealengine.com/ue-on-github) page.
    

You are not required to download the source code to work with Unreal Engine. If you'd rather simply download and install the binary version of Unreal, read our [Installing Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/install-unreal-engine?application_version=5.5) documentation to learn how to [Get Unreal](https://www.unrealengine.com/). However, you may find that having access to the source code can be extremely valuable for you and your project. For example:

-   You will get access to all the latest features and bug fixes that Epic engineers make every day, practically up to the minute.
    
-   If you find a bug that we haven't fixed yet, but that is crucial to your project, you can unblock your project by making the fix in your own version of the source code and rebuilding your own binaries.
    
-   You can improve the engine and help the whole Unreal community by submitting your fixes and features back to Epic.
    

If you are an Unreal Engine licensee, you can access the source code through our Perforce server instead of the public GitHub repository.

## Accessing Unreal Engine Source Code on GitHub

Unreal Engine includes full access to the complete C++ source code, so you can study, customize, extend, and debug the entire Unreal Engine, and complete your project without obstruction.

Our source code repository on GitHub is continually updated as we develop features in our own mainline, so you don’t even have to wait for the next product release to get your hands on the very latest code.

To access Unreal Engine source code, do the following:

1.  Navigate to [GitHub](https://github.com/) and sign up for an account.
    
2.  Sign in to [UnrealEngine.com](https://www.unrealengine.com/) with your verified Epic Games [account](https://accounts.unrealengine.com/). To open your account dashboard, hover over your **username**, and select **Personal** from the drop-down menu.
    
3.  With your account dashboard open, select the **Connections** tab from the sidebar. Select the **Accounts** tab, and then select the **Connect** button below the GitHub icon.
    
4.  If you have not already signed the Unreal Engine End User License Agreement, you will need to read through its terms and select the check box, then select **Link Account**. If you are signed out of your GitHub account, you will be directed to GitHub to sign in after clicking the Link Account button.
    
5.  To complete the OAuth App Authorization process, click the **Authorize EpicGames** button. You can learn more about this process in [GitHub’s overview on Authorizing OAuth Apps](https://docs.github.com/en/apps/oauth-apps/using-oauth-apps/authorizing-oauth-apps).
    
6.  GitHub will send an email inviting you to join the @EpicGames organization on GitHub. You must select the **Join @EpicGames** button in this email within seven days to complete the GitHub and Epic Games account linking process.
    

Upon completion, you will receive an email from Epic Games verifying that your GitHub and Epic Games accounts were successfully linked. If you don’t receive a confirmation email, or if your account is experiencing problems, get help from [Customer Service](https://www.epicgames.com/site/customer-service). You are now ready to get started by going to our [GitHub page](https://github.com/EpicGames/UnrealEngine) (login required) to download the full source code.

## Source Code Branches

You'll notice that we've published UE's source code in several branches.

[![github-branches](https://dev.epicgames.com/community/api/documentation/image/92270d28-fa89-4314-87d5-d637534e1839?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/92270d28-fa89-4314-87d5-d637534e1839?resizing_type=fit)

Branches whose names contain dev, staging, and test are typically for internal Epic processes, and are rarely useful for end-users Other short-lived branches may appear from time to time as we stabilize new releases or hotfixes.

### Release Branch

The **Release** branch always reflects the current official release. These are extensively tested by our QA team, so they make a great starting point for learning Unreal Engine and for making your own projects. We work hard to make releases stable and reliable, and aim to publish a new release every few months.

### Main Branch

Most active development on UE happens in the [ue5-main](https://github.com/EpicGames/UnrealEngine/tree/ue5-main) branch. This branch reflects the latest release of the engine and may be buggy or it may not compile. We make it available for developers who are eager to test new features or work in lock-step development with us.

If you choose to work in this branch, be aware that it is likely to be ahead of the branches for the current official release and the next upcoming release. Therefore, content and code that you create to work with the ue5-main branch may not be compatible with public releases until we create a new branch directly from ue5-main for a future official release.

## Downloading the Source Code

Please follow these instructions to download the Unreal Engine source code.

Refer to our [Setting Up Visual Studio](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine?application_version=5.5) to ensure that you have a version of Visual Studio that is compatible with your desired version of Unreal Engine.

1.  Install [GitHub for Windows](https://windows.github.com/) then [fork and clone our repository](https://guides.github.com/activities/forking/).
    
    To use Git from the command line, see the [Setting up Git](https://help.github.com/articles/set-up-git/) and [Fork a Repo](https://help.github.com/articles/fork-a-repo/) articles.
    
    If you'd prefer not to use Git, you can get the source with the 'Download ZIP' button on the right. The built-in Windows zip utility will mark the contents of zip files downloaded from the Internet as unsafe to execute, so right-click the zip file and select 'Properties...' and 'Unblock' before decompressing it. Third-party zip utilities don't normally do this.
    
2.  Install **Visual Studio**.
    
    All desktop editions of Visual Studio can build UE, including Visual Studio Community, which is free for small teams and individual developers. Refer to the [Setting Up Visual Studio](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine?application_version=5.5) page to ensure that you have downloaded all of the necessary VS components for working with UE.
    
3.  Open your source folder in Explorer and run `Setup.bat`.
    
    This will download binary content for the engine, as well as installing prerequisites and setting up Unreal file associations. On Windows, a warning from SmartScreen may appear. Click **More info**, then **Run anyway** to continue.
    
    A clean download of the engine binaries may take some time to complete. Subsequent checkouts only require incremental downloads and will be much quicker.
    
4.  Run `GenerateProjectFiles.bat` to create project files for the engine. It should take less than a minute to complete.
    
5.  Load the project into Visual Studio by double-clicking on the `UE5.sln` file. Set your solution configuration to **Development Editor** and your solution platform to **Win64**, then right click on the **UE** target and select **Build**. It may take anywhere between 10 and 40 minutes to finish compiling, depending on your system specs.
    
6.  After compiling finishes, you can load the editor from Visual Studio by setting your startup project to **UE5** and pressing **F5** to debug.
    

This page shows Licensees how to download and build Unreal Engine from our source code repository on GitHub. If you'd like to download the binary version of Unreal Engine, read our [Installing Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/install-unreal-engine?application_version=5.5) documentation to learn how to [Get Unreal](https://www.unrealengine.com/).

## Additional target platforms

-   **Android** support will be downloaded by the setup script if you have the Android NDK installed. See the [Android Quick Start](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development) guide.
    
-   **iOS** development requires a Mac. Instructions are in the [iOS Quick Start](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-an-unreal-engine-project-for-ios) guide.
    
-   Development for consoles and other platforms with restricted access, like Sony PlayStation, Microsoft Xbox, and Nintendo Switch, is only possible if you have a registered developer account with those third-party vendors.
    

Depending on the platform, additional documentation or guidance may be available in the Epic Pro Support site, or as a downloadable archive in the section of the [Unreal Engine Forums](https://forums.unrealengine.com/) that is dedicated to your platform.

If you don't have access to these resources, first register a developer account with the third party vendor. Then contact your Epic Games account manager if you have one, or fill out and submit the [Console Development Request](https://epicgames.secure.force.com/Forms/FormConsoleAccessRequest?) form for Unreal Engine if you don't. Epic will contact you with a formal agreement to digitally sign. Once this is approved, you will receive instructions on how to access source code, binaries, and additional instructions for your platform.

## Licensing and Contribution

Your access to and use of Unreal Engine on GitHub is governed by the [Unreal Engine End User License Agreement](https://www.unrealengine.com/eula). If you don't agree to those terms, as amended from time to time, you are not permitted to access or use Unreal Engine.

We welcome any contributions to Unreal Engine development through [pull requests](https://github.com/EpicGames/UnrealEngine/pulls/) on GitHub. Most of our active development is in the **master** branch, so we prefer to take pull requests there (particularly for new features). We try to make sure that all new code adheres to the Epic Games coding standards. All contributions are governed by the terms of the EULA.

## Next Steps

Now that you've downloaded and set-up Unreal Engine, you're ready to [build the engine from source](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source).

#### Footnotes

The first time you start the editor from a fresh source build, you may experience long load times. The engine is optimizing content for your platform to the *derived data cache*, and it should only happen once.

Your private forks of the Unreal Engine code are associated with your GitHub account permissions. If you unsubscribe or switch GitHub user names, you'll need to re-fork and upload your changes from a local copy.