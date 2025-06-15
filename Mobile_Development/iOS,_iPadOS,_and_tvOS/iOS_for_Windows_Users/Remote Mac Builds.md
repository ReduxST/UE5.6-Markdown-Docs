# Remote Mac Builds

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-remote-builds-of-unreal-engine-projects-for-ios](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-remote-builds-of-unreal-engine-projects-for-ios)  
**Processed:** 2025-06-14 16:17:45

---

Creating a signed build for iOS requires a Mac and an Apple Developer account. However, for teams that primarily use Windows machines, **Unreal Engine** can establish an **SSH connection** between a Windows PC and up to two Macs to create iOS builds remotely. This requires you to allow incoming SSH connections on your Mac, and then you need to set up the SSH key and credentials to access the Mac on your Windows machine. This guide will walk you through the process of setting up your connection and running a remote build.

### Primary and Secondary Remote Mac

You can find the settings for remote Macs in **Project Settings** > **Platforms** > **iOS**, under the **Remote Build** section.

![The remote build settings for iOS](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b22df28-43a5-47a8-b346-450a80855f2c/remotebuildsettingsupdated.png)

This section lists both **Remote Build Options**, which is intended for your primary remote build Mac, and **Secondary Remote Build Options**, which is intended for your secondary remote build Mac.

Your primary Mac should be a model with high processing power, such as a Mac Pro, which can act as a shared resource for your team. This is the Mac you will use to handle major build processes that require a Mac with Xcode.

Your secondary Mac should be a personal device to launch debugging builds on your test devices. The secondary Mac does not build anything. Instead, it downloads cached data you have already built on your primary Mac and sets up Xcode project files for debugging. This means it can have more modest specifications than your primary Mac, as it does not need to run a full build or cook for your project -- it only needs to launch on your specified iOS, tvOS, or iPadOS device. For details on how to handle this process, refer to Using a Remote Secondary Mac below.

### Prepare for Debugging

The **Prepare for Debugging** command injects previously-cooked data into your builds from Xcode, producing a `.ipa` file you can use to launch on your target device from Xcode. This streamlines the debugging pipeline for projects in two ways:

-   Prepare for Debugging automatically handles creating a debugging build without needing to reconfigure your Xcode project.
    
-   Projects with only a small number of macs can import cooked data from other machines. This makes it possible to skip building or using Unreal Editor and simply launch a build from Xcode.
    

Prepare for Debugging is designed for streamlining remote builds, particularly when using a secondary Mac. See [Debugging iOS Projects in Xcode](/documentation/en-us/unreal-engine/debugging-ios-projects-with-xcode-in-unreal-engine) for more details about how to use this command.

## 1\. Required Setup

To use iOS remote builds, you need at least one Mac capable of building your iOS project, as well as at least one Windows PC. Both machines must have an internet or local area network connection. The Mac does not need to have a copy of your project or Unreal Engine installed to work, as it only requires Xcode for signing and compilation.

Your Windows machine must have **iTunes** installed to ensure you have the necessary binaries for iOS projects. We recommend that you download and install iTunes from [Apple's web site](https://www.apple.com/itunes/) rather than from the Windows Store, as the Windows version includes extra binaries that sometimes interfere with the remote-build process. To obtain iTunes directly from Apple, scroll down to the section labeled "Looking for other versions?" and click **Windows**.

Your Mac must have your iOS Developer Certificates installed to the **System Keychain**, and you must set up your Provisioning Profile for your project, per the [iOS Provisioning](/documentation/en-us/unreal-engine/setting-up-ios-tvos-and-ipados-provisioning-profiles-and-signing-certificates-for-unreal-engine-projects) setup.

Once you have set up your Mac to create builds for your project, you should run a build directly on that machine at least once to ensure that it works before proceeding to the next section.

## 2\. Enabling Remote Login On Your Mac

Once you have set up your project, you will need to configure your Mac to allow SSH connections.

1.  Open your Mac's **System Preferences**, then navigate to **Sharing**.
    
2.  Check the box for **Remote Login**.
    
3.  Open System **Preferences** > **Network**.
    
4.  Note the computer's **IP Address**. You will need this for setting up the remote connection on your Windows PC.
    

Once you have completed these steps, your Mac will be able to accept an incoming SSH connection from your PC.

## 3\. Windows Configuration and Generating Your SSH Key

Complete the following steps on your Windows machine to configure it for remote iOS builds.

1.  Open your project in **Unreal Editor**, then open **Project Settings**.
    
    ![Locating the project settings in the Edit menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72027ed0-f7f2-4ca7-9e36-73341ec241d8/menu_project_settings.png)
2.  Navigate to **Platforms** > **iOS** > **Build**.
    
    ![The Platforms/iOS section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea929475-c2c3-4bcd-ad90-92afd0922be4/iossettings.png)
3.  In the **Remote Server Name** field, enter either the name of the Mac you are using to build the project, or its IP address.
    
4.  In the **Remote User Name** field, enter the username that you would normally use to log in to the Mac.
    
5.  Click **Generate SSH Key**. This will open a Command Prompt window with a series of prompts that will generate the SSH key.
    
6.  If you receive a message that your host could not be authenticated, enter "**yes**" in the prompt to continue.
    
7.  Enter the **password** that belongs to the user you specified in **Remote User Name** in the previous section.
    
8.  The prompt will ask you for a **passphrase**. If you choose not to enter a passphrase, you can use the remote connection without requiring any user interaction.
    
9.  When prompted, enter the **password** and **username** for the Mac again to complete the process.
    

Now that you have generated an SSH key, you will be able to start a remote connection on your Windows machine to your Mac for creating iOS builds.

### Workaround For Unprotected Private Key

You might see an error that reads as follows:

```
	`ERROR: Unable to determine home directory for remote user. SSH output:...WARNING: UNPROTECTED PRIVATE KEY FILE!...0660`
Copy full snippet
```
ERROR: Unable to determine home directory for remote user. SSH output:...WARNING: UNPROTECTED PRIVATE KEY FILE!...0660

If you do not see this error, you can proceed with the next step (**Optional Team Setup**). If you do see this error, use the following steps to resolve it:

1.  Navigate to your `RemoteToolChainPrivate.key`.
    
2.  Right-click the file and select **Properties**.
    
3.  Click the **Security** tab.
    
4.  Click **Edit**.
    
5.  Remove all group or user names.
    
6.  Click **Add**.
    
7.  Click **Object Types**. Make sure all boxes are checked, then click **OK**.
    
8.  In the text box, type **Users**, then press Enter.
    
9.  Make sure that permissions for Users are set to **Read** and **Read & Execute**.
    

This will change the file's primary group so that it is not the same as your username, which is what confuses SSH when it checks group permissions. The process should then work as normal.

SubInACL could previously be used for this purpose, but is no longer available from Microsoft.

## 4\. Optional Team Setup

To share this data for other projects in the future, specify the Remote Server Name and Remote User Name in one of the `*Engine.ini` files on your computer.

1.  Select the button next to the **Remote Server Name** property to open the **Configuration Editor**.
    
    ![The config editor button next to the Remote Server Name property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e52d9483-111f-4ec2-870c-1a3d2c30d25b/configfiles.png)
2.  Set the properties for each individual .ini file for which you want to share the SSH data.
    
    ![Editing the .ini files with the config editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ae28fbd-6dcc-405a-914a-c6cc28a97d26/inifileexample.png)
3.  Repeat these steps for **Remote User Name**.
    

By sharing these .ini files, you can keep the SSH information available for multiple projects or users. The SSH keys themselves are stored in the `Engine/Build/SSHKeys` folder. You can check this directory into your source control system to share them with your team.

## 5\. Final Result

After completing the above steps, you can initiate a remote build by clicking **Platforms** > **iOS** > **Package Project** or **Platforms** > **iOS** > **Prepare for Debugging** in Unreal Editor on your Windows machine. It will open a SSH connection and send the command to your Mac to begin making a build. Your build appears in a directory

## 6\. Use a Secondary Remote Mac

There are a few more steps you need to use the secondary Mac, as it uses existing build data from the primary Mac to skip the build process.

### Prepare for Debugging on Your Windows Machine

1.  On your Windows machine, open **Project Settings** > **Platforms** > **iOS**, then under the Remote Build section, make sure **Enable Secondary Remote Mac** is **disabled**.
    
2.  Build your project using the primary remote Mac. You must do this at least once to use your secondary Mac, as it depends on the files created by the primary Mac.
    
3.  Once you have completed at least one build on the primary Mac, enable the **Enable Secondary Remote Mac** setting.
    
4.  Click **Platforms** > **iOS** > **Prepare for Debugging**. This time, after completing the remote build on the primary Mac, the Windows machine will download its build data and send it to the secondary Mac.
    

You now have an Xcode project on the secondary Mac with cached data from the other machines. It is in a directory identical to the project directory created on the Primary Mac. The first attempt to use the secondary remote mac process usually takes 10-15 minutes to synch data between all three of your machines, but each subsequent build, it should only take about 30 seconds or so.

### Debug on the Secondary Remote Mac

To debug on the secondary remote Mac:

1.  Open the directory containing the generated Xcode project files, then open the Xcode solution.
    
2.  Configure Xcode as you would in the normal [Xcode debugging workflow](/documentation/en-us/unreal-engine/debugging-ios-projects-with-xcode-in-unreal-engine).
    
3.  You already have cached build data, therefore you don't need to run a full build. Instead, click **Product** > **Perform Action** > **Run Without Building** to launch on your iOS, iPadOS, or tvOS test device.
    
    ![Run Without Building](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6046d6c9-729f-4ce7-bdb5-782206a93e96/runwithoutbuilding.png)

Your project will launch on the iOS device.