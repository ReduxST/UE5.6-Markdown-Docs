# UGS Troubleshooting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-troubleshooting](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-troubleshooting)  
**Processed:** 2025-06-14 16:57:23

---

For many issues that you experience within **UnrealGameSync (UGS)**, there is a tooltip that gives you more information on what is going wrong with an option you believe should be working correctly.

## Basic Troubleshooting

When you need to ask a question to either Epic or your IT department about Unreal Game Sync, you should include basic information about your setup. This will help get you better, more efficient assistance. Some examples include:

-   Establish if you can reproduce the issue without using UGS. Often, issues that appear to be UGS-related, are not. For example:
    
    -   If there is a crash, try opening the editor without using UGS.
        
    -   If there is a Perforce sync issue, try using only Perforce instead of using it through UGS.
        
-   If you still see the issue without UGS involved, you will need to contact the team or department responsible for where the issue is actually occurring to get better assistance.
    
    -   Establish if you are on the latest version of UGS. Version information can be accessed through either the **Diagnostics** menu (**Main page > Options > Diagnostics...** ), or it can be found in `C:\Users[user]\AppData\Local\UnrealGameSync\` in `UnrealGameSync.log`. This can often be the cause of issues involving metadata and updates to UGS.
        
    -   If you have determined that this is a UGS-specific issue, please refer to the common issues below first.
        

### Troubleshooting Compile Errors

A large number of compile errors can be solved with simple troubleshooting steps:

-   Confirm which step in the Compile failed. For example, UnrealHeaderTool, ShaderCompileWorker, and so on.
    
-   Clean your Workspace through UnrealGameSync, by selecting **More... > Clean Workspace** in the **Project Overview** area. After that, attempt to sync or compile again.
    
-   Delete `UE5.sln`, then manually run `GenerateProjectFiles.bat` (Windows), or `GenerateProjectFiles.command` (Mac), and attempt to sync or compile again.
    
-   Attempt to manually compile using Visual Studio or XCode.
    
-   Attempt to sync or compile a Changelist marked as Good (indicated with a green circle)
    
    -   If failure continues, select **Options > Use Incremental Builds = False**
        
    -   Attempt to recompile
        
-   Ensure **Sync Precompiled Editor** is disabled
    
    Only available in certain streams.
    
-   Confirm the workspace in Perforce has been configured properly.
    
    This can be helpful in a lot of situations, but it does not cover if there are extra files within your workspace. If your workspace gets too complex to manage, you may need to contact your IT department for help, or remake your workspace and re-sync the data for it.
    

## Specific Problems

#### Cannot detect Precompiled Binaries.

-   Detecting PCBs can take a long time. UGS will first load all the CLs, then cross-reference them to see what PCBs are available. On a slower connection, this can take minutes, so be patient.
    
-   If the problem persists, this is likely a result of permissions issues with the stream where they're stored, or they are not getting created/uploaded correctly due to a build health issue. Contact your Perforce administrator and confirm your builds are successfully uploading the precompiled binaries, and that you have access.
    
-   The tooltip shown when hovering over **Sync Precompiled Binaries** will also give more information that is helpful when debugging this issue:
    
    ![Sync Precompiled Binaries tooltip](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3a35714-fed5-4fd6-83d5-9d5cfdef4719/sync-pcb-tooltip.png)

#### Cannot connect.

-   This is typically a Perforce or local network issue. We have seen problems with version 2019.2, and we recommend using a different version to start. Sometimes using P4V to relog into your Perforce server can help.
    
-   If, during a first time setup, you get the following error: `Failed to sync application` And your log contains: `Couldn't find last changelist` Make sure your **Depot Path** is set to the correct Perforce location provided to you by your Perforce administrator, and that the path is properly formatted with the two leading slashes, denoting a Perforce depot, and no terminating forward slash, as shown in the example below: `//depot/path/to/UnrealGameSync/bin` Then click **Connect** again.
    
-   If this is all set correctly, and your Perforce version is not 2019.2, you should contact your Perforce admin to confirm you have permissions for your depot path.
    

#### Failed sync or build due to too-long path.

There is a 260 character path limit on most Windows versions that UGS is unable to circumvent. In fact, if UGS detects a path that will be longer than 260 characters, it will block syncing a project entirely. There is currently no way to disable this check in UGS.

To help with this, you may need to set up your workspace in a folder that is closer to the root (for example, `D:/prj/workspace/` ). Also, try to enforce a file naming structure that shortens your file names as much as possible.

This can also occur in rare instances if you have decided to sync your project using a `.uprojectdirs` file instead of a `.uproject` file. This can be worked around by instead setting up the project in UGS with a `.uproject` file.

1.  Select **Settings**
    
    ![Click settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d801cd59-23d5-4fc5-a100-e8f7cea3dc20/ugs-settings.png)
2.  Select **Browse** for both the **Name** and the **Path** of the Workspace you are using.
    
    -   Workspace Name:
        
        ![Select Browse](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57ab9855-7cc1-4021-9a36-41a801014785/open-proj-browse.png) ![Example Workspace name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8df0cdeb-5f17-4144-b430-b9bfa71af274/example-wrkspc-name.png)
    -   Workspace Path:
        
        ![Workspace Path field and Browse button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1551201a-df25-4b35-b48e-12557316eadb/workspace-path.png)
3.  Instead of selecting a `.uprojectdirs` file like in the setup tutorial, select a `.uproject` file within that stream.
    
4.  Attempt to sync again.
    

#### UGS will not auto-update

-   **Case 1**: This one is typically due to file contention on the machine. This can be solved by closing UGS, confirming there are no active UGS processes running, and deleting `[AppData]/Local/UnrealGameSync/Latest/` which typically contains the files in contention that prevent the update.
    
    If the deletion of that folder fails, you should be shown what file is held in contention and what process is holding on to it. If you are unable to stop that process, rebooting should resolve that issue and allow you to delete that folder.
    
    Afterwards, you can use the UnrealGameSyncLauncher to download the latest update.
    
    You may need to remove UnrealGameSync from your startup applications before restarting, deleting the folder, re-adding UGS to the startup applications, and restarting from there depending on how you set up UGS.
    
-   **Case 2**: If a user either does not have the proper connection, or the proper permissions to see the Perforce path where the UGS updated binaries are, UGS can hang indefinitely, not allowing the user to proceed. If this is the case, either update the **Depot Path** in the connection settings, or speak with your Perforce admin to get the correct access to the files.
    

#### Random Build Errors related to "can not find files".

This is usually a Perforce related error, and not necessarily UGS-related. If your workspace has issues, first try force-syncing the entire engine directory, and if all else fails, create a new workspace.

This can also happen when Sync Filters are not configured properly, either with something important for building getting filtered out (for example, Win64 folders), or a dependency to a file that is covered by a sync filter has been introduced accidentally. Refer to the [UGS Sync Filter Setup](/documentation/en-us/unreal-engine/unreal-game-sync-filters-for-unreal-engine) documentation for more information.

#### Cooking from a UGS copy of the Editor fails.

If you are getting an error similar to,`ERROR: Failed to find command BuildCookRun`, when attempting to cook or package from a precompiled binary version of the engine distributed through UGS, it could be due to needing the source folder for this operation.

Currently, even if you are not actually building the source code, you will need the source directory for cooking and packaging through the precompiled binaries used by UGS. If this is part of your workflow, check your sync filters to make sure you are not excluding the source directory, even if you are not working directly with it.

#### Compiler limit: internal heap limit reached.

If you encounter an error similar to any of the following when compiling:

```
			`Fatal Error C1060: Compiler is out of Heap Space  			Fatal Error C1076: compiler limit: internal heap limit reached; use /Zm to specify a higher limit  			Error C3859: virtual memory range for PCH exceeded; please recompile with a command line option of '-Zm123' or greater`

Copy full snippet
```
Fatal Error C1060: Compiler is out of Heap Space Fatal Error C1076: compiler limit: internal heap limit reached; use /Zm to specify a higher limit Error C3859: virtual memory range for PCH exceeded; please recompile with a command line option of '-Zm123' or greater

You will need to use a workaround.

-   **Short-Term Workaround**: Restart your machine as this clears cached memory and can temporarily unblock a compile.
    
-   **Long-term Resolution**: You should contact your IT department with a description of your problem. In some cases, increasing the maximum page file size through the **Control Panel** may help, but this is something that would need to be done through IT at most studios.
    

#### (Windows) Nothing happens when launching the game or editor, or the editor crashes right away with a weird error.

Most of the time, this occurs on a machine that has not been configured to run Unreal before. If you are on a new machine, have everything synced, and everything else seems to be in working order, but nothing happens when launching, try running the `UEPrereqSetup_x64.exe` application located at:

`<Path to Workspace>/Engine/Extras/Redist/en-us`

This should install the prerequisites needed to run Unreal on a machine that has not done so previously.

#### UGS crashes on launch.

UnrealGameSync uses the P4 Command Line tools to query Perforce for updates. Not having Command Line tools installed is the most common cause of a crash on launch.

To resolve this problem:

1.  Rerun the Perforce Client Installer
2.  During installation, ensure command line tools are included

Check for P4 Command Line tools:

1.  Open a Command window
2.  Enter p4.
3.  Press Enter.
    
    -   If P4 Command Line tools are installed, a series of help commands are printed.
    -   If P4 Command Line tools are not installed, the error message `File not found` is printed,

#### Errors generating project files.

When generating project files, if you encounter an error similar to:

```
			`Setting up Unreal Engine 4 project files... 			UnrealBuildTool Exception: System.FormatException: Index (zero based) must be greater than or equal to zero and less than the size of the argument list. 			at System.Text.StringBuilder.AppendFormatHelper(IFormatProvider provider, String format, ParamsArray args) 			at System.String.FormatHelper(IFormatProvider provider, String format, ParamsArray args) 			at System.String.Format(String format, Object[] args) 			… 			ERROR: UnrealBuildTool was unable to generate project files. Press any key to continue . . . Failed to generate project files (exit code 1).`

Copy full snippet
```
Setting up Unreal Engine 4 project files... UnrealBuildTool Exception: System.FormatException: Index (zero based) must be greater than or equal to zero and less than the size of the argument list. at System.Text.StringBuilder.AppendFormatHelper(IFormatProvider provider, String format, ParamsArray args) at System.String.FormatHelper(IFormatProvider provider, String format, ParamsArray args) at System.String.Format(String format, Object\[\] args) … ERROR: UnrealBuildTool was unable to generate project files. Press any key to continue . . . Failed to generate project files (exit code 1).

This is typically caused by missing Visual Studio Components.

Ensure all Visual Studio Components are installed according to the instructions in the [Visual Studio Setup](/documentation/404) documentation.

If you encounter an error similar to:

`error MSB3644: The reference assemblies for framework ".NETFramework,Version=v4.6.2" were not found.`

Install the [Microsoft SDK and Developer Pack](https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/)

#### Error: System.ComponentModel.Win32Exception

When building using UGS, if the following error appears:

```
			`ubt> Using Visual Studio 2017 14.16.27023 toolchain (C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\VC\Tools\MSVC\14.16.27023) and Windows 10.0.17763.0 SDK (C:\Program Files (x86)\Windows Kits\10).  			ubt> ERROR: System.ComponentModel.Win32Exception (0x80004005): The system cannot find the file specified`
Copy full snippet
```
ubt> Using Visual Studio 2017 14.16.27023 toolchain (C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Professional\\VC\\Tools\\MSVC\\14.16.27023) and Windows 10.0.17763.0 SDK (C:\\Program Files (x86)\\Windows Kits\\10). ubt> ERROR: System.ComponentModel.Win32Exception (0x80004005): The system cannot find the file specified

This is caused by installing the .NET Framework and other developer packages, and trying to sync before restarting the computer.

To correct this problem, restart the computer, generate project files again, and rebuild.

#### Error: System.UnauthorizedAccessException

This occurs typically with versions of UGS that haven't been updated in some time and looks like:

```
	`UnrealGameSync has crashed. 	System.UnauthorizedAccessException:  Access to the path <path> is denied.`

Copy full snippet
```
UnrealGameSync has crashed. System.UnauthorizedAccessException: Access to the path <path> is denied.

To resolve the problem:

1.  Navigate to `C:[user]\AppData\Local\UnrealGameSync`
    
2.  Delete UnrealGameSync.ini
    
    Removing this file will remove user data, including:
    
    -   Saved build configurations.
    -   Editor command line arguments.
    -   Favorited open projects.
    -   Precompiled editor and incremental build elections.
    

#### Could not find any Perforce workspace containing .../.uproject. Check your connection settings.

If you are setting up UGS for the first time and add a project using the local file dialog, but still get the above error:

1.  Try adding the same file through the **Open Project > Workspace > New…** dialog.
    
2.  If you are not able to, this is a Perforce permissions issue and you will need to work with your Perforce administrator to make sure you have the correct access permissions for the stream and files that your workspace targets.
    

#### Connection to server failure.

Attempting to connect to your Perforce server with an unrecognized port number will return the following error:

`Perforce client error: Connect to server failed; check $P4PORT`

To fix this problem:

1.  Open a command/terminal window
    
2.  Enter `p4 set P4PORT=<_local P4 port from admin_>`.
    
3.  Press **Enter**.
    
4.  Close and relaunch UGS.
    

Likewise, connecting with an unknown user will generate the error:

`Access for user 'USERNAME' has not been enabled by 'p4 protect'`

To fix this, open a command window and:

1.  Enter `p4 set P4USER=<perforce.username>`.
    
2.  Press **Enter.**
    
3.  Close and relaunch UGS.
    

#### System.Io.FileNotFoundException: Ionic.Zip.Reduced

Verify that `C:\Users[User.name]\AppData\Local\UnrealGameSync\Latest` contains `Ionic.Zip.Reduced.dll`

-   If it does exist, you are likely missing a file from the workspace and should force sync the `Engine\Binaries` folder in your workspace

Otherwise, check that your anti-virus is not quarantining it. Follow the steps for your anti-virus to "trust" the file

If you're unsure how to do that, proceed as follows:

1.  Terminate UGS from the task manager.
    
2.  Delete the contents of `C:\Users[User.name]\AppData\Local\UnrealGameSync\Latest`.
    
3.  Restart UGS.
    
4.  Confirm after UGS opens that the file now exists.
    

#### UGS is not using the correct proxy server.

If after opening the **Diagnostics** menu (bottom right corner of main window, **Options -> Diagnostics** at the very bottom of the list), the diagnostics menu shows that you're using your proxy server but syncing is still failing, proceed as follows:

1.  Open a new project in UGS
    
2.  Look for **Using default Perforce server settings**.
    
3.  Click on **Change**.
    
4.  Disable **Use default connection settings**.
    
5.  Enter your proxy server and user name in the provided fields.
    
6.  Click **Ok.**
    
7.  Opening the UGS diagnostic should now show the correct server settings.
    
    ![Changing the default Perforce server settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8000df1-a8a2-4bea-82b8-26d3e58e903e/p4-change-defaults.png)