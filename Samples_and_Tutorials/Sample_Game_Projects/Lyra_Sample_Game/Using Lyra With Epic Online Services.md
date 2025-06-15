# Using Lyra With Epic Online Services

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lyra-with-epic-online-services-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lyra-with-epic-online-services-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:44

---

The [Lyra Starter Game](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine) is an example project that is designed for developing and shipping a multiplayer game. It uses its online multiplayer support and integrates with the [Epic Online Services](https://dev.epicgames.com/en-US/services) (**EOS**) backend. However, if you downloaded Lyra from the **Epic Games Launcher**, then it will not work with EOS without some additional setup.

The Lyra Starter Game accesses Epic Online Services functionality inside the Common User Plugin. The Common User Plugin implements EOS functionality using both the Online Subsystem (OSSv1) and Online Services (OSSv2) plugins. The Online Subsystem (OSSv1) implementation is used in Lyra by default. The [Common User Plugin](/documentation/en-us/unreal-engine/common-user-plugin-in-unreal-engine-for-lyra-sample-game) documentation page includes a description of what the plugin does, including how to use OSSv2 for Epic Online Services. You can read more information about the differences between OSSv1 and OSSv2, including when to use each, on the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) documentation page.

## Epic Account and Engine Setup

To use EOS in Lyra, you will need to set up accounts for access to both EOS and the Unreal engine source code:

1.  To test multiplayer, you need at least 2 **Epic Accounts**. You can create a new account by navigating to the [Epic Games Store](https://store.epicgames.com/en-US/) page, then click **Sign In**, and **Sign Up** with a new email address and password.
    
    For efficiency, you can use a second browser to login with your second account.
    
2.  To enable full EOS support, you need one Account that has access to the Unreal Engine source code. Check that your primary Epic Account is synced with **GitHub** as described in [Unreal on GitHub](https://www.unrealengine.com/en-US/ue-on-github).
    
3.  Once you have source code access, follow [Downloading Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine) to download and install the engine source code. Install the **Release branch** of the engine. You can use either **Visual Studio 2019** or **Visual Studio 2022**.
    
    Downloading the source code and running `Setup.bat` can take some time. We recommend you continue with account creation while waiting for the setup to complete.
    
4.  You need to enable **2-factor authentication** on both accounts to gain access to the EOS developer tools. This can be done from the **Account Management** page, by navigating to **Password &** **Security,** or can be prompted when you perform step 5.
    
5.  Both Epic Accounts need access to the [\[EOS Developer Portal\](https://dev.epicgames.com/portal/)](https://dev.epicgames.com/portal/en-US/) (**Dev Portal**). When you navigate to the Dev Portal, a prompt appears to accept licenses and to choose between starting **On your own**, or **As an Organization**. Choose **As an Organization** to create an organization with your primary Account.
    
6.  While you are logged into your primary Account and Organization using the Dev Portal, you will need to add your secondary Account to the Organization. Click the **Organization** section on the left in the **Developer Portal** table of contents, then from the **Team** tab, click the **Invite** button. You are then prompted to fill in the email address of your secondary Account.
    
    The role does not matter for development testing so you can select **Community Tools** before clicking **Invite**. You can rename your **Organization** by clicking **Settings**. Optionally, you can make an organization for your secondary Account, however, it is not necessary for this tutorial.
    
7.  Your secondary Account will receive an invite link in the email. You will need to visit this URL while signing in to your secondary Account.
    
    You can paste the URL into the browser where your secondary Account is already signed in to accept the invite.
    

After accepting the invite, the secondary Account will not be used for anything other than logging in during testing.

## Epic Online Services Product Setup

When you have an Epic Account with Developer access and an Organization, you need to set up a product on the backend to use in your local copy of Lyra. To develop and test Lyra on the PC platform, an additional setup needs to be completed for both EOS and **Epic Account Services (EAS)**.

[Epic Account Services](https://dev.epicgames.com/docs/services/en-US/EpicAccountServices/index.html) provides authentication and social tools designed to integrate with EOS. The use of EAS is not required if you have access to another authentication system provided by a platform or publisher. Lyra uses EAS to handle development login as well as integration with Epic Games Store.

The steps in this section are all performed in the [EOS Dev Portal](https://dev.epicgames.com/portal/) and cover the same information as the [EOS setup guide](https://dev.epicgames.com/en-US/news/how-to-set-up-epic-online-services-eos) and the [Epic Account Services getting started page](https://dev.epicgames.com/docs/services/en-US/EpicAccountServices/GettingStarted/index.html):

1.  First, you need to set up a [Product](https://dev.epicgames.com/docs/services/en-US/DevPortal/ProductManagement/index.html). You can create a new product by selecting **Create Product**. You can then select your product to see the options for the various EOS features.
    
2.  Next, you need to set up a [Client](https://dev.epicgames.com/docs/services/en-US/DevPortal/ClientCredentials/index.html) and **Client policy** for your version of Lyra. From the **Product Settings**, click the **Clients** tab. This prompts you to read and accept legal agreements After doing so, the Clients page displays prompts for additional licenses. For this tutorial, you need to accept the licenses for **Epic Account Services**.
    
3.  Click **Add New Client** to create a new client named "Lyra Test Client". Then click **Add New Client Policy**.
    
4.  In the **Client policy name** field, enter "Peer to Peer client" as it can be reused for multiple products. For the **Client policy type**, select **Peer2Peer** as it provides everything needed by Lyra. Click **Save & Exit** twice to save your new policy and client.
    
5.  To allow the use of EOS for development testing, you need to set up an Application to connect your product with EAS. To use your game with EOS, you need to set up an EOS Application on the service. This links your game with Epic Account Services. To do this, select **Epic Account Services**, This prompts you to read and accept legal agreements. After doing so, click the **Permissions (1)** field of your **Lyra Test Product**. Or, you can click **Create Application (2)** and click the **Permissions** tab in the upper right.
    
    The [Brand Settings](https://dev.epicgames.com/docs/services/en-US/EpicAccountServices/BrandReview/index.html) need to be set up before the release, however, it is not required for development and testing.
    
    ![brand-settings-menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/285b605c-6ada-498d-8fd3-6ece3a027455/brandsettings.png)
6.  On the **Permissions** page, enable both **Online Presence (1)** and **Friends (2)** as Lyra needs them to enable social features. Click **Save Changes (3)**.
    
7.  Select **Linked Clients (1),** then click the drop-down arrow next to **Select Clients** and choose the **Lyra Test Client (2)** to link it to this application, then click **Save Changes(3)**.
    
    You can navigate to the **Product Settings** page and from the **General** tab, scroll down to view all the information you will require later.
    
8.  The final step for EOS setup is to install the [Developer Authentication Tool](https://dev.epicgames.com/docs/services/en-US/EpicAccountServices/DeveloperAuthenticationTool/index.html). This makes multiplayer testing easier because you can log in to each account once instead of having to do a 2-factor authentication check every single time you launch the game.
    

There is a copy of the authentication tool inside the `Engine/Source/ThirdParty/EOSSDK/Tools` folder of your UE5 source installation directory, or it can be found inside the [EOS SDK download](https://dev.epicgames.com/portal/en-US/sdk).

## Installing and Configuring Lyra

You now have a fully downloaded version of the engine and a completely set up EOS product. The steps below walk you through the process of installing, configuring, and building Lyra so it can be used with EOS. These steps are similar to those in the [Lyra documentation](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine).

1.  Open the **Epic Games Launcher** (log in with your primary Account), and select **Unreal Engine** > **Samples**. Click **Lyra Starter Game** and then **Create Project**.
    
2.  Do not accept the default settings. Instead, name your project.
    
    If you are planning on adapting Lyra into another game, you should use that name here.
    
3.  Select the root folder where you installed your engine source code. click **Browse** to select that folder, then click **Create** to download the project. After this, you should have both an Engine subfolder and a subfolder matching the project name (LyraStarterGame by default) you just selected.
    
4.  You will need to install the **UnrealVS** extension located in the `Engine/Extras/UnrealVS` folder. This provides you with easy management of the startup project and command line parameters inside of Visual Studio.
    
5.  Navigate to the root of your engine source code, then install and run GenerateProjectFiles.bat to create a new solution file called UE5.sln. Double-click that file to load Visual Studio. After a loading time, your version of the LyraStarterGame is listed in the **Solution Explorer** under the **Games** category (including LyraGameEOS).
    
6.  Right-click LyraStarterGame, select **Set As Startup Project** then [build it](/documentation/en-us/unreal-engine/compiling-game-projects-in-unreal-engine-using-cplusplus).
    
    This will compile Lyra and all the engine features required and may take a while. If you have any compile errors, you need to resolve them before continuing.
    
7.  Once Lyra has been built from source, you can run it from the **Debug menu** and explore the project sample.
    
8.  You need an additional set-up so the project is configured for EOS. Lyra comes with EOS-specific config files that are enabled using the **CustomConfig** feature of the [Common User Plugin](/documentation/en-us/unreal-engine/common-user-plugin-in-unreal-engine-for-lyra-sample-game). To do this, you need to modify the `DefaultEngine.ini` located in the `Config/Custom/EOS` folder inside your project. Online Services and Online Subsystem have different configuration methods.
    
    -   To configure Online Subsystem (OSSv1), open the file and search for the following line:
        
        ```
              `;For OSSV1, fill in the following line with actual details and then uncomment       ;+Artifacts=(ArtifactName="ARTIFACTNAME",ClientId="CLIENTID",ClientSecret="CLIENTSECRET",ProductId="PRODUCTID",SandboxId="SANDBOXID",DeploymentId="DEPLOYTMENTID",EncryptionKey="ENCRYPTIONKEY")`
        Copy full snippet
        ```
        ;For OSSV1, fill in the following line with actual details and then uncomment ;+Artifacts=(ArtifactName="ARTIFACTNAME",ClientId="CLIENTID",ClientSecret="CLIENTSECRET",ProductId="PRODUCTID",SandboxId="SANDBOXID",DeploymentId="DEPLOYTMENTID",EncryptionKey="ENCRYPTIONKEY")
        -   For more information about configuring Online Subsystem EOS, see the [Online Subsystem EOS Plugin](/documentation/en-us/unreal-engine/online-subsystem-eos-plugin-in-unreal-engine#artifactsettings) documentation.
    -   To configure Online Services (OSSv2), open the file and search for the following lines:
        
        ```
              `;For OSSv2, fill in the following lines with actual details and then uncomment       ;+[OnlineServices.EOS]       ;+ProductId=PRODUCTID       ;+SandboxId=SANDBOXID       ;+DeploymentId=DEPLOYTMENTID       ;+ClientId=CLIENTID       ;+ClientSecret=CLIENTSECRET`
        Copy full snippet
        ```
        ;For OSSv2, fill in the following lines with actual details and then uncomment ;+\[OnlineServices.EOS\] ;+ProductId=PRODUCTID ;+SandboxId=SANDBOXID ;+DeploymentId=DEPLOYTMENTID ;+ClientId=CLIENTID ;+ClientSecret=CLIENTSECRET
        
        -   For more information about enabling OSSv2 and disabling OSSv1 in Lyra, consult the [Using the Online Services Plugin](/documentation/en-us/unreal-engine/common-user-plugin-in-unreal-engine-for-lyra-sample-game#usingtheonlineservicesplugin) section of the [Common User Plugin](/documentation/en-us/unreal-engine/common-user-plugin-in-unreal-engine-for-lyra-sample-game) documentation.
        -   For more information about configuring Online Services EOS, see the [Enable and Configure Online Services EOS](/documentation/en-us/unreal-engine/enable-and-configure-online-services-eos-in-unreal-engine#epiconlineservices) documentation.
        
        Unreal Engine configuration files (`.ini`) use a semicolon (`;`) at the beginning of a line to denote a comment. To uncomment a line in an engine configuration file, remove the semicolon (`;`) at the beginning of the line.
        
9.  After modifying the configuration files, save your changes.
    

## Testing EOS in an Editor Build

You can now begin the steps to test the game in the editor and packaged builds.

1.  Inside **Visual Studio**, enable the **UnrealVS toolbar**, and add the following line to the command line section:
    
    ```
         `-game -customconfig=EOS`
    Copy full snippet
    ```
    \-game -customconfig=EOS
2.  Debug the project to launch with the new command line, this launches in standalone game mode and uses the EOS config files. When finished, an error message displays "Login Failure Not Implemented".
    
3.  Click **OK** and the Lyra main menu will load. This error message means your project is trying to use EOS but is failing to log in because you did not specify enough information on the command line. If you do not see a login failure error message, there may be an error with the config file, therefore you should search the output log for any errors related to EOS.
    
4.  Now, run the **Developer Authentication Tool** you unzipped in the **Epic Online Services Product Setup** step. When you run the **EOS\_DevAuthTool** program, it prompts you for a **port** to use, enter **6666**.
    
    On Windows, you may receive an additional prompt asking for firewall access. You need to allow access.
    
5.  Next, click **Login** to open an embedded browser where you can log in with your primary Epic Account. After entering your two-factor code, it prompts you for a **Credential name**, enter "Player1" or something similar.
    
6.  Repeat this process for your secondary Account, but give it a different credential name like "Player2". Your two Accounts will stay logged into the EOS backend for that testing session. Eventually, you will need to reboot the dev tool and log in again to refresh the authentication.
    
7.  Navigate back to **Visual Studio** and add the following options to your command line in **UnrealVS**:
    
    ```
         `-AUTH_LOGIN=localhost:6666 -AUTH_PASSWORD=Player1 -AUTH_TYPE=developer`
    Copy full snippet
    ```
    \-AUTH\_LOGIN=localhost:6666 -AUTH\_PASSWORD=Player1 -AUTH\_TYPE=developer
    
    However, you need to replace the port and credential name with the one you picked above. For example, the full command line at this point could be:
    
    ```
     `LyraStarterGame -game -customconfig=EOS -AUTH_LOGIN=localhost:6666 -AUTH_PASSWORD=Player1 -AUTH_TYPE=developer.`
    Copy full snippet
    ```
    LyraStarterGame -game -customconfig=EOS -AUTH\_LOGIN=localhost:6666 -AUTH\_PASSWORD=Player1 -AUTH\_TYPE=developer.
8.  Click **Debug** to launch the game again. This time, it uses the extra info on the command line to log in to EOS. A browser window opens to warn you about an unverified application, this is because of the incomplete Brand Settings. Click accept twice to authorize linking the Application to your Epic Account. This takes you back into the game and displays the main menu with no error message. Press **shift**+**F3** to open the Epic Account overlay that indicates you are fully logged in.
    
9.  This account is the host for your multiplayer game, so click **Play Lyra** then **Start a Game** to load the hosting screen. Ensure **Network** is set to **Online**, then select **Elimination** to start the match.
    
    You may want to set your graphics quality to Low and enable windowed mode in the settings menu to make sure your computer can handle two copies of the game.
    
10.  Return to **Visual Studio** and detach this client from the **Debug** menu. Prepare your secondary account login by changing the -AUTH\_PASSWORD value in the command line in UnrealVS to the second credential name (Player2). Click **Debug** to launch the game again. When the second instance starts, you are prompted to authorize the Application for your second Account, and then shown the main menu.
    
11.  To ensure everything is working, click **Browse** to show the **Server Browser,** and check the game hosted by your first instance of the game is still running.
    
12.  Select the game. If you join the game successfully then the process is complete. You are now in a multiplayer game with 2 players(and bots).
    

## Packaging LyraGameEOS

After you verify that EOS works in a development editor build, you can follow additional steps to create a packaged version of **LyraGameEOS**.

These steps only work if you followed the full process of installing Lyra into a copy of the engine built from the source code, as the launcher-installed version is not capable of customizing the build process.

1.  Set up your project in a **Development** build and load the editor to create a packaged EOS version of the game.
    
    You can clear the command line after the project name, UnrealVS will keep a history of command lines in the dropdown menu.
    
2.  Once the editor loads, Navigate to the toolbar, click **Platforms** > **Windows** > **Build Target**, then select **LyraGameEOS** to build a customized version of the game that bakes the `-CustomConfig=EOS` setting into the executable.
    
3.  Navigate to the **Toolbar > Platforms > Windows > Package Project** to choose an output directory. Once you select a directory it will start the cook and package process.
    
    Check the output log for any errors.
    
    If packaging Lyra fails and the log shows an error message related to UAT, you may be encountering a bug that was present in the original 5.0 release of the Lyra game sample. This can be fixed by downloading the Lyra sample for the 5.0.2 (or later) version of the sample or installing Lyra into a `Samples/Games` subfolder of your engine base install (`C:\UE5\Samples\Games\LyraStarterGame`).
    
4.  If the cook and package process succeeds, it places a packaged copy of the game in the directory you selected. This packaged build can be zipped up and sent to another computer for real-world multiplayer testing.
    

If you run this packaged build from the Epic Games Store, it passes the correct user credentials in. However, for development testing you need to make a shortcut or batch file and add the command line:

```
`-AUTH_LOGIN=localhost:6666 -AUTH_PASSWORD=Player1 -AUTH_TYPE=developer`
Copy full snippet
```
\-AUTH\_LOGIN=localhost:6666 -AUTH\_PASSWORD=Player1 -AUTH\_TYPE=developer

## Next Steps

After following these steps, you now have a fully working version of Lyra usable for multiplayer development and testing using EOS. With a working version of an EOS-enabled Lyra Game sample, you can use it as a base for other development tasks with the eventual goal of releasing your game. To adapt the Lyra multiplayer code for another existing game, you can either build your game on top of the entire Lyra code base, or you can copy the [CommonUser](/documentation/en-us/unreal-engine/common-user-plugin-in-unreal-engine-for-lyra-sample-game) plugin and config files into your own game as described in the documentation.

Lyra was designed to work on all supported console, mobile, and PC desktop platforms, however, the current version of the sample was primarily tested on PC using an internal version of the Epic Games Store. To prepare for publishing your own game on the [Epic Games Store](https://dev.epicgames.com/docs/services/en-US/EpicGamesStore/index.html), we recommend you work with your publisher to complete the [Brand Review](https://dev.epicgames.com/docs/services/en-US/EpicAccountServices/BrandReview/index.html) process and start a conversation with the publishing team.

If you need help developing a cross-platform version of the game or have issues with the EOS setup steps in this tutorial, you can create a discussion on the [EOS Community Forums](https://eoshelp.epicgames.com/s/) or contact EOS support.