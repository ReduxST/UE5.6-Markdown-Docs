# UGS Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-reference-guide-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-reference-guide-for-unreal-engine)  
**Processed:** 2025-06-14 16:57:22

---

This page describes how to configure **UnrealGameSync (UGS)** for deployment as a studio.

## Orientation

The source code for UnrealGameSync is under `Engine/Source/Programs/UnrealGameSync`.

The UnrealGameSync solution consists of the following projects:

| Project | Description |
| --- | --- |
| **UnrealGameSync** | The main program. |
| **UnrealGameSyncLauncher** | Launcher for UGS, which automatically updates the main program executable when a new version is available. |
| **MetadataServer** | 
REST API that deploys alongside UGS to enable its full feature set, including commenting on builds, voting on build health and marking bad builds, and displaying **Continuous Integration System (CIS)** results submitted by PostBadgeStatus.

The Metadata Server must be deployed to the Windows Server machine with IIS 7.0 or higher and .NET 4.6.2 installed.



 |
| **Installer** | 

MSI installer for UnrealGameSyncLauncher. This is typically used to get the launcher on developer machines, which can then automatically update and run the program from Perforce.

Requires Wix 3.8 to build.



 |
| **PostBadgeStatus** | Utility to push build results to a MetadataServer instance. |

## Configuration

Deployment settings for UGS are specified in `Engine/Source/Programs/UnrealGameSync/UnrealGameSync/DeploymentSettings.cs`. You can modify this file with settings for your own team, then compile them into the executables you distribute.

These settings are:

| Setting | Description |
| --- | --- |
| `ApiUrl` | URL of a running instance of the metadata service (see below) used to surface information to developers. |
| `DefaultDepotPath` | 
The default Perforce depot path that UnrealGameSyncLauncher should sync UnrealGameSync executables from.

See below for how this folder should be laid out.



 |
| `bSendTelemetry` | Whether to post telemetry about build times to the metadata service. |

## Auto-Update

To enable development on UGS out of band with different branches and projects, we distribute UGS via a self-patching mechanism that leverages Perforce for versioning.

A rarely updated launcher application is manually installed on each developers machine (UnrealGameSyncLauncher) using a Microsoft Installer (MSI) package (the 'Installer' project). Installing this creates a start-menu icon, and running it syncs the latest UGS executables from Perforce and runs them. That path is monitored, and if new executables are submitted, the program restarts and re-syncs them.

No workspace is required for these files to be synced; they are fetched from the Perforce server in a stateless way.

Wix 3.8 is required to build the installer.

The path that UnrealGameSyncLauncher uses to update the application is specified by the `DefaultDepotPath` variable compiled into the application via `DeploymentSettings.cs` (link above). This folder should be laid out as follows (example for `DefaultDepotPath = "//depot/UnrealGameSync"`):

`//depot/UnrealGameSync/`**Release/UnrealGameSync.exe** `//depot/UnrealGameSync/`**Release/UnrealGameSync.exe.config** `//depot/UnrealGameSync/`**Release/UnrealGameSync.pdb** `//depot/UnrealGameSync/`**Release/Ionic.Zip.Reduced.dll**

`//depot/UnrealGameSync/`**UnstableRelease/UnrealGameSync.exe** `//depot/UnrealGameSync/`**UnstableRelease/UnrealGameSync.exe.config** `//depot/UnrealGameSync/`**UnstableRelease/UnrealGameSync.pdb** `//depot/UnrealGameSync/`**UnstableRelease/Ionic.Zip.Reduced.dll**

There are two copies of UnrealGameSync checked in — one under the "Release" folder, and a second under the "UnstableRelease" folder.

The executable under the `Release` folder is used by default, but the `UnstableRelease` folder can be used to distribute test builds to users that opt in to it via the **Application Settings** dialog in UGS, or by holding down the shift key while starting the launcher.

New versions of UnrealGameSync can be pushed out simply by submitting new executables. The application will poll the folder for submitted changes, and restart and re-sync the binaries if any new changes are found.

## Setting Up the Metadata Service

UGS can communicate with a web service to share information between team members. While it can run without this being set up, some of the more powerful collaboration features will not be available:

-   Surfacing build results and providing desktop notifications for build breakages
-   Allowing users to mark changes as good and bad, and indicate to other team members that they're investigating a problem with the build
-   Showing which users are synced to which changes

The metadata service is implemented with ASP.NET and requires setting up a MySql instance for the database backend.

It is recommended to host an IIS instance with the MetadataServer and the database backend on separate machines, as the database process should (ideally) be available to consume all available machine resources — however, this is not necessary.

### Setting up the MySql Backend

Before continuing, note that the minimum requirement is [MySQL 8.0](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/).

To set up the MySql backend, perform the following steps:

1.  Download the newest version of the MySql installer: [https://dev.mysql.com/downloads/installer/](https://dev.mysql.com/downloads/installer/)
    
2.  On **Choosing a Setup Type**, select **Server Only**.
    
3.  In the **Configuration Steps**, set:
    
    1.  **High Availability**: Standalone MySql Server
    2.  **Type and Networking**: Either **Server Computer** if sharing with the IIS instance as mentioned above, or **Dedicated Server** if it is on a separate instance. Leave all the TCP/IP configuration and ports as their defaults.
    3.  **Authentication Method**: Use Strong Password Encryption
    4.  For **Accounts** and **Roles**:
        1.  Pick a root username and password. Do not lose the password because this is the master account to the database.
        2.  Add another user as a service account that your IIS instance will use to connect. Do not use the root account.
    5.  **Windows Service** (assuming the installation is on a Windows machine): You can leave these options alone.
    
    Install MySql Workbench on your local workstation: [https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/). With MySQL Workbench, you can view and manipulate the database. Also, you can perform administrative tasks such as backups and restores.
    

#### Troubleshooting

##### Disabling ONLY\_FULL\_GROUP\_BY

If you enable the `ONLY_FULL_GROUP_BY` function, you may run into errors while running the MySQL script. You can disable this function by either running a command (Method 1) or by modifying the MySQL option file (Method 2).

###### Method 1: Running a Command

Start MySQL server from the command-line and run:

```
	`mysql > SET GLOBAL sql_mode=(SELECT_REPLACE(@@sql_mode, 'ONLY_FULL_GROUP_BY', ''));`

Copy full snippet
```
mysql > SET GLOBAL sql\_mode=(SELECT\_REPLACE(@@sql\_mode, 'ONLY\_FULL\_GROUP\_BY', ''));

If you are a Windows user experiencing difficulty running MySQL server from the command-line, read the MySQL 8.0 Reference Manual, [Starting MySQL from the Windows Command Line](https://dev.mysql.com/doc/refman/8.0/en/windows-start-command-line.html).

###### Method 2: Modifying the Option File

**Required:** If you do not know how to use MySQL options files, read the MySQL 8.0 Reference Manual, [Using Option Files](https://dev.mysql.com/doc/refman/8.0/en/option-files.html).

1.  Locate and open the `my.cnf` option file.
2.  Run this query to check `sql_mode`:
    
    ```
             `SELECT @@sql_mode;`
    		
    Copy full snippet
    ```
    SELECT @@sql\_mode;
3.  Review the query result, which should be similar to these values:
    
    ```
             `ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION`
    		
    Copy full snippet
    ```
    ONLY\_FULL\_GROUP\_BY,STRICT\_TRANS\_TABLES,NO\_ZERO\_IN\_DATE,NO\_ZERO\_DATE, ERROR\_FOR\_DIVISION\_BY\_ZERO,NO\_ENGINE\_SUBSTITUTION
4.  Edit `my.cnf` by entering the following `sql_mode` statement (under \[mysqld\]) with the values from the previous step:
    
    ```
             `sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION`
    		
    Copy full snippet
    ```
    sql\_mode=STRICT\_TRANS\_TABLES,NO\_ZERO\_IN\_DATE,NO\_ZERO\_DATE, ERROR\_FOR\_DIVISION\_BY\_ZERO,NO\_ENGINE\_SUBSTITUTION
    
    Note that the statement does not include the `ONLY_FULL_GROUP_BY` value.
    
5.  Restart the MySQL server.

For additional information, check out these MySQL 8.0 Reference Manual sections:

-   Server [SQL Modes](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html)
-   MySQL [Handling of GROUP BY](https://dev.mysql.com/doc/refman/8.0/en/group-by-handling.html)

### Setting up the Metadata Service

To set up the metadata service, perform the following steps:

-   Modify UGS executable to set ApiUrl

1.  Ensure that ASP.NET Web Publishing tools are installed. You can find this package in the Visual Studio installation. If you don't have this package installed, building the project will fail with a "TransformXml task not found" error.
2.  The project does not ship with a traditional `web.config` file, but instead comes with a `web.template.config.xml`, which is transformed against the `.debug` and `.release` XML files to dynamically produce a `web.config`. You want to check the `web.template.config` into source control, not `web.config`.
3.  In the `.debug` and `.release` XML files, you can specify the path for where the MySql database will live via the "Connection String" property. This will look like a standard MySql Connection string:
    
    ```
             `<add name="ConnectionString" connectionString="server=localhost;UserId=service_account_username;password=service_account_password;" providerName="MySql.Data.Client"/>`
    		
    Copy full snippet
    ```
    <add name="ConnectionString" connectionString="server=localhost;UserId=service\_account\_username;password=service\_account\_password;" providerName="MySql.Data.Client"/>
    
    `service_account_username` and `service_account_password` are the account credentials entered during the MySql setup process.
    
4.  The database is seeded automatically the first time the site is launched.

To verify that the server is configured correctly, open `servername.com/api/latest` in a web browser. You should see something like this:

```
	`<LatestData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/MetadataServer.Models"> 	  <LastBuildId>0</LastBuildId> 	  <LastCommentId>0</LastCommentId> 	  <LastEventId>0</LastEventId> 	</LatestData>`

Copy full snippet
```
<LatestData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/MetadataServer.Models"> <LastBuildId>0</LastBuildId> <LastCommentId>0</LastCommentId> <LastEventId>0</LastEventId> </LatestData>

To ensure that the database initializes properly, the site will terminate if it cannot be created or found. If you deploy your site and receive a 404 error, this is likely the reason. Check your connection string and if on separate instances, the IIS instance can communicate with the database.

## Integrating with your Build Process

### Badges

UGS can surface build system results (and notifications that a build is "in progress") via **Badges** shown in the list of submitted changelists. If the build breaks, it will show a notification to developers that have submitted since it last succeeded. Clicking on a badge opens a web browser at a URL containing the build log.

This information is stored by the Metadata Service, and entries can be added to it using the PostBadgeStatus utility.

### PostBadgeStatus

The command-line syntax for `PostBadgeStatus` is as follows:

```
	`PostBadgeStatus.exe 	    //(The badge name that will appear in UGS.) 	  -Name=Editor 	    //(The changelist being compiled.) 	  -Change=123456 	    //(The project to show the badge for. Note that this is the path to a folder, not the actual .uproject file.) 	  -Project=//UE4/Main/Samples/StarterContent 	    //(The base URI where UGSAPI is deployed) 	  -RestUrl="http://ugsapi-server.net" 	    //(The status of the build. Valid values are 'Starting', 'Failure', 'Warning', and 'Success'.) 	  -Status=Success 	    //(If a user clicks on a badge, this is the link that takes the user to the build log.) 	  -Url=http://link-to-build-log`

Copy full snippet
```
PostBadgeStatus.exe //(The badge name that will appear in UGS.) -Name=Editor //(The changelist being compiled.) -Change=123456 //(The project to show the badge for. Note that this is the path to a folder, not the actual .uproject file.) -Project=//UE4/Main/Samples/StarterContent //(The base URI where UGSAPI is deployed) -RestUrl="http://ugsapi-server.net" //(The status of the build. Valid values are 'Starting', 'Failure', 'Warning', and 'Success'.) -Status=Success //(If a user clicks on a badge, this is the link that takes the user to the build log.) -Url=http://link-to-build-log

## Customizing for your Project

### Branding

You can add a project logo to be displayed in UGS by placing a `Build\UnrealGameSync.png` file in the directory containing your project. The image will be scaled to a height of 126 pixels.

We recommend pixel dimensions of 200x126. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72bc0fe0-71c1-483d-bbca-3360ac16f932/brandpxdim.png "BrandPxDim.png")

*Feel free to download this reference image.*

### Project Config Files

You can customize the way that a project is presented to users with a project-specific config file. Project config files should be submitted to Perforce as `<ProjectDir>/Build/UnrealGameSync.ini`.

The following settings are available:

-   By default, UGS only displays build failure notifications resulting from changes to the project's source code. If you have any badges that should be shown to developers submitting content, allow them as follows:
    
    ```
              `[Notifications]           +ContentBadges=Content`
    		
    Copy full snippet
    ```
    \[Notifications\] +ContentBadges=Content
-   If you add clickable buttons to a CL's description column, the corresponding buttons, when clicked, take users to a URL by running a regular expression over the CL description. For example, the following use case adds a badge next to every CL with a `#jira` tag with a link to the corresponding issue in Jira:
    
    ```
              `[Badges]           +DescriptionBadges=(Pattern="(?i)#\\s*jira\\s*:?\\s+([A-Za-z]+-[0-9]+)", Name="$1", Group="Jira", Color="#c0c0c0", HoverColor="#e0e0e0", Url="https://jira.it.yourcompany.net/browse/$1")`
    		
    Copy full snippet
    ```
    \[Badges\] +DescriptionBadges=(Pattern="(?i)#\\\\s\*jira\\\\s\*:?\\\\s+(\[A-Za-z\]+-\[0-9\]+)", Name="$1", Group="Jira", Color="#c0c0c0", HoverColor="#e0e0e0", Url="https://jira.it.yourcompany.net/browse/$1")
    
    The following attributes were used in this example:
    
    | Attribute | Description |
    | --- | --- |
    | **Pattern** | Specifies a regex to match; it may capture portions of the matched text, which can be substituted later. |
    | **Label** | Specifies a label appearing on the badge. |
    | **Group** | Specifies an arbitrary identifier, grouping related badges rather than separating them with whitespace. |
    | **Color** | Specifies hexadecimal RGB values for badges. |
    | **HoverColor** | Specifies hexadecimal RGB values for badges on hover. |
    | **Url** | Specifies the path to open with a C# Process. Open call when the badge is clicked. |
    
-   Add a "Message of the day" along with a status panel color corresponding to a particular branch:
    
    ```
              `[//UE4/Main/Samples/Games/ShooterGame/ShooterGame.uproject]           Message=:alert: Lock-down for fixes is **5 pm on Friday**. Only fixes for the 1.2.3 release should be submitted to this branch. 123 issues are remaining as of 1/23.           StatusPanelColor=#e20000 		           Using the StatusPanelColor option enables you to easily identify streams. Additionally, when using the Message option, a limited subset of Markdown is supported, including: 		           [web links](http://www.google.com)           *italic*           _italic_           **bold**           __bold__`
    		
    Copy full snippet
    ```
    \[//UE4/Main/Samples/Games/ShooterGame/ShooterGame.uproject\] Message=:alert: Lock-down for fixes is \*\*5 pm on Friday\*\*. Only fixes for the 1.2.3 release should be submitted to this branch. 123 issues are remaining as of 1/23. StatusPanelColor=#e20000 Using the StatusPanelColor option enables you to easily identify streams. Additionally, when using the Message option, a limited subset of Markdown is supported, including: \[web links\](http://www.google.com) \*italic\* \_italic\_ \*\*bold\*\* \_\_bold\_\_
    
    Icons are supported using `:icon:` syntax; however, `:alert:` is the only icon that is currently available.
    
-   Customize the size and arrangement of badges in the CIS column:
    
    ```
              `[Default]           ColumnWidth_CIS=580           +BadgeGroups=Editor           +BadgeGroups=And, Lin, PS4, XB1, Win, IOS, Mac, Swi           +BadgeGroups=Content`
    		
    Copy full snippet
    ```
    \[Default\] ColumnWidth\_CIS=580 +BadgeGroups=Editor +BadgeGroups=And, Lin, PS4, XB1, Win, IOS, Mac, Swi +BadgeGroups=Content
-   Define project-specific sync filters with the following:
    
    ```
              `[Options]           +SyncCategory=(UniqueId="d9610e2f-7f6f-4898-bc98-d39dd7053d75", Name="FirstCategory", Paths="/MyGame/Content/Foo/...")`
    		
    Copy full snippet
    ```
    \[Options\] +SyncCategory=(UniqueId="d9610e2f-7f6f-4898-bc98-d39dd7053d75", Name="FirstCategory", Paths="/MyGame/Content/Foo/...")
    
    -   `UniqueId` should be a randomly generated GUID.
    -   `Name` displays in the UGS UI.
    -   `Paths` can be separated by semicolons.
    
    To modify existing category settings, specify its `GUID`, which is in the `DefaultSyncCategories` array in `.../UnrealGameSync/Workspace.cs`. By default, UGS will append your specified paths to the existing list, but setting `Clear=true` will replace it.
    

### Precompiled Binaries

To enable users to download precompiled Editor builds instead of compiling locally, you can submit a zip file containing the required binaries to Perforce, and have UnrealGameSync sync and extract that instead. Doing so uses the same user interface as compiling locally, but any changes that don't have matching binaries will be greyed out. Once configured, users can opt in to using precompiled binaries by checking the **Sync Precompiled Binaries** item under the **Options** menu.

To configure a path for precompiled binaries, add a `Build\UnrealGameSync.ini` file under your project and reference a location on the Perforce server where they are submitted, like this:

```
	`[//UE4/Main/Samples/Games/ShooterGame/ShooterGame.uproject] 	ZippedBinariesPath=//UE4/Dev-Binaries/++UE4+Main-Editor.zip`

Copy full snippet
```
\[//UE4/Main/Samples/Games/ShooterGame/ShooterGame.uproject\] ZippedBinariesPath=//UE4/Dev-Binaries/++UE4+Main-Editor.zip

It is recommended to use a location outside of your regular development stream for precompiled binaries, to avoid churn for anyone not using them. It is not necessary to maintain a separate workspace for this; UnrealGameSync will fetch them in a stateless way using the same login credentials that it uses to sync files.

It is not necessary to set up a metadata server to use precompiled binaries; the corresponding changelist for each zip file revision is parsed from the changelist description (it should start with the tag `[CL 12345678]`).

An example script showing how to create and submit editor binaries in the correct format is available at: `Engine/Build/Graph/Examples/BuildEditorAndTools.xml`

And a typical command-line to run it is as follows:

```
	`Engine\Build\BatchFiles\RunUAT.bat 	  BuildGraph 	  -Script=Engine/Build/Graph/Examples/BuildEditorAndTools.xml 	  -Target="Submit To Perforce for UGS" 	  -set:EditorTarget=ShooterGameEditor 	  -set:ArchiveStream=//UE4/Dev-Binaries 	  -p4 	  -submit`

Copy full snippet
```
Engine\\Build\\BatchFiles\\RunUAT.bat BuildGraph -Script=Engine/Build/Graph/Examples/BuildEditorAndTools.xml -Target="Submit To Perforce for UGS" -set:EditorTarget=ShooterGameEditor -set:ArchiveStream=//UE4/Dev-Binaries -p4 -submit

This will submit a zip file to `//UE4/Dev-Binaries/++UE4+Main-Editor.zip`, where `++UE4+Main` is the name of the current branch with slashes escaped as '+' characters. The same path should be set as the value for `ZippedBinariesPath` in `UnrealGameSync.ini`.

Additional information about using `BuildEditorAndTools.xml` can be found in the comments at the start of the file.

### Sync Filters

To learn more about this feature, read this reference about [Sync Filters](/documentation/en-us/unreal-engine/unreal-game-sync-filters-for-unreal-engine).